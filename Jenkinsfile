pipeline {
    agent any
    stages {
        stage('Checkout SCM') {
            steps {
                git '/home/OneDrive/Documents/GitHub/JenkinsDependencyCheckTest'
            }
        }

        stage('OWASP Dependency-Check Vulnerabilities') {
            steps {
                script {
                    dependencyCheck additionalArguments: ''' 
                        -o './'
                        -s './'
                        -f 'ALL' 
                        --prettyPrint''', odcInstallation: 'OWASP Dependency-Check Vulnerabilities'

                    // Assuming dependency-check-report.xml is the output file from Dependency-Check
                    archiveArtifacts artifacts: 'dependency-check-report.xml', fingerprint: true
                }
            }
        }
    }   
    post {
        success {
            dependencyCheckPublisher pattern: 'dependency-check-report.xml'
        }
    }
}