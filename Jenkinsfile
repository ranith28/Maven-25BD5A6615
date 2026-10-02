pipeline {
    agent any

    tools {
        maven 'MAVEN_HOME'
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'master', url: 'https://github.com/ranith28/Maven-25BD5A6615.git'
            }
        }

        stage('Build') {
            steps {
                dir('MavenWebProject25BD5A6615') {
                    bat 'mvn clean package'
                }
            }
        }

        stage('Test') {
            steps {
                dir('MavenWebProject25BD5A6615') {
                    bat 'mvn test'
                }
            }
        }

        stage('Docker Build') {
            steps {
                dir('MavenWebProject25BD5A6615') {
                    bat 'docker build -t webimage .'
                }
            }
        }

        stage('Docker Run') {
            steps {
                bat 'docker run -d -p 8094:8080 webimage'
            }
        }
    }

    post {
        success {
            mail to: 'userkmit11@gmail.com',
                 subject: "Success: Pipeline ${env.JOB_NAME} [Build #${env.BUILD_NUMBER}]",
                 body: "The pipeline completed successfully!\n\nView the logs here: ${env.BUILD_URL}"
        }

        failure {
            mail to: 'userkmit11@gmail.com',
                 subject: "Failure: Pipeline ${env.JOB_NAME} [Build #${env.BUILD_NUMBER}]",
                 body: "The build has failed.\n\nCheck the console output: ${env.BUILD_URL}console"
            
        }
    }
}
