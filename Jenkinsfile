
pipeline {
	/* A Declarative Pipeline */
	/* any just means use any available node*/
	agent any

	stages {

		stage ('Build') {
			steps {
				sh 'mvn clean package'
			}
			post {
				success {
				echo 'Now Archiving...'
				archiveArtifacts artifacts: '**/target/*.war'
				}
			}
		}
	}
}