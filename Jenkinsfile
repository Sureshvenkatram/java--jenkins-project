pipeline {
    agent any
     environment {
         imageName = "sureshcld28/sureshram12"
    }
    tools {
       maven 'maven8'
    }
   
    stages {
        stage("git clone"){
            steps{
                git 'https://github.com/kajamal/java--jenkins-project.git'
            }

        }
        stage("build code"){
            steps{
                sh "mvn clean install"
            }

        }

        stage("Docker login"){
            steps{
              withCredentials([string(credentialsId: 'docker2', variable: 'docker_hub')]) {
               sh "docker login -u sureshcld28 -p ${docker_hub}"
               }
               

}
            }

        
        stage("build Docker image"){
            steps{
                sh "docker build -t sureshcld28/sureshram12 ."

            }

        }
        stage("Docker push"){
            steps{
                sh "docker  push sureshcld28/sureshram12"

            }

        }
        //  stage("Docker deployement"){
        //     steps{
        //         sh "docker run -d -p 8070:8080 sureshcld28/sureshram1:1.5"

        //     }

        // }
        stage('sonar'){
            steps{
                
         sh 'mvn clean verify sonar:sonar \
  -Dsonar.projectKey=sonardemo \
  -Dsonar.host.url=http://44.204.8.134:9000 \
  -Dsonar.login=sqp_0e31639928f2c7fc7987f81325c131352169679e'
                }
        }
       stage('Building image') {
      steps{
        script {
          dockerImage = docker.build imageName
        }
      }
       }
      
    }
}

