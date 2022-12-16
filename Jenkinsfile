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
		stage ('Upload to Artifactory') {
			steps {
				sh 'jfrog rt upload --url http://20.235.82.247:8080/job/artifactory/ --access-token ${ARTIFACTORY_ACCESS_TOKEN} target/my-app-1.0-SNAPSHOT.jar java-maven-app'
			}
		}
		stage('Deploy') {
			steps {
				archiveArtifacts '**/target/*.jar'
			}
			
		}
		
	}
}
