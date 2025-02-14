pipeline {
  agent any
  stages {
    stage('SCMPullStage') {
      steps {
        git(branch: 'main', url: 'https://github.com/jenkinsrb/hellorepo1', credentialsId: '1c87d371-c0a3-4d0b-baaa-f33ccaaf8b37')
      }
    }

    stage('buildStage') {
      steps {
        sh '''sudo docker rm -f $(sudo docker ps -aq)||true
sudo docker rmi -f $(sudo docker images -aq)
sudo docker build -t jenkinsrb/eprepo1:latest .
sudo docker push jenkinsrb/eprepo1:latest
sudo docker run -d -p 7777:8080 --name con1 jenkinsrb/eprepo1:latest'''
      }
    }

    stage('Dev & QA') {
      parallel {
        stage('deployDevStage') {
          steps {
            echo 'Dev Deploy done'
          }
        }

        stage('deployQAstage') {
          steps {
            echo 'QA deploy done'
          }
        }

      }
    }

    stage('deployProdStage') {
      steps {
        echo 'Prod deploy done'
      }
    }

  }
}