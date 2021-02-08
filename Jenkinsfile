pipeline {
   agent any

   stages {
      stage('Installation') {
        steps {
          sh '''
          echo 'Installing required packages'
          echo "Running ${env.BUILD_ID} ${env.BUILD_DISPLAY_NAME} on ${env.NODE_NAME} and JOB ${env.JOB_NAME}"
          sudo apt-get install wget unzip -y
          wget  https://releases.hashicorp.com/terraform/0.13.5/terraform_0.13.5_linux_amd64.zip
          unzip "terraform_0.13.5_linux_amd64.zip"
          mv terraform /usr/local/bin
          echo "Installation Completed"
          '''
        }
   }
      
  stage ('Verification') {
         steps {
            sh '''
            terraform version
            '''
         }
   }    
   stage('Initialization') {
     steps {
        sh '''
        echo 'Initializing Terraform....'
        cd terraform/
        terraform init
        '''
     }
   }
   stage('Planning') {
     steps {
       sh '''
       echo 'Planning Terraform Code...'
       pwd
       terraform plan
       '''
     }
   }
      stage('Deploying') {
     steps {
       sh '''
       echo 'Applying Terraform Code...'
       pwd
       terrform apply
       '''
     }
   }
  }
}
