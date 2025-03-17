pipeline {
    agent any
    environment {
        DOCKER_IMAGE = "srinu298/node-js-sample:1.0"
        PATH = "/usr/local/bin:$PATH" 
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
                    withCredentials([file(credentialsId: 'k8s-config', variable: 'KUBECONFIG')]) {
                        sh 'kubectl apply -f k8s/deployment.yaml --kubeconfig=$KUBECONFIG'
                        sh 'kubectl apply -f persistent-volume.yaml --kubeconfig=$KUBECONFIG'
                        sh 'kubectl apply -f network-policy.yaml --kubeconfig=$KUBECONFIG'
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
            echo 'Pipeline failed!'
        }
    }
}
