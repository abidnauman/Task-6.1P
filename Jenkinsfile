pipeline {
    agent any

    parameters {
        string(name: 'emailRecipient', defaultValue: 'abidnauman0@gmail.com', description: 'Email address to receive notifications.')
        booleanParam(name: 'attachLog', defaultValue: true, description: 'If true, the build log will be attached to the email notifications.')
    }

    triggers {
        pollSCM('* * * * *') // Polls the Source Code Management (SCM) system every minute for changes.
    }

    stages {
        stage('Build') {
            steps {
                echo 'Building the application using Maven to compile the source code and package it into an executable form.'
            }
        }
        stage('Unit and Integration Tests') {
            steps {
                echo 'Running unit tests with JUnit to validate individual components and integration tests with TestNG to ensure system-wide coordination and functionality.'
            }
        }
        stage('Code Analysis') {
            steps {
                echo 'Analyzing the source code with SonarQube to detect potential quality issues and ensure compliance with coding standards.'
            }
        }
        stage('Security Scan') {
            steps {
                echo 'Conducting a comprehensive security scan with OWASP ZAP to identify and report any security vulnerabilities in the code.'
            }
            post {
                success {
                    emailext(
                        subject: 'Security Scan Completed: No Vulnerabilities Detected',
                        body: 'The security scan has been completed successfully with no vulnerabilities found. Your code has passed the security checks and is ready for the next steps in the deployment process.',
                        to: "${params.emailRecipient}",
                        attachLog: "${params.attachLog}"
                    )
                }
                failure {
                    emailext(
                        subject: 'Security Scan Alert: Vulnerabilities Detected',
                        body: 'The security scan has detected vulnerabilities in your code. Please review the attached log for detailed information and address these issues promptly to ensure the security of your application.',
                        to: "${params.emailRecipient}",
                        attachLog: "${params.attachLog}"
                    )
                }
            }
        }
        stage('Deploy to Staging') {
            steps {
                echo 'Deploying the application to a staging environment on AWS EC2 to test the real-world functionality under controlled conditions.'
            }
        }
        stage('Integration Tests on Staging') {
            steps {
                echo 'Executing integration tests in the staging environment to ensure the application operates seamlessly and meets performance benchmarks.'
            }
            post {
                always {
                    emailext(
                        subject: 'Staging Integration Tests Completed',
                        body: 'All integration tests on the staging environment have been completed successfully. The application is now ready for final deployment to production.',
                        to: "${params.emailRecipient}",
                        attachLog: "${params.attachLog}"
                    )
                }
            }
        }
        stage('Deploy to Production') {
            steps {
                echo 'Deploying the application to the production server to make it available for end-user access.'
            }
        }
    }
}
