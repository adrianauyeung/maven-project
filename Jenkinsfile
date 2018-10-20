
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

		stage ('Deploy to Production') {
			steps{
				/* This create a confirmation button before it deploys
				Currently it is set to expire or fail after 5 days without
				a response */
				timeout(time:5, unit: 'DAYS'){
					input message: 'Approve PRODUCTION deploy?'
				}

				build job: 'jf-deploy-to-production'
			}
			post {
				success {
					echo 'Code deployed to Production'
				}

				failure {
					echo 'Deployment failed.'
				}
			}
		}
	}
}