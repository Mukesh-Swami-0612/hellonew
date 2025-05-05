pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'mukesh0612/hello'
    }

    stages {
        stage('Clone Repo') {
            steps {
                git branch: 'main', credentialsId: 'github-token', url: 'https://github.com/Mukesh-Swami-0612/hellonew.git'
            }
        }

        stage('Manual Docker Build') {
            steps {
                script {
                    bat "docker build -t ${DOCKER_IMAGE} ."
                }
            }
        }

        stage('Push to DockerHub') {
            steps {
                script {
                    withDockerRegistry([credentialsId: 'docker-deploy', url: 'https://index.docker.io/v1/']) {
                        docker.image("${DOCKER_IMAGE}").push('latest')
                    }
                }
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed.'
        }
    }
}
