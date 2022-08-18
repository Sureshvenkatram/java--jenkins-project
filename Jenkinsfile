pipeline {
    agent any
    tools {
       maven 'maven8'
    }
    environment {
         imageName = "sureshcld28/sureshram12"
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
               withCredentials([string(credentialsId: 'docker', variable: 'docker_hub_password')]) {
                   sh "docker login -u sureshcld28 -p ${docker_hub_Password}"

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
  -Dsonar.projectKey=sonarqube \
  -Dsonar.host.url=http://3.86.255.94:9000 \
  -Dsonar.login=sqp_0100c6bbf3959df53d78fde5832480f184c101fc'
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
