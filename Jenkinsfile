pipeline {
  //agent any
  agent {label 'jenkins-node2'}

  triggers {
    pollSCM('* * * * *')
  }

  stages {
    stage('Checkout') {
      steps {
        git branch: 'main', 
        url: 'https://github.com/eomjinyoung/source-maven-java-spring-hello-webapp.git'
      }
    }
    stage('Test Application') {
      steps {
        sh 'mvn test'
      }
    }
    stage('Build Application') {
      steps {
        sh 'mvn package -DskipTests=true'
      }
    }
    stage('Application Deploy') {
      steps {
        deploy adapters: [tomcat9(credentialsId: 'tomcat-admin', url: 'http://192.168.56.102:8080')], contextPath: null, war: 'target/hello-world.war'
      }
    }
  }
}

