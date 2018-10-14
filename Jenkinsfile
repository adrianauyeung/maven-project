
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
				sh 'mvn clean package'
			}
			post {
				success {
				echo 'Now Archiving...'
				archiveArtifacts artifacts: '**/*.war'
				}
			}
		}

		stage('Deploy to Staging') {
			steps {
				/* Used to define a job to build */
				build job: 'jf-deploy-to-staging'
			}
		}
	}
}