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
        pollSCM('H/2 ')
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