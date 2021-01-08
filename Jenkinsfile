pipeline {
    agent any
    stages {

        stage('Clone Repo') {
          steps {
            sh 'rm -rf dockertest1'
            sh 'git clone https://github.com/jkarnam7/dockertest1.git'
            }
        }

        stage('Build Docker Image') {
          steps {
            sh 'ls -al'
            sh 'pwd'
            sh 'docker build -t jaswanthk7/pipelinetestprod:${BUILD_NUMBER} .'
            }
        }

        stage('Push Image to Docker Hub') {
          steps {
           sh    'docker push jaswanthk7/pipelinetestprod:${BUILD_NUMBER}'
           }
        }

        stage('Deploy to Docker Host') {
          steps {
            sh    'docker -H tcp://191.19.1.215:2375 stop featurewebapp1 || true'
            sh    'docker -H tcp://191.19.1.215:2375 run --rm -dit --name prodwebapp1 --hostname featurewebapp1 -p 9000:80 jaswanthk7/pipelinetestprod:${BUILD_NUMBER}'
            }
        }

        stage('Check WebApp Rechability') {
          steps {
          sh 'sleep 10s'
          sh ' curl http://191.19.1.215:9000'
          }
        }

    }
}
