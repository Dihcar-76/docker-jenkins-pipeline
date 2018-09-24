 pipeline {//node
  //checkout scm
  //env.PATH = "${tool 'Maven3'}/bin:${env.PATH}"
  agent any
  stages{
        stage('Build') {
              steps{
                bat 'mvn clean package -DskipTests'
              }              
          }

          stage('Create Docker Image') {
            steps{
                bat'docker.build("rbougrin/docker-jenkins-pipeline:${env.BUILD_NUMBER}")'
            }
          }

          stage ('Run Application') {
           steps{
              // Start database container here
              // sh 'docker run -d --name db -p 8091-8093:8091-8093 -p 11210:11210 arungupta/oreilly-couchbase:latest'

              // Run application using Docker image
              bat "DB=`docker inspect --format='{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' db`"
              bat "docker run -e DB_URI=$DB rbougrin/docker-jenkins-pipeline:${env.BUILD_NUMBER}"

              // Run tests using Maven
              //dir ('webapp') {
              //  sh 'mvn exec:java -DskipTests'
              //}
           }
          }

          stage('Run Tests') {
            steps {
                bat "mvn test"
                bat'docker.build("rbougrin/docker-jenkins-pipeline:${env.BUILD_NUMBER}").push()'
            } 
          }
  }
  
}
