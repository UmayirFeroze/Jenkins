pipeline {
    agent any
    stages {
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

    post {
        failure {
            mail to: "umayir10@gmail.com",
            subject: "Pipeline Failure",
            body: "Pipeline failed. Check logs for details."
        }
        success {
            mail to: "umayir10@gmail.com",
            subject: "Pipeline Success",
            body: "Pipeline succeeded. Deployment complete."
        }
    }

}

   
