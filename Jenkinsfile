pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'master', url: 'https://github.com/A-B-USERS/opensourcepos.git'
            }
        }
     
        stage('Update Branding') {
            steps {
                // Replace "opensourcePOS" with "ITSW" in your header file (adjust path if needed)
                sh 'sed -i "s/opensourcePOS/ITSW/g" application/views/header.php'
             }
         }



        
        stage('Build & Deploy') {
            steps {
                sh 'docker compose down'
                sh 'docker compose up -d --build'
            }
        }

        stage('Test') {
            steps {
                sh 'echo "POS system deployed! Add tests here if needed."'
            }
        }
    }

    post {
        success {
            echo "✅ Deployment successful!"
        }
        failure {
            echo "❌ Deployment failed!"
        }
    }
}
