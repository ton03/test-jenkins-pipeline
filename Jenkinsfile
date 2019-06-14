pipeline {
	agent any

	tools {
		nodejs "node"
	}

	environment {
		CI = 'true'
	}

	stages {
		stage('Prepare') {
			steps {
				bat 'SET Path=%PATH%;%AppData%\\npm;%AppData%\\npm\\node_modules;.\\node_modules'
				bat 'npm i'
			}
		}

		stage('Build') {
			steps {
				bat 'npm build'
			}
		}

		stage('Test') {
			steps {
				bat 'dir'
				bat 'npm run test.cypress'
			}
		}
	}

	post {
		always {
			junit 'results/cypress-report.xml'
		}
	}
}
