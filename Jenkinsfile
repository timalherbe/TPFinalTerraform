properties([pipelineTriggers([githubPush()])])

pipeline {
    agent {
      docker {
        image 'hashicorp/terraform'
        args '--entrypoint='
      }
    }
    
    options {
      withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: <nom_creds>, secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']])
    }
    
    
    environment {
      AWS_REGION = "eu-west-3"
    }
    
    stages {
      stage('Init Terraform directory') {
        steps {
          sh 'terraform init'
        }
      }
      stage('Plan Terraform code') {
        steps {
          sh 'terraform plan'
        }
      }
      stage('Apply Terraform code') {
        steps {
          sh 'terraform apply -auto-approve'
        }
      }
    }
  }
        
