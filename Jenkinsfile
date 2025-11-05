pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo " Checking out the repository..."
                git branch: 'master', url: 'https://github.com/A-B-USERS/opensourcepos.git'
            }
        }

        stage('Debug Workspace') {
            steps {
                echo "🛠 Debugging workspace structure..."
                sh 'pwd'
                sh 'ls -R'
            }
        }

        stage('Update Branding') {
            steps {
                script {
                    // Jenkins workspace ka path le lo
                    def workspace = env.WORKSPACE
                    def headerFile = "${workspace}/application/views/header.php"

                    // Check karo file exist karti hai ya nahi
                    if (fileExists(headerFile)) {
                        echo " Updating branding in header.php..."
                        sh "sed -i 's/opensourcePOS/ITSW/g' ${headerFile}"
                    } else {
                        error "❌ File not found: ${headerFile}"
                    }
                }
            }
        }

        stage('Build & Deploy') {
            steps {
                script {
                    def workspace = env.WORKSPACE
                    echo " Building and deploying Docker containers..."
                    dir("${workspace}") {
                        // Safe docker compose down (agar containers run nahi ho rahe toh error na aaye)
                        sh 'docker compose down || true'
                        sh 'docker compose up -d --build'
                    }
                }
            }
        }

        stage('Test') {
            steps {
                echo " Running post-deployment checks..."
                sh 'echo "✅ POS system deployed successfully! Add automated tests here if needed."'
            }
        }
    }

    post {
        success {
            echo " Deployment completed succ
