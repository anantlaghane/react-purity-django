pipeline {
    agent any

    environment {
        DOCKERHUB_CREDENTIALS = credentials('docker')  // Jenkins credentials
        DOCKERHUB_USERNAME = 'anantlaghane'
    }

    stages {
        stage('Checkout') {
            steps {
                checkout([
                    $class: 'GitSCM',
                    branches: [[name: '*/main']],
                    userRemoteConfigs: [[
                        url: 'https://github.com/anantlaghane/react-purity-django.git',
                        credentialsId: 'Git'
                    ]]
                ])
            }
        }

        stage('Build Frontend Image') {
            steps {
               dir('react-ui') {
                     sh 'docker build -t $DOCKERHUB_USERNAME/react-frontend:latest .'
                 }
            }
        }


        stage('Build Backend Image') {
            steps {
                dir('api-server-django') {
                    sh 'docker build -t $DOCKERHUB_USERNAME/django-backend:latest .'
                }
            }
        }

        stage('Push Images to Docker Hub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-creds', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                    sh '''
                    echo "$PASSWORD" | docker login -u "$USERNAME" --password-stdin
                    docker push $DOCKERHUB_USERNAME/react-frontend:latest
                    docker push $DOCKERHUB_USERNAME/django-backend:latest
                    '''
                }
            }
        }

        // stage('Deploy to Kubernetes') {
        //     steps {
        //         sh 'kubectl apply -f k8s/'
        //     }
        // }
    }
}
