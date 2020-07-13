/*node {
	stage('Build') {
		echo "Build"
	}
	stage('Test') {
		echo "Test"
	}
}*/
//Declarative Pipeline

Pipeline {
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
}
