node {
	checkout scm
	state('cleanup') {
		cleanWs();
	}
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
	}
}