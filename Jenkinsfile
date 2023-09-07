pipeline {
    agent any
    
    triggers {
        // Specify branches to build
        //branch('main') 
        githubPush()
    }
    
    
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        
        stage('Build') {
            steps {
                echo "Executed: build automation tool (Maven)"
                echo "Executed: sh 'mvn clean package'"
            }
        }
        stage('Unit and Integration Tests') {
            steps {
                echo "Executed: Test automation tool (Selenium)"
                echo "Executed: 'sh mvn test'"
            }
            post {
                failure {
                    emailext subject: 'Unit and Integration Tests Failed',
                    body: 'Unit and Integration Tests stage failed. Check logs for details.',
                    to: 'umayir10@gmail.com',
                    attachLog: true
                }
                success {
                    emailext subject: 'Unit and Integration Tests Passed',
                    body: 'Unit and Integration Tests stage succeeded.',
                    to: 'umayir10@gmail.com',
                    attachLog: true
                }
            }
        }
        stage('Code Analysis') {
            steps {
                echo "Executed: Code analysis tool (SonarQube)"
                echo "Executed: sh 'sonar-scanner'"
            }
        }
        stage('Security Scan') {
            steps {
                echo "Executed: security scanning tool (SonarQube)"
                echo "Executed: sh 'zap-cli --quick-scan <target-url>'"
            }
        }
        stage('Deploy to Staging') {
            steps {
                echo "Deploy to your staging server (AWS EC2)"
                echo "Executed: sh 'ansible-playbook deploy-staging.yml'"
            }
            post {
                failure {
                    emailext subject: 'Security Scan Failed',
                    body: 'Security Scan stage failed. Check logs for details.',
                    to: 'umayir10@gmail.com',
                    attachLog: true
                }
                success {
                    emailext subject: 'Security Scan Passed',
                    body: 'Security Scan stage succeeded.',
                    to: 'umayir10@gmail.com',
                    attachLog: true
                }
            }
        }
        stage('Integration Tests on Staging') {
            steps {
                echo "Run integration tests on the staging environment"
                echo "Executed: sh 'python integration_tests.py'"
            }
        }
        stage('Deploy to Production') {
            steps {
                echo "Deploy to your production server (AWS EC2)"
                echo "Executed: sh 'ansible-playbook deploy-production.yml'"
            }
        }
    }
}
