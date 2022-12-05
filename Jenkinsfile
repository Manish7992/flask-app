

def COLOR_MAP = ['SUCCESS': 'good', 'FAILURE': 'danger', 'UNSTABLE': 'danger', 'ABORTED': 'danger']

pipeline {
    agent any
    environment {
        DATE = new Date().format('yy.M')
        TAG = "${DATE}.${BUILD_NUMBER}"
    }
    stages {
        stage('Build') {
            steps {
	            sh 'echo build '
            }
        }
        stage('Docker Build and push') {
            steps {
               sh "docker build -t manish8757/rancher:${GIT_COMMIT} . "
               sh "docker login -u manish8757 -p manish123@"
               sh "docker push manish8757/rancher:${GIT_COMMIT} "
            }
        }
        
    }

}
