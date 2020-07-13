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
	agent any
	stages{
		stage('Build') {
			steps {
					echo "Build"
			}
		}
		stage('Test') {
			steps {
				echo "Test"
			}
		}
		stage('Integration Test') {
			steps {
				echo "Integration Test"
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
