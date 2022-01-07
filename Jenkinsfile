def semanticVersion = "${env.BUILD_NUMBER}.0.0"
def packageName = "devops_pipeline_demo_${env.BUILD_NUMBER}"
def version = "${env.BUILD_NUMBER}.0"

pipeline {
	agent any
	tools {
		maven "Maven"
	}
	stages {
		stage('build') {
			steps {
				echo 'build...'
				snDevOpsStep()
				sleep 15
			}
		}
		stage('test') {
			steps {
				echo 'test....'
				snDevOpsStep()
				snDevOpsArtifact(artifactsPayload:"""{"artifacts": [{"name": "qa_artifact.jar","version": "1.${env.BUILD_NUMBER}","semanticVersion": "1.${env.BUILD_NUMBER}.0","repositoryName": "multibranch"}],"stageName": "test"}""")
				sleep 15
				//snDevOpsChange()
			}
		}
		stage('Deploy for development') {
			when {
				branch 'development'
			}
			steps {
				echo 'dev branch deployment ...'
				snDevOpsStep()
				
				sleep 15
			}
		}
		stage('Deploy for production') {
			when {
				branch 'prod'
			}
			steps {
				echo 'prod branch deployment...'
				snDevOpsStep()
				sleep 15
			}
		}
	}
}
