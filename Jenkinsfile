pipeline {
	agent {
		docker {
			image 'node:10-alpine'
			args '-p 3200:3200' 
		}
	}
	environment {
		CI = 'true'
	}
	stages {
		stage("Build") {
			steps {
				sh 'npm install'
			}
		}
		stage("Test") {
			steps {
				sh './scripts/test.sh'
			}
		}
		stage("Deliver") {
			steps {
				sh './jenkins/scripts/deliver.sh'
				input message: 'Finished using the web site? (Click "Proceed" to continue)'
				sh './jenkins/scripts/kill.sh'
			}
		}
	}
}