pipeline {
    agent any

    tools {
        sonarQubeScanner 'SonarScanner'
    }

    environment {
        IMAGE_NAME = "femiwebsite"
        IMAGE_TAG = "project"
        CONTAINER_NAME = "femiwebsite"
        HOST_PORT = "8081"
        CONTAINER_PORT = "80"
    }

    stages {

        stage('Clone Source') {
            steps {
                echo "Using source code from Jenkins workspace..."
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('SonarQube') {
                    sh '''
                        sonar-scanner \
                        -Dsonar.projectKey=FEMIWEBSITE \
                        -Dsonar.projectName=FEMIWEBSITE \
                        -Dsonar.sources=.
                    '''
                }
            }
        }

        stage('Trivy Filesystem Scan') {
            steps {
                sh 'trivy fs --severity HIGH,CRITICAL .'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t ${IMAGE_NAME}:${IMAGE_TAG} .'
            }
        }

        stage('Trivy Image Scan') {
            steps {
                sh 'trivy image --severity HIGH,CRITICAL ${IMAGE_NAME}:${IMAGE_TAG}'
            }
        }

        stage('Stop Old Container') {
            steps {
                sh '''
                    docker stop ${CONTAINER_NAME} || true
                    docker rm ${CONTAINER_NAME} || true
                '''
            }
        }

        stage('Run New Container') {
            steps {
                sh '''
                    docker run -d \
                    --name ${CONTAINER_NAME} \
                    -p ${HOST_PORT}:${CONTAINER_PORT} \
                    ${IMAGE_NAME}:${IMAGE_TAG}
                '''
            }
        }
    }

    post {
        always {
            archiveArtifacts artifacts: '*.txt', allowEmptyArchive: true
        }

        success {
            echo "Deployment completed successfully!"
        }

        failure {
            echo "Deployment failed!"
        }
    }
}
