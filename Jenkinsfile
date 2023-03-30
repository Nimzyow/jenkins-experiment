/* Requires the Docker Pipeline plugin */
pipeline {
    agent any
    options {
        timeout(time: 7, unit: "SECONDS")
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
    }
}