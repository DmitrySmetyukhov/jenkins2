pipeline {
    agent any

    stages {
        stage('Install HTTP Server') {
            steps {
                script {
                    sh 'sudo apt update'
                    sh 'sudo apt install -y apache2'  
                    sh 'sudo systemctl restart apache2'  
                }
            }
        }
        stage('Check Log Files for Errors') {
            steps {
                script {
                    // Retrieve and check the log file for 4xx and 5xx errors
                    def logFilePath = '/var/log/apache2/access.log'  
                    def errors = sh(script: "grep -E ' [45][0-9]{2} ' $logFilePath", returnStatus: true)

                    if (errors == 0) {
                        echo 'No 4xx or 5xx errors found in the log file.'
                    } else {
                        echo '4xx or 5xx errors found in the log file.'
                    }
                }
            }
        }
    }

    post {
        success {
            echo 'Pipeline succeeded'
        }
        failure {
            echo 'Pipeline failed'
        }
    }
}