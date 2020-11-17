//DECLARATIVE PIPELINE
pipeline {
	agent any // It is similar to node. Will be running the agent inside a docker image
	// agent { 
	//	docker { 
	//		image 'maven:3.6.3'
	//		} 
	//	}
	environment {
		dockerHome = tool 'myDocker'
		mavenHome = tool 'myMaven'
		PATH = "$dockerHome/bin:$mavenHome/bin:$PATH"
	}
	stages {
//		stage ('Build') {
//			steps {
//				sh "mvn --version"
//				sh "docker --version"
//				echo "Build"
//				echo "PATH - $PATH"
//				echo "BUILD_NUMBER - $env.BUILD_NUMBER"
//				echo "BUILD_ID - $env.BUILD_ID"
//				echo "BRANCH_NAME - $env.BRANCH_NAME"
//				echo "JOB_NAME - $env.JOB_NAME"
//				echo "BUILD_TAG - $env.BUILD_TAG"
//				echo "BUILD_URL - $env.BUILD_URL"
//			}
//		}
		stage ('Checkout') {
			steps {
				sh "mvn --version"
				sh "docker --version"
				echo "Build"
				echo "PATH - $PATH"
				echo "BUILD_NUMBER - $env.BUILD_NUMBER"
				echo "BUILD_ID - $env.BUILD_ID"
				echo "BRANCH_NAME - $env.BRANCH_NAME"
				echo "JOB_NAME - $env.JOB_NAME"
				echo "BUILD_TAG - $env.BUILD_TAG"
				echo "BUILD_URL - $env.BUILD_URL"
			}
		}
		stage ('Compile') {
			steps {
				sh "mvn clean compile" //It downloads all the dependencies and compile the java code
			}
		}
		stage ('Test') {
			steps {
				// echo "Test"
				sh "mvn test"
			}
		}
		stage ('Integration Test') {
			steps {
				// echo "Integration Test"
				sh "mvn failsafe:integration-test failsafe:verify" // It is for running the unit tests
			}
		}
		stage ('Build Docker Image'){
			steps {
				// docker build -t arnabdocker001 / currency-exchange-devops:$env.BUILD_TAG
				script {
					dockerImage = docker.build("arnabdocker001/currency-exchange-devops:${env.BUILD_TAG}")
				}

			}
		}
		stage ('Package'){
			steps {
				sh "mvn package -DskipTests"
			}
		}
		stage ('Push Docker Image'){
			steps {
				script {
					docker.withRegistry('','dockerhub') {
					dockerImage.push();
					dockerImage.push('latest');
				}
				}
			}
			}
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

