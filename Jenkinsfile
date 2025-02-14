pipeline {
    agent any
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

        stage('Deploy') {
            steps {
                // Add deployment steps here
                echo 'echo Deploying the application...'
            }
        }  
    }
}
