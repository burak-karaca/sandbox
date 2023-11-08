pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                // Checkout code from the GitHub repository
                git 'https://github.com/burak-karaca/sandbox.git'
            }
        }
        stage('Choose Test Files') {
            steps {
                script {
                    // Fetch the list of test files dynamically from the var folder
                    def testFiles = sh(script: 'ls var', returnStdout: true).trim().split('\n')
                    // Display the fetched test files as choices for the user
                    dynamicChoice = testFiles.collect { it -> it }
                }
            }
        }
        stage('Run Tests') {
            input {
                // Define a parameter to choose the test files dynamically
                message "Select the test files to run"
                parameters {
                    // Add a parameterized build to select test files dynamically
                    choice(name: 'TEST_FILE', choices: dynamicChoice.join('\n'), description: 'Choose the test file to run')
                }
            }
            steps {
                // Run the selected test files
                sh "cat ${TEST_FILE}"
            }
        }
    }
}
