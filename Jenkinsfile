pipeline {
    agent any
    environment {
        YOUR_NAME = credentials("YOUR_NAME")
    }
    stages {
        stage('Build') {
            steps {
                sh '''
                docker build -t pixcs13/task1jenk .
                '''
            }

        }
        stage('Push') {
            steps {
                sh '''
                docker push pixcs13/task1jenk
                '''
            }

        }
        stage('Deploy') {
            steps {
                sh '''
                sed -e 's,{{password}},'${YOUR_NAME}',g;' db-password.yaml | kubectl apply -f -
                kubectl apply -f task1-manifest.yaml
                kubectl apply -f nginx-config.yaml
                kubectl apply -f nginx-pod.yaml
                sleep 60
                kubectl get services
                '''
            }

        }

    }

}