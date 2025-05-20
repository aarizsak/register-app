pipeline {
    agent { label 'Jenkins-Agent' }
    tools {
        jdk 'Java17'
        maven 'Maven3'
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
		
		
  }    
}
	    
