pipeline {
    agent any

    environment {
        IMAGE_NAME = "yourdockerhub/simpleapp"
        TAG = "v${BUILD_NUMBER}"
    }

    stages {
        stage('Clone') {
            steps {
                git 'https://github.com/yourname/simpleapp-cicd.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh "docker build -t $IMAGE_NAME:$TAG ."
            }
        }

        stage('Push Image to DockerHub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-creds', usernameVariable: 'USER', passwordVariable: 'PASS')]) {
                    sh '''
                        echo $PASS | docker login -u $USER --password-stdin
                        docker push $IMAGE_NAME:$TAG
                    '''
                }
            }
        }

        stage('Deploy to K8s') {
            steps {
                script {
                    sh "sed -i 's|image:.*|image: $IMAGE_NAME:$TAG|' k8s/deployment.yaml"
                    sh "kubectl apply -f k8s/"
                }
            }
        }
    }
}
