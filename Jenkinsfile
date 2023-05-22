node {
    def app

    stage('Clone repository') {
        /* Let's make sure we have the repository cloned to our workspace */

        checkout scm
    }

    stage('Build image') {
        /* This builds the actual image; synonymous to
         * docker build on the command line */

        app = docker.build("sa3dou77/example-app")
    }

    stage('Push image') {
        /* Finally, we'll push the image into Docker Hub */

       # withDockerRegistry([ credentialsId: "docker-hub-crendentials", url: "" ]) {
        docker.withRegistry('https://registry.hub.docker.com', 'docker-hub-crendentials') {
           app.push("${env.BUILD_NUMBER}")
            app.push("latest")
        }
    }
}
