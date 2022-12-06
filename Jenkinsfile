

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
	stage('Git Push'){
        steps{
        script{
            GIT_CREDS = credentials('manish-git-cred')
            sh '''
                echo ${GIT_PREVIOUS_SUCCESSFUL_COMMIT}
                rm -rf flask-frontend-k8s-menifest
                git clone https://github.com/Manish7992/flask-frontend-k8s-menifest.git
                cd flask-frontend-k8s-menifest
                cat deployment.yaml
                git pull 
                sed -i " s%manish8757/rancher:${GIT_PREVIOUS_SUCCESSFUL_COMMIT}%manish8757/rancher:${GIT_COMMIT}%g" deployment.yaml
                git status
                git add deployment.yaml
                git commit -m  "This is manish8757/rancher "
                git push 
            '''
             }
          }
        }
        
    }

}
