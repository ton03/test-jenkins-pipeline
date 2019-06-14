pipeline {
	agent any
	environment {
		CI = 'true'
	}
	stages {
		stage('Prepare') {
			steps {
				bat 'SET Path=%PATH%;%AppData%\\npm;%AppData%\\npm\\node_modules'
				bat 'npm install'
			}
		}

		stage('Test') {
			steps {
				bat 'dir'
				bat 'npm run test.cypress'
			}
		}
	}
}
