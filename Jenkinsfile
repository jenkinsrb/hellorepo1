pipeline {
  agent any
  stages {
    stage('SCMPullStage') {
      agent {
        node {
          label 'linuxnode'
        }

      }
      steps {
        git(branch: 'main', url: 'https://github.com/jenkinsrb/hellorepo1', credentialsId: '1c87d371-c0a3-4d0b-baaa-f33ccaaf8b37')
      }
    }

    stage('buildStage') {
      agent any
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
          agent {
            node {
              label 'linuxnode'
            }

          }
          steps {
            echo 'Dev Deploy done'
          }
        }

        stage('deployQAstage') {
          agent any
          steps {
            echo 'QA deploy done'
          }
        }

      }
    }

    stage('deployProdStage') {
      agent any
      steps {
        echo 'Prod deploy done'
      }
    }

  }
}