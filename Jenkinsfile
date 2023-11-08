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
                    input message: "Select the test files to run", parameters: [choice(name: 'TEST_FILE', choices: dynamicChoice.join('\n'), description: 'Choose the test file to run')]
                    echo "${TEST_FILE}"
                }
            }
        }
        stage('Print File Content') {
            steps {
                // Print the content of the selected file
                script {
                    echo "${TEST_FILE}"
                    def fileContent = sh(script: "cat var/${TEST_FILE}", returnStdout: true).trim()
                    echo "Content of the file ${TEST_FILE}:"
                    echo "${fileContent}"
                }
            }
        }
    }
}
