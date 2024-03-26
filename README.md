--Give t2.medium instance iam permissions of s3bucket and ec2instance full access for this to work!!


--Goto terraformpractice repo
--Goto day2instance_bucket

--we can apply the terraform in this directory in jenkins by typing in the pipeline script

pipeline {
    agent any
    stages {
        stage('checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/sagari-a/terraformpractice.git'
            }
        }
         stage('init') {
            steps {
                dir('day2instance_bucket'){
                sh "terraform init"
                }
            }
        }
        stage('plan') {
            steps {
                dir('day2instance_bucket'){
                sh "terraform plan"
                }
                    
            }
        }
        stage('action') {
            steps {
                dir('day2instance_bucket'){
                echo "Terraform action is --> ${action}"
                sh "terraform ${action} -auto-approve"
                }
            }    
        }
    }
}


--Now for the groovy script

node {
    stage('checkout') { 
        git branch: 'main', url: 'https://github.com/sagari-a/terraformpractice.git'
    }
    stage('init') {
        dir('day2instance_bucket'){
        sh "terraform init"
       }
    }
    stage('action') {
        dir('day2instance_bucket'){
        echo "Terraform action is --> ${action}"
        sh "terraform ${action} -auto-approve"
       }
    }
}


--To apply Jenkins SCM pipeline in 'day2instance_bucket' FOLDER in 'terraformpractice' REPO
--We go to 'terraformpractice' REPO and go to 'day2instance_bucket' FOLDER and have created the 2 files :

1)jenkins_pipeline_scm
2)jenkins_groovy_scm


