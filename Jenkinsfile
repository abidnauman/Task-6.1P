pipeline {
    agent any
    
    triggers {
        pollSCM('* * * * *') // Poll SCM every minute
    }
    
    stages {
        stage('Build') {
            steps {
                echo '''
                Stage 1: Build
                Task: Build the code using a build automation tool to compile and package your code.
                Tool: Maven
                '''
            }
        }
        stage('Unit and Integration Tests') {
            steps {
                echo '''
                Stage 2: Unit and Integration Tests
                Task: Run unit tests to ensure the code functions as expected and run integration tests to ensure the different components of the application work together as expected.
                Tools: JUnit (for Unit Tests), TestNG (for Integration Tests)
                '''
            }
        }
        stage('Code Analysis') {
            steps {
                echo '''
                Stage 3: Code Analysis
                Task: Integrate a code analysis tool to analyze the code and ensure it meets industry standards.
                Tool: SonarQube
                '''
            }
        }
        stage('Security Scan') {
            steps {
                echo '''
                Stage 4: Security Scan
                Task: Perform a security scan on the code using a tool to identify any vulnerabilities.
                Tool: OWASP Dependency-Check
                '''
            }
        }
        stage('Deploy to Staging') {
            steps {
                echo '''
                Stage 5: Deploy to Staging
                Task: Deploy the application to a staging server.
                Tool: AWS EC2 (Staging)
                '''
            }
        }
        stage('Integration Tests on Staging') {
            steps {
                echo '''
                Stage 6: Integration Tests on Staging
                Task: Run integration tests on the staging environment to ensure the application functions as expected in a production-like environment.
                Tool: Selenium
                '''
            }
        }
        stage('Deploy to Production') {
            steps {
                echo '''
                Stage 7: Deploy to Production
                Task: Deploy the application to a production server.
                Tool: AWS EC2 (Production)
                '''
            }
        }
    }
    
    post {
        always {
            script {
                def currentStage = env.STAGE_NAME
                def status = currentBuild.currentResult
                emailext(
                    to: 'qasimziak85@gmail.com',
                    subject: "${currentStage} Stage: ${status}",
                    body: "${currentStage} stage completed with status: ${status}",
                    attachmentsPattern: "*/.log"
                )
            }
        }
    }
}
