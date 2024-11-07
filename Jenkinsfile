pipeline {
  agent any
  stages {
    stage('SCM') {
      steps {
        git(credentialsId: '33905e1c-dda2-4bf2-8d9c-d6830a9b1fb0', branch: 'main', url: 'https://github.com/devops646/gitrepo2')
      }
    }

    stage('Build&Publish') {
      steps {
        sh '''sudo docker build -t devops646/srepo1:latest .
sudo docker push devops646/srepo1:latest'''
      }
    }

    stage('Deploy') {
      parallel {
        stage('DeployDev') {
          steps {
            sh '''sudo docker rm -f $(sudo docker ps -aq)||true
sudo docker run -d -p 7777:80 --name devcon1 devops646/srepo1:latest'''
          }
        }

        stage('DeploQA') {
          steps {
            sh '''sudo docker rm -f $(sudo docker ps -aq)||true
sudo docker run -d -p 9999:80 --name qacon1 devops646/srepo1:latest'''
          }
        }

      }
    }

  }
}