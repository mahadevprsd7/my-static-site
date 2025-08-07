pipeline {
    agent any

    stages {
        stage('Clone Repo') {
            steps {
                echo 'Repository cloned by Jenkins'
            }
        }
        stage('Build Docker Image') {
            steps {
                bat 'docker build -t static-website'
            }
        }
        stage('Run Container') {
            steps {
                bat ''' 
                docker stop static-site || exit 0
                docker rm static-site || exit 0
                docker run -d -p 8080:80 --name static-site static-website
                '''
            }
        }
    }
    post {
        success {
            echo 'Static Website deployed successfully'
        }
        failure {
            echo 'Build Failed'
        }
    }
}