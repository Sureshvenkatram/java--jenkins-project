pipeline {
    agent any
    tools {
       maven 'maven8'
    }
    stages {
        stage("git clone"){
            steps{
                git 'https://github.com/Abbas811/java--jenkins-project_sonar.git'
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
                sh "docker build -t sureshcld28/suresh007:1.5 ."

            }

        }
        stage("Docker push"){
            steps{
                sh "docker  push sureshcld28/suresh007:1.5"

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
  -Dsonar.projectKey=jenkins-dev \
  -Dsonar.host.url=http://18.212.250.27:9000 \
  -Dsonar.login=sqp_d6b7c19ced9213bccc50bb0bc0118bf848fe0834'
                }
        }
    }
}
