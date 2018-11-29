node {
	def app
	stage('Clone Repository') {
		/* Lets make sure we have the repository cloned to our workspace */
		checkout scm
	}

	stage('Build Image') {
		/* This builds the actual image; synonymous to
		 * docker build on command line */

		app = docker.build("rspdevops/hellonode") 
	}

	stage('Test Image') {
	/* Ideally, we would run a test framework against our image.
	 * For this example, we're using a Volkswagen-type approach ;-) */

		app.inside {
			sh 'echo "Test passed"'
		}
	}

	stage('Push Image') {
		/* Finally, we'll push the image with two tags:
		 * First, the incremental build number from Jenkins
		 * Second, the 'latest' tag.
		 * Pushing multiple tags is cheap, as all the layers are reused. */

		sh 'docker login rspdevops.azurecr.io -u rspdevops -p tuFE+dQzKdx1RdIjAUk56wN3DqmBmNMf'
        sh 'docker tag hellonode rspdevops.azurecr.io/hellonode' 
        sh 'docker push rspdevops.azurecr.io/hellonode'
        sh 'docker push rspdevops.azurecr.io:${env.BUILD_NUMBER}'
	}
}
