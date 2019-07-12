pipeline {
	agent any

	options {
		disableConcurrentBuilds()
	}

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

	lock(resource: "compiler_${env.NODE_NAME}", inversePrecedence: true) {
		node('Test') {
			stage('Test') {
				steps {
					bat 'dir'
					bat 'yarn run test.cypress'
					junit 'results/cypress-report.xml'
				}
			}
		}
	}
}
