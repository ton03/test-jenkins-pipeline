pipeline {
	environment {
		CI = 'true'
	}
	stages {
		stage('Prepare') {
			bat 'SET Path=%PATH%;%AppData%\npm;%AppData%\npm\node_modules'
			bat 'npm install -g yarn'
			bat 'yarn install'
		}

		stage('Test') {
			bat 'dir'
			bat 'yarn test.cypress'
		}
	}
}
