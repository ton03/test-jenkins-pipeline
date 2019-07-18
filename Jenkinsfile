def buildNumber = env.BUILD_NUMBER as int
if (buildNumber > 1) milestone(buildNumber - 1)
milestone(buildNumber)

pipeline {
	agent any

	tools {
		nodejs "node"
	}

	environment {
		CI = 'true'
	}

	options {
		// disableConcurrentBuilds()
		disableResume()
		// lock resource: 'build-lock'
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
				stage('Test - Cypress') {
					steps {
						lock(resource: "compiler_${env.NODE_NAME}", inversePrecedence: true) {
							bat 'yarn run test.cypress'
							junit 'results/cypress-report.xml'
						}
					}
				}
				stage('Test - Ping') {
					steps {
						bat 'ping localhost -n 60'
					}
				}
			}
		}
	}
}
