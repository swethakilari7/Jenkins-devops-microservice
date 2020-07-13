/*node {
	stage('Build') {
		echo "Build"
	}
	stage('Test') {
		echo "Test"
	}
}*/
//Declarative Pipeline

pipeline {
	//agent { docker { image 'maven:3.6.3'} }
	agent any
	environment {
		dockerHome = tool 'MyDocker'
		mavenHome = tool 'myMaven'  //Get this information from Global tool configuration...
		PATH  = "$dockerHome/bin:$mavenHome/bin:$PATH"
	}
	stages{
		stage('checkout') {
			steps {
					
				sh 'mvn --version'
				sh 'docker version'
				echo "Build"
				echo "PATH - $PATH"
				echo "BUILD NUMBER - $env.BUILD_NUMBER"
				echo "BUILD_ID - $env.BUILD_NUMBER"
				echo "JOB_NAME - $env.JOB_NAME"
				echo "BUILD_TAG - $env.BUILD_TAG"
				echo "BUILD_URL - $env.BUILD_URL"
			}
		}
		stage('Compile') {
			steps {
				sh "mvn clean compile"
			}
		stage('Test') {
			steps {
				sh "mvn test"
				echo "Test"
			}
		}
		stage('Integration Test') {
			steps {
				sh "mvn failsafe:integration-test failsafe:verify"
			}
		}
		stage('package') {
			steps {
				sh "mvn package -DskipTests"
			}
		}
		
		stage ('Build Docker Image') {
			steps {
				//"docker build -t swethak071/currency-exchange-devops:$env.BUILD_TAG"
				script {
					docker.build("swethak071/currency-exchange-devops:${env.BUILD_TAG}")
				}
			}
		}
		stage ('Push Docker Image') {
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
	post {
		always {
			echo "I am awesome, I run always"
		}
		success {
			echo "I run when you are success"
		}
		failure {
			echo "I run when build is failed"
		}
		aborted {
			echo "I run when build is aborted"
		}
		
	}
}
