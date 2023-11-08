pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                // Checkout code from the GitHub repository
                git 'https://github.com/burak-karaca/sandbox'
            }
        }
        stage('Choose Test Files') {
            steps {
                script {
                    // Fetch the list of test files dynamically from the var folder
                    def testFiles = sh(script: 'ls var', returnStdout: true).trim().split('\n')
                    // Display the fetched test files as choices for the user
                    def dynamicChoice = testFiles.collect { it }
                    // Add a parameterized build to select test files dynamically
                    input message: "Select the test files to run", parameters: [choice(name: 'TEST_FILE', choices: dynamicChoice.join('\n'), description: 'Choose the test file to run')]
                }
            }
        }
        stage('Run Tests') {
            steps {
                // Run the selected test files
                sh "run_test.sh ${TEST_FILE}"
            }
        }
    }
}
