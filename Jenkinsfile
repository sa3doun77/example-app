node {
        def app

        stage('Clone repository') {
                checkout scm
        }

        stage('Build image') {
                app = docker.build('mjuuso/example-app')
        }

        stage('Test') {
                app.inside {
                        sh 'npm test'
                }
        }

        stage('Push image') {
                docker.withRegistry('https://registry.hub.docker.com', 'docker-hub-credentials') {

                        /* We'll push the image with two tags:
                 * First, the branch name and the latest tag
                 * Second, the branch name and the incremental build number
                 * Pushing multiple tags is cheap, as all the layers are reused. */

                        app.push("${env.BRANCH_NAME}-latest")
                        app.push("${env.BRANCH_NAME}-${env.BUILD_NUMBER}")
                }
        }
}
