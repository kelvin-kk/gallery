pipeline{
    agent any

    tools{
        nodejs "nodejs"
    }
    stages {
        stage('clone repository'){
            steps {
                git 'https://github.com/kelvin-kk/gallery.git'
            }
        }
        stage('Build ') {
            steps {
                    npm install 
            }
        }
        stage('Test'){
            steps {
                echo 'Testing the project' {
                    sh 'npm test'
                }
            }
        }
    }
    post {
            success {
                slackSend color: "good", message: "Build #${BUILD_NUMBER} ran successfully"
            }
            failure {
                slackSend color: "danger", message: "Build #${BUILD_NUMBER} failed"
            }
        }
    }