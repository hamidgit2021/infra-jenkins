pipeline {
    agent any
   
    environment {
        AWS_ACCESS_KEY_ID = credentials('hamid_AWS_ACCESS_KEY_ID')
        AWS_SECRET_ACCESS_KEY = credentials('hamid_AWS_SECRET_ACCESS_KEY')
        AWS_DEFAULT_REGION = "us-east-1"
    }
    stages {
        stage('Checkout') {
            steps {
           git branch: 'main', url: 'https://github.com/hamidgit2021/infra-jenkins.git'
  
            }
        }
    
        stage ("terraform init") {
            steps {
                sh "terraform init" 
            }
        }
  
        stage ("plan") {
            steps {
                sh "terraform plan" 
            }
        }
        stage ("Action") {
            steps {
                sh 'terraform ${action} --auto-approve'  
           }
        }
        stage("Deploy to EKS") {
            // when {
            //   expression { params.apply }
            // }
            steps {
                   sh "aws eks update-kubeconfig --name eks_cluster"
                   // sh "kubectl apply -f deployment.yml"   # we commented this now cause we need resource for other project
                   sh "kubectl delete -f deployment.yml"     // we delete this deployment
             }
        }
    }
}
   
    
