
pipeline {
	/* A Declarative Pipeline */
	/* any just means use any available node*/
	agent any

	tools{
      maven 'localMavel'
    }

	stages {

		stage ('Build') {
			steps {
				sh 'mvn clean' 
				sh 'mvn package'
			}
			post {
				success {
				echo 'Now Archiving...'
				archiveArtifacts artifacts: '**/*.war'
				echo 'Done Archiving...'
				}
			}
		}

		stage('Deploy to Staging') {
			steps {
				echo 'Dp checkstyle'
				sh 'mvn checkstyle:checkstyle'
				/* Used to define a job to build */
				build job: 'jf-deploy-to-staging'
			}
		}
	}
}