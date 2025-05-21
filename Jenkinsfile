pipeline {
    agent { label 'jenkins-agent' }
    tools {
        jdk 'java17'
        maven 'maven3'
    }
    environment{
	    APP_NAME = "register-aa--ci"
	    RELASE   = "1.0.0"
	    DOCKER_USER = "aarizsak"
	    DOCKER_PASS = "dockerhub_pass"
	    IMAGE_NAME = "${DOCKER_USER}" + "/" + + "${APP_NAME}"
	    IMAGE_TAG = "${RELEASE}"-"${BUILD_NUMBER}"
	    
    }	
    stages {
	stage('clean ws'){
	   steps{
		   cleanWs()
	   }
	}
	stage('chexkout'){
		steps{
		    git branch: 'main', credentialsId: 'github-pass', url: 'https://github.com/aarizsak/register-app.git'
		
		}
	}
	stage('build application'){
		steps{
		  sh 'mvn clean package'
		}
	}
	stage('test application'){
		steps{
		   sh'mvn test'	
		}
	}
	stage("SonarQube Analysis"){
           steps {
	           script {
		        withSonarQubeEnv(credentialsId: 'sonar-token') { 
                        sh "mvn sonar:sonar"
		        }
	           }	
           }
      }
      stage("Quality Gate"){
           steps {
               script {
                    waitForQualityGate abortPipeline: false, credentialsId: 'sonar-token'
               }	
           }

      }    
		
		
  }    
}
	    
