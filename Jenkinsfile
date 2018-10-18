pipeline {
    agent {
        docker { image 'node:7-alpine' }
    }

    stages {
        stage('Build') {
            steps {
                echo 'Building..'
                sh 'docker run -it --rm -v $PWD:/data -w /data node npm install'
            }
        }
        stage('Test') {
            steps {
                echo 'Testing..'
                sh 'docker run -it --rm -v $PWD:/data -w /data node npm test'
            }
        }
        stage('Deploy') {
            when {
              expression {
                currentBuild.result == null || currentBuild.result == 'SUCCESS' 
              }
            }
            steps {
                echo 'make publish...'
            }
        }
    }
}