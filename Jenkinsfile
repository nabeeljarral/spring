pipeline {
  environment {
    imagename = "nabeel636/pipe1"
    registryCredential = 'nabeel'
    dockerImage = ''
  }
  agent any
  stages {
    stage('Clone Git') {
      steps {
        git([url: 'git@github.com:nabeeljarral/spring.git', credentialsId: 'nabeel', branch: 'master'])

      }
    }
        stage('Build') {
            steps {
                sh './gradlew assemble'
            }
        }
        stage('Test') {
            steps {
                sh './gradlew test'
            }
        }
        stage('Build Docker image') {
            steps {
                sh './gradlew build'
                }
        }
        stage('Push Docker image') {
            environment {
                DOCKER_HUB_LOGIN = credentials('hub')
          }  
          
        steps {
                sh 'docker login --username=$DOCKER_HUB_LOGIN_USR --password=$DOCKER_HUB_LOGIN_PSW'
                sh './gradlew dockerPush nabeel636/pipe1:25'
            }  
    }
  }
} 
