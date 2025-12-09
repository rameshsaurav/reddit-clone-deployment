pipeline {
    agent { label 'k8s-agent' }

    environment {
        DOCKER_USERNAME = credentials('docker-username')
        DOCKER_PASSWORD = credentials('docker-password')
    }

    stages {

        stage('Clone Code') {
            steps {
                git branch: 'main', url: 'https://github.com/rameshsaurav/reddit-clone-deployment.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t ${DOCKER_USERNAME}/reddit-clone:${BUILD_NUMBER} .'
                //sh 'docker tag reddit-clone:${BUILD_NUMBER} ${DOCKER_USERNAME}/reddit-clone:${BUILD_NUMBER}'
            }
        }

        stage('Push to DockerHub') {
            steps {
                sh "echo ${DOCKER_PASSWORD} | docker login -u ${DOCKER_USERNAME} --password-stdin"
                sh 'docker push ${DOCKER_USERNAME}/reddit-clone:${BUILD_NUMBER}'
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                sh '''
                cd k8
                kubectl apply -f deployment.yml
                kubectl apply -f service.yml
                '''
            }
        }
        
        stage('Show Service URL') {
            steps {
                sh '''
                echo "========= Minikube Service URL ========="
                minikube service reddit-clone-service --url 2>/dev/null || true
                '''
            }
        }
    }
}
