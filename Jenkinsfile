pipeline {
    agent any
    environment {
        PATH = "/usr/local/bin:$PATH" 
    }
    stages {
        stage('Clone Repository') {
            steps {
                //cleanWs()
                // Clone the Git repository
                git credentialsId: 'git-credentials', url: 'https://github.com/zendesk/node-js-sample.git', branch: 'main' // Replace with your Git repository
                sh 'echo $?'
                sh 'echo "successfully cloned"'
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    // Build the Docker image
                    sh 'docker --version'
                    sh 'docker build -t ${DOCKER_IMAGE} .'
                    sh 'docker images'
                }
            }
        }
        stage('Push to Docker Hub') {
            steps {
                script {
                    withCredentials([usernamePassword(credentialsId: 'dockerhub-credentials', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]) {
                        // Log in to Docker Hub using username and password
                        sh "echo ${DOCKER_PASSWORD} | docker login -u ${DOCKER_USERNAME} --password-stdin"
                        // Push the Docker image to Docker Hub
                        sh "docker push sandip9292/node-js-sample:1.0"
                    }
                }
            }
        }
        stage('Deploy to Kubernetes') {
            steps {
                script {
                    // Apply the Kubernetes deployment
                    sh 'kubectl apply -f k8s/deployment.yaml'
                    sh 'kubectl apply -f persistent-volume.yaml'
                    sh 'kubectl apply -f network-policy.yaml'
                }
            }
        }
    }
    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}
