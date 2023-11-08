pipeline {
    agent any
    stages {
        stage('Choose Test Files') {
            steps {
                script {
                    // Fetch the list of test files dynamically from the var folder
                    def testFiles = sh(script: 'ls var', returnStdout: true).trim().split('\n')
                    // Display the fetched test files as choices for the user
                    def dynamicChoice = testFiles.collect { it }
                    // Add a parameterized build to select test files dynamically
                    def userInput = input(
                        message: "Select the test files to run",
                        parameters: [extendedChoice(name: 'TEST_FILE', multiSelectDelimiter: ',', type: 'PT_MULTI_SELECT', description: 'Choose the test files to run', value: dynamicChoice.join(','))]
                    )
                    echo "Chosen test file: ${userInput}"
                    sh "cat var/${userInput}"
                    env.envUserInput = "${userInput}"
                }
            }
        }
        stage('Print File Content') {
            steps {
                // Print the content of the selected file
                script {
                    sh "cat var/${env.envUserInput}"
                }
            }
        }
    }
}
