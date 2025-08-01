pipeline {
    agent any

    environment {
        COMPOSE_PROJECT_NAME = "myapp"
        COMPOSE_FILE = "docker-compose.yml" // change path if needed
    }

    stages {
        stage('Checkout') {
            steps {
                git credentialsId: 'Github-ID', url: 'https://github.com/NeetGupta/task-tracke-rDocker.git', branch: 'main'
            }
        }

        stage('Deploy with Docker Compose') {
            steps {
                script {
                    sh 'docker-compose down || true' // optional: stop previous containers
                    sh 'docker-compose pull'         // pull latest images
                    sh 'docker-compose up -d --build'
                }
            }
        }
    }

    post {
        success {
            echo 'Deployment successful!'
        }
        failure {
            echo 'Deployment failed.'
        }
    }
}
