pipeline {
    agent {
      node {
        label "master"
      }
    }

    stages {
      stage('Latest_Code') {
        steps {
            script{
                sh "git clone https://dip18:dip_github@2017@github.com/Terraform_Codes.git ."
                sh "git branch -a"
                sh "git checkout phase1"
            }
        }
      }

      stage('TF Init&Plan') {
        steps {
          sh 'terraform init'
          sh 'terraform plan'
        }
      }

      stage('Approval') {
        steps {
          script {
            def userInput = input(id: 'confirm', message: 'Apply Terraform?', parameters: [ [$class: 'BooleanParameterDefinition', defaultValue: false, description: 'Apply terraform', name: 'confirm'] ])
          }
        }
      }

      stage('TF Apply') {
        steps {
          sh 'terraform apply -input=false'
        }
      }
    }
  }