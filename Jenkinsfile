//DECLARATIVE PIPELINE
pipeline {
	//agent any // It is similar to node. Will be running the agent inside a docker image
	agent { image { docker 'maven:3.6.3'}}
	stages {
		stage ('Build') {
			steps {
				sh "mvn --version"
				echo "Build"
			}
		}
		stage ('Test') {
			steps {
				echo "Test"
			}
		}
		stage ('Integration Test') {
			steps {
				echo "Integration Test"
			}
		}
	} 
	post {
		always {
			echo 'I am awesome and run always'
		}
		success {
			echo 'I run when you are successful'
		}
		failure {
			echo 'I run when you fail'
		}
	}

}

