node {
	stage('cleanup') {
		cleanWs();
	}
	checkout scm
	/*
	dir('services/ui/angular') {
		stage ('Dependencies') {
			docker.image('node:14.16').inside {
				sh 'npm ci --quiet --cache="./npm"'
			}
		}
		stage('Build') {
			docker.image('node:14.16').inside {
				sh 'npm run build.production --cache="./npm"'
			}
		}
		stage('lint') {
		try {
			echo 'linting'
		}	catch(Exception e) {
			echo 'Failed linting ' + e.toString();
			}
		}
		stage('test') {
			docker.image('buildkite/puppeteer:8.0.0').inside {
				sh 'npm run test --cache="./npm"'
			}
		}
		*/
		stage('delivery') {
			if(env.BRANCH_NAME == 'master') {
				docker.withRegistry('', 'DockerHub'){
					def myImage = docker.build("iceboi714/ui:${env.BUILD_ID}")
					myImage.push()
					myImage.push('latest')
				}
			}
		}
	//}
}