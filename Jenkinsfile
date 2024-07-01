pipeline{
    agent any

    tools{
        nodejs "nodejs"
    }
    stages {
        stage('clone repository'){
            steps {
                git url: "https://github.com/kelvin-kk/gallery.git", branch: "master"
            }
        }
        stage('Build') {
            steps {
                sh 'npm install'
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
                slackSend color: "good", message: "Pipeline ran successfully"
            }
            failure {
                slackSend color: "danger", message: "Pipeline failed"
            }
        }
    }