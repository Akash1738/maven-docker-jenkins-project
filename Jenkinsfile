pipeline {
 agent any

 stages {

  stage('Clone Code') {
   steps {
    git 'https://github.com/Akash1738/maven-docker-jenkins-project.git'
   }
  }

  stage('Build Maven Project') {
   steps {
    sh 'mvn clean package'
   }
  }

  stage('Build Docker Image') {
   steps {
    sh 'docker build -t maven-app .'
   }
  }

  stage('Terraform Infrastructure') {
   steps {
    dir('terraform') {
     sh 'terraform init'
     sh 'terraform apply -auto-approve'
    }
   }
  }

  stage('Configure Server using Ansible') {
   steps {
    dir('ansible') {
     sh 'ansible-playbook -i inventory install-docker-java.yml'
    }
   }
  }

  stage('Deploy Docker Container') {
   steps {
    dir('ansible') {
     sh 'ansible-playbook -i inventory deploy-app.yml'
    }
   }
  }

 }
}
