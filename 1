pipeline {
    agent any

    options {
        timestamps()
        disableConcurrentBuilds()
    }

    environment {
        AWS_REGION   = 'ap-south-1'
        EKS_CLUSTER  = 'trend-cluster'
        DOCKERHUB_USER = 'praveenappu'
        IMAGE_NAME   = 'trend-store'
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
                sh 'git rev-parse --short HEAD'
            }
        }

        stage('Validate Files') {
            steps {
                sh '''
                    test -f Dockerfile
                    test -f nginx.conf
                    test -f k8s/deployment.yaml
                    test -f k8s/service.yaml
                    test -f dist/index.html
                '''
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    env.IMAGE_TAG = sh(
                        script: 'git rev-parse --short HEAD',
                        returnStdout: true
                    ).trim()
                }
                sh '''
                    docker build \
                      -t ${DOCKERHUB_USER}/${IMAGE_NAME}:${IMAGE_TAG} \
                      -t ${DOCKERHUB_USER}/${IMAGE_NAME}:latest .
                '''
            }
        }

        stage('Test Container') {
            steps {
                sh '''
                    set -e
                    docker rm -f trend-ci-test 2>/dev/null || true

                    docker run -d --name trend-ci-test \
                      -p 127.0.0.1:13000:3000 \
                      ${DOCKERHUB_USER}/${IMAGE_NAME}:${IMAGE_TAG}

                    trap 'docker rm -f trend-ci-test >/dev/null 2>&1 || true' EXIT

                    for i in $(seq 1 15); do
                      if curl -fsS http://127.0.0.1:13000/health; then
                        exit 0
                      fi
                      sleep 2
                    done

                    docker logs trend-ci-test
                    exit 1
                '''
            }
        }

        stage('Push Image') {
            steps {
                withCredentials([
                    usernamePassword(
                        credentialsId: 'dockerhub-creds',
                        usernameVariable: 'DH_USER',
                        passwordVariable: 'DH_TOKEN'
                    )
                ]) {
                    sh '''
                        set +x
                        echo "$DH_TOKEN" | docker login \
                          -u "$DH_USER" --password-stdin

                        docker push \
                          ${DOCKERHUB_USER}/${IMAGE_NAME}:${IMAGE_TAG}

                        docker push \
                          ${DOCKERHUB_USER}/${IMAGE_NAME}:latest

                        docker logout
                    '''
                }
            }
        }

        stage('Deploy to EKS') {
            steps {
                sh '''
                    set -e

                    aws eks update-kubeconfig \
                      --region "$AWS_REGION" \
                      --name "$EKS_CLUSTER"

                    kubectl set image deployment/trend-store \
                      trend-store=${DOCKERHUB_USER}/${IMAGE_NAME}:${IMAGE_TAG} \
                      --namespace default

                    kubectl rollout status deployment/trend-store \
                      --namespace default --timeout=300s

                    kubectl get deployment trend-store
                    kubectl get pods -o wide
                    kubectl get service trend-store-service
                '''
            }
        }

        stage('Verify Application') {
            steps {
                sh '''
                    kubectl get endpoints trend-store-service
                    kubectl get deployment trend-store \
                      -o jsonpath='{.status.availableReplicas}{"\\n"}'
                '''
            }
        }
    }

    post {
        always {
            sh 'docker rm -f trend-ci-test 2>/dev/null || true'
        }
        success {
            echo 'Trend Store CI/CD completed successfully.'
        }
        failure {
            echo 'Pipeline failed. Review the stage console output.'
        }
    }
}

