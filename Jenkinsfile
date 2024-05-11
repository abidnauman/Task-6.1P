pipeline {
    agent any

    parameters {
        string(name: 'emailRecipient', defaultValue: 'qasimziak85@gmail.com', description: 'Email address to receive notifications')
        booleanParam(name: 'attachLog', defaultValue: true, description: 'Attach build log to email')
    }

    triggers {
        pollSCM('* * * * *')
    }

    stages {
        stage('Build') {
            steps {
                echo 'Build the code using a build automation tool to compile and package your code. You need to specify at least one build automation tool e.g., Maven.  '
            }
        }
        stage('Unit and Integration Tests') {
            steps {
                echo 'run unit tests to ensure the code functions as expected and run integration tests to ensure the different components of the application work together as expected. You need to specify test automation tools for this stage.'

            }
        }
        stage('Code Analysis') {
            steps {
                echo ' integrate a code analysis tool to analyse the code and ensure it meets industry standards. Research and select a tool to analyse your code using Jenkins. '
            }
        }
        stage('Security Scan') {
            steps {
                echo 'perform a security scan on the code using a tool to identify any vulnerabilities. Research and select a tool to scan your code. '
            }
            post {
                success {
                    emailext(
                        subject: 'Security Scan - No Vulnerabilities Found!',
                        body: 'Security scan completed successfully - No vulnerabilities detected!',
                        to: "${params.emailRecipient}",
                        attachLog: "${params.attachLog}"
                    )
                }
                failure {
                    emailext(
                        subject: 'Security Scan - Vulnerabilities Found!',
                        body: 'Security scan detected vulnerabilities! Address them before deployment.',
                        to: "${params.emailRecipient}",
                        attachLog: "${params.attachLog}"
                    )
                }
            }
        }
        stage('Deploy to Staging') {
            steps {
                echo ' deploy the application to a staging server (e.g., AWS EC2 instance). '
            }
        }
        stage('Integration Tests on Staging') {
            steps {
                echo 'run integration tests on the staging environment to ensure the application functions as expected in a production-like environment. '
            }
            post {
                always {
                    emailext(
                        subject: 'Integration Tests on Staging - Complete!',
                        body: 'Integration tests on Staging environment completed!',
                        to: "${params.emailRecipient}",
                        attachLog: "${params.attachLog}"
                    )
                }
            }
        }
        stage('Deploy to Production') {
            steps {
                echo 'deploy the application to a production server (e.g., AWS EC2 instance).'
            }
        }
    }
}
