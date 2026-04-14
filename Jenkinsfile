pipeline {
    agent any;

    stages{
        stage("Checkout"){
            steps{
                echo "Code already checked out by multibranch pipeline"
            }
        }

        stage("Build"){
            steps{
                sh "docker build -t user-service:${env.BUILD_NUMBER}"
            }
        }

        stage("Test"){
            parallel{
                stage("Unit Test"){
                    steps {
                        echo "Running unit tests..."
                    }
                }
                stage("Integration Test"){
                    steps {
                        echo "Running integration tests..."
                    }
                }
            }
        }

        stage("Deploy"){
            steps {
                sh "docker run -d -p 3001:3000 user-service:${env.BUILD_NUMBER}"
            }
        }
    }
}