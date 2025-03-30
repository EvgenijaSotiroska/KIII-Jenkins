node {
    def app
    stage('Clone repository') {
        checkout scm
    }
    
    // Check if the current branch is 'dev'
    if (env.BRANCH_NAME == 'dev') {
        stage('Build image') {
            app = docker.build("evgenijasotiroska24/kiii-jenkins")
        }
        stage('Push image') {   
            docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
                app.push("${env.BRANCH_NAME}-${env.BUILD_NUMBER}")
                app.push("${env.BRANCH_NAME}-latest")
                // signal the orchestrator that there is a new version
            }
        }
    } else {
        echo "Skipping Docker build and push because branch is not 'dev'."
    }
}
