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
           withCredentials([azureServicePrincipal(credentialsId: 'azurelogin',
                                                       subscriptionIdVariable: '8df92471-3d44-4acb-b904-9bc3eb1ae550',
                                                       clientIdVariable: 'b7568031-a099-4eff-9702-d2dddcdc060c',
                                                       clientSecretVariable: '-cifAqfeoPCCcV0eQiu=.bCjQWx]k862',
                                                       tenantIdVariable: '806d602b-a09f-4d9a-a655-a426119acbb9')]) {
                                                            sh 'terraform init'
                                                            sh 'terraform plan -out "check.out"'
                  }   
            }      
         }
      } 
   }
