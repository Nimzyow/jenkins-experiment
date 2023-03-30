/* Requires the Docker Pipeline plugin */
pipeline {
    agent any
    options {
        timeout(time: 30, unit: "SECONDS")
    }
    stages {
        stage('build') {
            steps {
                sh 'echo "Hello World"'
                sh '''
                    echo "Multiline shell steps works too"
                    ls -lah
                '''
            }
        }
        stage('input') {
            agent any
            input {
                message "What is your first name?"
                ok "Submit"
                parameters {
                    string(defaultValue: 'Dave', name: 'FIRST_NAME', trim: true)
                }
            }
            options {
                timeout(time: 10, unit: 'SECONDS')
            }
            steps {
                echo "Good Morning, $FIRST_NAME"
                sh '''
                    hostname
                    cat /etc/redhat-release
                '''
            }
        }
        post {
            always {
                echo "This will always run"
            }
            success {
                echo "This will run only if successful"
            }
            failure {
                echo "This will run only if failed"
            }
            unstable {
                echo "This will run only if the run was marked as unstable"
            }
            changed {
                echo "This will only run if the state of the pipeline has changed"
                echo "For example. if the pipeline was previously failing but is now successful"
            }
        }
    }
}