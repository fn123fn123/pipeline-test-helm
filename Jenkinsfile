pipeline {
    agent {
      docker { image 'alpine' }
  }
    stages {
        stage('Say Hi') {
            steps {
                echo 'Hello World..'
            }
        }
        stage('Preview') {
            steps {
                echo 'Testing..'
            }
        }
        stage('Configure') {
            steps {
                echo 'Deploying....'
            }
        }
    }
}
