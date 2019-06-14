stage 'Prepare'
node {
	bat 'npm install -g yarn'
	bat 'yarn install'
}

stage 'Test'
node {
	bat 'dir'
	bat 'yarn test.cypress'
}
