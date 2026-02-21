pipeline {
    agent any
	
	triggers {
		pollSCM('H/2 * * * *')
	}

    stages {

        stage("Checkout") {
            steps {
                checkout scm
            }
        }

        stage("Restore Dependencies") {
            steps {
                echo 'Restoring NuGet packages...'
                bat 'dotnet restore'
            }
        }

        stage("Build") {
            steps {
                echo 'Building the application...'
                bat 'dotnet build --no-restore'
            }
        }

        stage("Test"){
            steps {
                echo 'Running Unit and Integration tests...'
                bat 'dotnet test --no-build --verbosity normal'
            }
        }
    }

    post {
        always {
            echo 'Pipeline execution finished.'
        }
        success {
            echo 'Build and Tests passed successfully!'
        }
        failure {
            echo 'Build or Tests failed. Please check the console output.'
        }
    }
}