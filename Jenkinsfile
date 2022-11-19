pipeline {
	agent {
		label 'master'	
	}
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
			}
		}
		stage('Deploy') {
			steps {
				archiveArtifacts '**/target/*.jar'
			}
			post {
				success {
					mail (cc: "ravic@sproutonweb.com", to: "pradi.ravi@gmail.com", subject: "Job '${JOB_NAME}' (${BUILD_NUMBER}) is waiting for input", body: "Please go to ${BUILD_URL} and verify the build")
				}
			}
		}
		
	}
}
