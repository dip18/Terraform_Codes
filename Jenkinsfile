pipeline {
    environment {
      gitCredentialId = 'Jenkins-Git'
      gitUrl = 'https://github.com/dip18/Terraform_Codes.git'
      deployBranch = 'phase1'
    }
    agent {
      node {
        label "master"
      }
    }

    stages {
      stage('Latest_Code') {
        steps {
            git(
              url: gitUrl,
              credentialsId: gitCredentialId,
              branch: deployBranch
            )
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