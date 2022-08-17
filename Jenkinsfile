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
    }
}
