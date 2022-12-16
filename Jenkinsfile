pipeline {
	agent any
	tools {
		maven 'Maven-v3.8.6'
	}
	environment {
		CI = true
		ARTIFACTORY_ACCESS_TOKEN = credentials('artifactory-access-token')
	}

	stages {
		stage('Build') {
			steps {
				sh 'mvn -B -DskipTests clean install'
			}
		}
		stage('Test') {
			steps {
				sh 'mvn test'
			}
			post {
				always {
					junit 'target/surefire-reports/*.xml'
				}
			}
		}
		stage('Deploy') {
			steps {
				archiveArtifacts '**/target/*.jar'
			}
			
		}
		
	}
}
