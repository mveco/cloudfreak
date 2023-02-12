pipeline {
  agent any
    tools {
      maven 'maven3'
                 jdk 'JDK17'
    }
    stages {      
        stage('Build maven ') {
            steps { 
                    sh 'pwd'      
                    sh 'mvn  clean install package'
            }
        }
        
        stage('Copy Artifact') {
           steps { 
                   sh 'pwd'
		   sh 'cp -r target/*.jar docker'
           }
        }
         
        stage('Build docker image') {
           steps {
               script {         
                 def customImage = docker.build('cloudfreak/petclinic', "./docker")
                 docker.withRegistry('https://marijavregistry.azurecr.io', 'acr-credentials') {
                 customImage.push("${env.BUILD_NUMBER}")
                 }                     
           }
        }
	  }
    }
}
