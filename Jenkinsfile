pipeline {
    agent any

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/codinTarantino/simple-java-maven-app.git'
            }
        }

        stage('Build') {
            steps {
                bat 'mvn clean compile'
            }
        }

        stage('Unit Test') {
            steps {
                bat 'mvn test'
            }
        }

        stage('Code Analysis (Optional)') {
            when {
                expression { return params.RUN_SONARQUBE == true }
            }
            steps {
                echo 'Running SonarQube analysis...'
                // Example if SonarQube installed:
                // bat 'mvn sonar:sonar'
            }
        }

        stage('Package') {
            steps {
                bat 'mvn package'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying application...'
                bat 'mkdir target\\deploy'
                bat 'copy target\\simple-java-maven-app-1.0-SNAPSHOT.jar target\\deploy\\'
                echo 'Application deployed successfully to target\\deploy\\'
            }
        }
    }

    post {
        success {
            echo 'Pipeline executed successfully!'
        }
        failure {
            echo 'Pipeline failed.'
        }
    }
}
