pipeline {
    agent any

    environment {
        DOCKERHUB_CREDENTIALS = credentials('dckr_pat_ZT9S60N33HDbz6uHUx9wKjptSJE')
        DOCKER_IMAGE = 'martin8207/students-with-jenkinsfile'
        DOCKER_TAG = "${BUILD_NUMBER}"
    }

    stages {
        stage('Install Dependencies') {
            steps {
                // Install npm dependencies
                bat 'npm install'
            }
        }

       
        
        stage('Run Audit') {
            steps {
                // Run tests
                bat 'npm audit'
            }
        }

        stage('Run Test') {
            steps {
                // Run tests
                bat 'npm test'
            }
        }
         /*  stage('Build') {
            steps {
                // Build the application
                  echo 'Hellow World'   
            }
        }*/

        stage('Build Docker Image') {
            steps {
                script {
                    // Build Docker image
                    bat "docker build -t ${DOCKER_IMAGE}:${DOCKER_TAG} ."
                    bat "docker tag ${DOCKER_IMAGE}:${DOCKER_TAG} ${DOCKER_IMAGE}:latest"
                }
            }
        }

        stage('Push to DockerHub') {
            steps {
                script {
                    // Login to DockerHub
                    bat 'echo %DOCKERHUB_CREDENTIALS_PSW%| docker login -u %DOCKERHUB_CREDENTIALS_USR% --password-stdin'
                    
                    // Push Docker images
                    bat "docker push ${DOCKER_IMAGE}:${DOCKER_TAG}"
                    bat "docker push ${DOCKER_IMAGE}:latest"
                    
                    // Logout from DockerHub
                    bat 'docker logout'
                }
            }
        }

        stage('Deploy') {
            steps {
                // Manual approval before deployment
                input message: 'Proceed with deployment?'
                
                // Add deployment steps here
                echo 'echo Deploying the application...'
            }
        }  
    }

    post {
        always {
            // Clean up Docker images
            script {
                bat "docker rmi ${DOCKER_IMAGE}:${DOCKER_TAG}"
                bat "docker rmi ${DOCKER_IMAGE}:latest"
            }
        }
    }
}
