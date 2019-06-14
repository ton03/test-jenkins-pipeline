pipeline {
	agent none
	environment {
		CI = 'true'
	}
	stages {
		stage('Prepare') {
			steps {
				bat 'SET Path=%PATH%;%AppData%\npm;%AppData%\npm\node_modules'
				bat 'npm install -g yarn'
				bat 'yarn install'
			}
		}

		stage('Test') {
			steps {
				bat 'dir'
				bat 'yarn test.cypress'
			}
		}
	}
}
