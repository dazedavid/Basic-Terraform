pipeline {
   agent any
   stages {
      stage ('Checking out GIT Files') {
         steps {
            checkout scm
        }
      }
      stage ('Preparing the Environment') {
         steps {
            script {
               def tfHome = tool 'Terraform'
               def jdk = tool 'jdk8'
               env.PATH = "${tfHome}:${env.PATH}"
            }
            sh 'terraform -version'
         }
      }   
      stage ('Provisioning Infrastructure'){
         steps {
              withCredentials([azureServicePrincipal('azurelogin')]) {
                 
                      sh 'terraform init'
                      sh 'terraform plan -out "check.out"'
                      sh 'terraform apply "check.out"'
                  }   
            }      
         }
      } 
   }
