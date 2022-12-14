pipeline {
    agent any

    stages {
        stage('Git Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/thisismikem/myapp.git'
            }
        }
        stage('UNIT Testing') {
            steps {
                sh 'mvn test'
            }
        }
        stage('Integration Testing') {
	        steps {
	            sh 'mvn verify -DskipUnitTests'
            }
        }
        stage('Maven Build') {
	        steps {
	            sh 'mvn clean install'
            }
        }
        stage('SonarQube analysis') {
	        steps {
	        	script {
		        	withSonarQubeEnv(credentialsId: 'sonar-api') {
		            	sh 'mvn clean package sonar:sonar'
		            }
	        	}
            }
        }
        stage('Quality Gate status') {
	        steps {
	        	script {
		        	waitForQualityGate abortPipeline: false, credentialsId: 'sonar-api'
	        	}
            }
        }
    }
}