pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/mohamedbenaoune25-netizen/Devops-4SSA12.git'
            }
        }

        stage('Création de l\'image Docker') {
            steps {
                dir('backend') {
                    sh 'docker build -t mohamed5012/studentmang-app:latest .'
                }
            }
        }

        stage('Push de l\'image sur Docker Hub') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'dockerhub-credentials',
                    usernameVariable: 'DOCKER_USER',
                    passwordVariable: 'DOCKER_PASS'
                )]) {
                    sh '''
                        echo "$DOCKER_PASS" | docker login -u "$DOCKER_USER" --password-stdin
                        docker push mohamed5012/studentmang-app:latest
                        docker logout
                    '''
                }
            }
        }
    }
}
