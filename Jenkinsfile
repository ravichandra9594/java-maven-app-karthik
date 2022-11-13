pipeline {
	agent any
	tools {
		maven 'Maven-v3.8.6'	
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
				success {
					sh 'cp /var/lib/jenkins/workspace/JAVA_MAVEN_APP/target/*.jar /home/ravichandra9594/tomcat/javaMavenApp/webapps/'
				}
			}
		}
		stage('Deliver') {
			steps {
				sh './scripts/deliver.sh'
			}
		}
	}
}
