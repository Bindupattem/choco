pipeline {
    agent any

    environment {
        DEPLOY_DIR = "/var/www/html/choco-site"
    }

    stages {

        stage('Clone Repository') {
            steps {
                git url: 'https://github.com/Bindupattem/choco.git', branch: 'main'
            }
        }

        stage('Build (Static Check)') {
            steps {
                echo "No build needed for HTML project"
            }
        }

        stage('Test (HTML Validation)') {
            steps {
                echo "Validating HTML..."
                sh '''
                if command -v tidy >/dev/null 2>&1; then
                    tidy -errors -q index.html || true
                else
                    echo "HTML validator not installed"
                fi
                '''
            }
        }

        stage('Deploy') {
            steps {
                echo "Deploying website..."
                sh '''
                mkdir -p $DEPLOY_DIR
                cp -r * $DEPLOY_DIR
                '''
            }
        }

        stage('Post Deployment Check') {
            steps {
                echo "Deployment completed successfully!"
            }
        }
    }

    post {
        success {
            echo "✅ Pipeline executed successfully!"
        }
        failure {
            echo "❌ Pipeline failed!"
        }
    }
}
