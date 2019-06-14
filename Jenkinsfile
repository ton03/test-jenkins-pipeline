pipeline {
	agent any

	tools {
		nodejs "node"
	}

	environment {
		CI = 'true'
	}

	options {
		disableConcurrentBuilds()
	}

	stages {
		stage('Prepare') {
			steps {
				bat 'SET Path=%PATH%;%AppData%\\npm;%AppData%\\npm\\node_modules;.\\node_modules'
				bat 'yarn install'
			}
		}

		stage('Build') {
			steps {
				bat 'yarn run build'
			}
		}

		stage('Test') {
			steps {
				bat 'dir'
				bat 'yarn run test.cypress'
			}
		}
	}

	post {
		always {
			junit 'results/cypress-report.xml'
		}
	}
}
