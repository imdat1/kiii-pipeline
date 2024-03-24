node {
    def app
    stage('Clone repository') {
        sh 'git checkout dev'
    }
    stage('Build image') {
        app = docker.build("imdat1/kiii-jenkins")
    }
    stage('Push image') {
        docker.withRegistry('https://registry.hub.docker.com', 'docker-hub-credentials') {
            app.push("${env.BRANCH_NAME}-${env.BUILD_NUMBER}")
            app.push("${env.BRANCH_NAME}-latest")
            // signal the orchestrator that there is a new version
        }
    }
}
