pipeline {
	agent any

	tools {
		nodejs "node"
	}

	environment {
		CI = 'true'
	}

	options {
		ansiColor('xterm')
		disableConcurrentBuilds()
		disableResume()
		lock resource: 'build-lock'
		parallelsAlwaysFailFast()
		quietPeriod(10)
		rateLimitBuilds(throttle: [count: 60, durationName: 'hour', userBoost: true])
		timeout(time: 1, unit: 'HOURS')
		timestamps()
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
			failFast true
			parallel {
				stage('Test A') {
					steps {
						// bat 'yarn run test.cypress'
						bat 'ping localhost -n 5'
						// junit 'results/cypress-report.xml'
					}
				}
				stage('Test B') {
					steps {
						// bat 'yarn run test.cypress'
						bat 'ping localhost -n 10'
						// junit 'results/cypress-report.xml'
					}
				}
			}
		}
	}

	// post {
	// 	always {
	// 		junit 'results/cypress-report.xml'
	// 	}
	// }
}
