podTemplate(label: 'dnscontrolpod', containers: [
    containerTemplate(name: 'docker', image: 'docker', ttyEnabled: true, command: 'cat'),
    containerTemplate(name: 'kubectl', image: 'lachlanevenson/k8s-kubectl:v1.8.0', command: 'cat', ttyEnabled: true)
  ],
  volumes: [
    hostPathVolume(mountPath: '/var/run/docker.sock', hostPath: '/var/run/docker.sock'),
  ]) {
    node('dnscontrolpod') {

       stage('Preview DNS-Control') {
           if (env.BRANCH_NAME == 'master') {
	   checkout scm		   
               echo 'Preview changes'
               container('kubectl') { 
		  BRANCH_NAME_LC=env.BRANCH_NAME.toLowerCase()
      		  sh "kubectl run --attach pipeline-dnscreate-preview-$BRANCH_NAME_LC --image=docker-sbx.artifactory.sbx.infra.aws-us-east-1.mlbinfra.net/dnscreate:latest --env='COMMAND=preview' --env='REPO_NAME=dnscontrol-conf' --env=BRANCH_NAME=$BRANCH_NAME -n default"
                  sh "kubectl delete deployment pipeline-dnscreate-preview-$BRANCH_NAME_LC -n default"
                  sh "kubectl run --attach pipeline-dnscontrol-preview-$BRANCH_NAME_LC --image=docker-sbx.artifactory.sbx.infra.aws-us-east-1.mlbinfra.net/dnscontrol:latest --env='COMMAND=preview' --env='REPO_NAME=dnscontrol-conf' --env=BRANCH_NAME=$BRANCH_NAME -n default"
                  sh "kubectl delete deployment pipeline-dnscontrol-preview-$BRANCH_NAME_LC -n default"
     
               }                
           } else {
               echo 'Nothing to do in this stage.'
           }
       }

    }
}
