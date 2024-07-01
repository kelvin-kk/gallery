pipeline{
    agent any

    environment{
        RENDER_APP_NAME = 'gallery'
        SLACK_CHANNEL = 'project'
        SLACK_CREDENTIALS_ID = 'SLACK-TOKEN-API'
        EMAIL_RECIPIENT = 'kelvinkiariek@gmail.com'
    }

    tools{
        nodejs "nodejs"
    }

    triggers {
        pollSCM('0 */4 * * 1-5')
    }

    stages {
        stage('clone repository'){
            steps {
                git branch: 'master', url: 'https://github.com/kelvin-kk/gallery'
            }
        }

        stage('Build') {
            steps {
                sh 'npm install'
                sh 'npm run'
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests...'
                sh 'npm test'
            }
        }

        stage('Start server') {
            steps {
                echo 'Starting server...'
                sh 'npm start &'
            }
        }

        stage('Deploy to Render') {
            steps {
                script {
                    // Use credentials binding for RENDER_API_KEY
                    withCredentials([string(credentialsId: 'render_api_key', variable: 'RENDER_API_KEY')]) {
                        sh "curl -X POST -H 'Authorization: Bearer \${RENDER_API_KEY}' \
                            -H 'Content-Type: application/json' \
                            -d '{\"branch\": \"master\", \"env\": {\"NODE_ENV\": \"production\"}}' \
                            https://api.render.com/v1/services/${RENDER_APP_NAME}/deploy"
                    }
                }
            }
        }


    }
    
    post {
            success {
                echo "Pipeline ran successfully"
            }
            failure {
                echo "Pipeline failed"
            }
        }
    }