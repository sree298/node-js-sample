pipeline {
    agent any
    environment {
        DOCKER_IMAGE = "srinu298/node-js-sample:1.0"
        PATH = "/usr/local/bin:$PATH" 
        KUBECONFIG = '/home/labuser/.kube/config' // Define the KUBECONFIG environment variable
    }
    stages {
        stage('Clone Repository') {
            steps {
                git credentialsId: 'git-credentials', url: 'https://github.com/sree298/node-js-sample.git', branch: 'main'
                sh 'echo $?'
                sh 'echo "successfully cloned"'
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
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
                        sh "echo ${DOCKER_PASSWORD} | docker login -u ${DOCKER_USERNAME} --password-stdin"
                        sh "docker push ${DOCKER_IMAGE}"
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
