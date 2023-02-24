pipeline {
    agent { label 'jenk-deploy' }
    stages {
        stage('build') {
            steps {
            	withCredentials([usernamePassword(credentialsId: 'my-app', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                    sh   """
                        docker login -u $USERNAME -p $PASSWORD
                        docker build -t alzahraa14/hello-world ./my-app/
                        docker push alzahraa14/hello-world
                    """
                 }
            }
        }
        stage('deploy') {
            steps {
                    sh    """
                        kubectl apply -f k8s -n dev
                    """
            }
        }
    }
}