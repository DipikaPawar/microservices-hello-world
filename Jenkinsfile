pipeline {
    agent any

    environment {
        GITHUB_CREDENTIALS = credentials('github-pat')  // Replace with your credential ID
    }

    stages {
        stage('Checkout') {
            steps {
                // Clone the GitHub repository
                git branch: 'master', 
                    url: 'https://github.com/DipikaPawar/microservices-hello-world.git',
                    credentialsId: 'github-pat'
            }
        }

        stage('Build') {
            steps {
                // Run Maven build (if using Maven)
                echo 'Building the application...'
                cd helloworld_service
                sh 'mvn clean install'
            }
        }

        stage('Test') {
            steps {
                // Run tests (assumes the project has test cases)
                echo 'Running tests...'
                sh 'mvn test'
            }
        }

        stage('Package') {
            steps {
                // Package the application (if needed)
                echo 'Packaging the application...'
                sh 'mvn package'
            }
        }

        stage('Deploy') {
            when {
                branch 'master' // Only deploy when on the main branch
            }
            steps {
                // Deployment logic - this can be customized based on your environment.
                echo 'Deploying the application...'
                // Example: SCP files to server or push Docker image
            }
        }
    }

    post {
        always {
            // Always clean up after build
            echo 'Cleaning up workspace...'
            deleteDir()
        }
        success {
            echo 'Build succeeded!'
        }
        failure {
            echo 'Build failed!'
        }
    }
}
