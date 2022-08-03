pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo 'Checking out...'
                git credentialsId: 'pedronogpereira-github-credentials', url:'https://github.com/PedroNogPereira/devops.git', branch: 'main'
            }
        }
        stage('Build') {
            steps {
                echo 'Building...'
                dir('my-app'){
                    sh 'npm install @angular/cli'
                    sh 'npm run build'
                }
            }
        }
        stage ('Docker Image') {
          steps {
            script {
                docker.withRegistry('https://registry.hub.docker.com', 'pedronogpereira-dockerhub-credentials') {
                    def customImage = docker.build("pedronogpereira/main_image:${env.BUILD_ID}")
                    customImage.push()
                }
            }
          }
        }
    }
}