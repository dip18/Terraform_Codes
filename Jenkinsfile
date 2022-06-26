pipeline {
    environment {
      gitCredentialId = 'afc6f0c3-d062-43d7-a7ea-acda4daafef1'
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
          bat 'tf_init_plan.bat'
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
            bat 'tf_apply.bat'
        }
      }
    }  
  }
