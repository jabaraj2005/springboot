pipeline {
    agent {
        label 'AgentA'
    }

    environment {
        IMAGE_NAME = "dockerhub-username/springboot-ci-cd"
        DOCKER_CREDS = credentials('dockerhub-creds')
    }

    triggers {
        githubPush()
    }

    stages {

        stage('Checkout Code') {
            steps {
                checkout scm
            }
        }

        stage('Maven Build') {
            steps {
                sh '''
                    mvn clean package -DskipTests
                '''
            }
        }

        stage('Docker Build') {
            steps {
                sh '''
                    docker build -t $IMAGE_NAME:latest .
                    docker tag $IMAGE_NAME:latest $IMAGE_NAME:${BUILD_NUMBER}
                '''
            }
        }

        stage('Docker Login') {
            steps {
                sh '''
                    echo $DOCKER_CREDS_PSW | docker login -u $DOCKER_CREDS_USR --password-stdin
                '''
            }
        }

        stage('Docker Push') {
            steps {
                sh '''
                    docker push $IMAGE_NAME:latest
                    docker push $IMAGE_NAME:${BUILD_NUMBER}
                '''
            }
        }

        stage('Deploy using Docker Compose') {
            steps {
                sh '''
                    docker compose down || true
                    docker compose pull
                    docker compose up -d
                '''
            }
        }
    }

    post {
        success {
            echo "✅ CI/CD completed successfully"
        }
        failure {
            echo "❌ Pipeline failed"
        }
    }
}
