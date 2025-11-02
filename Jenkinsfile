pipeline {
    agent any

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/<your-username>/simple-java-maven-app.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean compile'
            }
        }

        stage('Unit Test') {
            steps {
                sh 'mvn test'
            }
        }

        stage('Code Analysis (Optional)') {
            when {
                expression { return params.RUN_SONARQUBE == true }
            }
            steps {
                echo 'Running SonarQube analysis...'
            }
        }

        stage('Package') {
            steps {
                sh 'mvn package'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying application...'
                sh 'cp target/simple-java-maven-app-1.0-SNAPSHOT.jar /tmp/'
                echo 'Application deployed successfully to /tmp/'
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
