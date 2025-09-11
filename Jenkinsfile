pipeline {
    agent any

    environment {
        DOCKERHUB_CREDENTIALS = credentials('dockerhub-creds')   // Jenkins credentials ID
        DOCKER_IMAGE = "nufailans107/nuf-chatapp"
        KUBECONFIG_CREDENTIALS = credentials('kubeconfig-creds') // Jenkins credentials ID
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/Nufail-ans-107/Nuf-chatApp.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    sh 'docker build -t $DOCKER_IMAGE:$BUILD_NUMBER .'
                }
            }
        }

        stage('Trivy Scan') {
            steps {
                script {
                    sh '''
                    docker run --rm \
                      -v /var/run/docker.sock:/var/run/docker.sock \
                      aquasec/trivy:latest image --exit-code 0 --severity HIGH,CRITICAL $DOCKER_IMAGE:$BUILD_NUMBER
                    '''
                }
            }
        }

        stage('Push to Docker Hub') {
            steps {
                script {
                    sh '''
                    echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin
                    docker push $DOCKER_IMAGE:$BUILD_NUMBER
                    '''
                }
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                script {
                    // Save kubeconfig from Jenkins credentials
                    writeFile file: 'kubeconfig', text: KUBECONFIG_CREDENTIALS
                    withEnv(["KUBECONFIG=${WORKSPACE}/kubeconfig"]) {
                        sh '''
                        kubectl apply -f k8s/
                        kubectl set image deployment/chatapp-deployment chatapp=$DOCKER_IMAGE:$BUILD_NUMBER -n default
                        kubectl rollout status deployment/chatapp-deployment -n default
                        '''
                    }
                }
            }
        }
    }
}
