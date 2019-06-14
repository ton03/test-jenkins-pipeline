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
				bat 'git config --global core.longpaths true'
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
				lock(resource: "compiler_${env.NODE_NAME}", inversePrecedence: true) {
					bat 'dir'
					bat 'yarn run test.cypress'
				}
			}
		}
	}

	post {
		always {
			junit 'results/cypress-report.xml'
		}
	}
}
