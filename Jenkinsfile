
pipeline {
    agent any

    triggers {
        githubPush()
    }

    tools {
        maven 'MAVEN-HOME'
    }

    stages {
        stage('Git Clone') {
            steps {
                bat 'if exist mavenjava rmdir /s /q mavenjava'
                bat 'git clone https://github.com/pranathi-13/mavenjava.git'
            }
        }

        stage('Clean') {
            steps {
                bat 'mvn clean -f mavenjava/pom.xml'
            }
        }

        stage('Compile') {
            steps {
                bat 'mvn compile -f mavenjava/pom.xml'
            }
        }

        stage('Test') {
            steps {
                bat 'mvn test -f mavenjava/pom.xml'
            }
        }

        stage('Package') {
            steps {
                bat 'mvn package -f mavenjava/pom.xml'
            }
        }

        stage('Docker Build') {
            steps {
                bat 'docker version'
                bat 'docker build -t mavenjava:latest mavenjava'
            }
        }
    }

    post {
        success {
            echo 'Maven build and Docker image creation completed successfully!'
        }
        failure {
            echo 'Pipeline failed. Check Console Output.'
        }
    }
}
