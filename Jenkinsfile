pipeline {
    agent any

    environment {
        IMAGE_NAME = "mi-app:latest"
    }

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }
//////
        stage('Build') {
            steps {
                sh 'mvn clean package -DskipTests -Dmaven.test.skip=true'
            }
        }

        stage('Static Analysis (SonarQube)') {
            steps {
                withCredentials([string(credentialsId: 'sonar-token', variable: 'SONAR_TOKEN')]) {
                    sh '''
                    mvn sonar:sonar \
                    -Dsonar.projectKey=my-app \
                    -Dsonar.host.url=http://host.docker.internal:9000 \
                    -Dsonar.token=$SONAR_TOKEN
                    '''
                }
            }
        }//

        stage('Quality Gate') {
            steps {
                script {
                    sleep(30)
                    def result = sh(
                        script: "curl -s http://host.docker.internal:9000/api/qualitygates/project_status?projectKey=my-app",
                        returnStdout: true
                    )
                    if (!result.contains('"status":"OK"')) {
                        error("Quality Gate FAILED")
                    }
                }
            }
        }

        stage('Docker Build') {
            steps {
                sh 'docker build -t $IMAGE_NAME .'
            }
        }

        stage('Security Scan (Trivy)') {
            steps {
                sh 'trivy image --exit-code 1 --severity CRITICAL $IMAGE_NAME'
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                docker stop mi-app || true
                docker rm mi-app || true
                docker run -d -p 80:8080 --name mi-app $IMAGE_NAME
                '''
            }
        }
    }

    post {
        always {
            sh 'docker system prune -f || true'
            cleanWs()
        }
        failure {
            echo "Pipeline falló"
        }
    }
}