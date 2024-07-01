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
                sh 'npm run'
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