pipeline {
    agent any
    stages {
        stage('checkout') {
            steps {
                checkout scm
            }
        }   
         stage('init') {
            steps {
                sh "terraform init"
            }
        }
        stage('plan') {
            steps {
                sh "terraform plan"
            }
        }
        stage('action') {
            steps {
                echo "Terraform action is --> ${action}"
                sh "terraform ${action} -auto-approve"
            }
        }
    }
}
