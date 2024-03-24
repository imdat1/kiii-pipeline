node {
    def app
    stage('Clone repository') {
	when {
            expression {
                return env.BRANCH_NAME == 'dev'
            }
        }
        checkout dev
    }
    stage('Build image') {
       app = docker.build("imdat1/kiii-jenkins")
    }
    stage('Push image') {
	when {
            expression {
                return env.BRANCH_NAME == 'dev'
            }
        }   
        docker.withRegistry('https://registry.hub.docker.com', 'docker-hub-credentials') {
            app.push("${env.BRANCH_NAME}-${env.BUILD_NUMBER}")
            app.push("${env.BRANCH_NAME}-latest")
            // signal the orchestrator that there is a new version
        }
    }
}
