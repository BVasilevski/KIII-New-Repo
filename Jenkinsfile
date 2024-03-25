node {
    def app
    stage('Clone repository') {
        checkout scm
    }
    stage('Build image') {
        def repositoryName = "BVasilevski/kiii-new-repo".toLowerCase()
        app = docker.build(repositoryName)
    }
    stage('Push image') {   
        docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
            app.push("${env.BRANCH_NAME}-${env.BUILD_NUMBER}")
            app.push("${env.BRANCH_NAME}-latest")
            // signal the orchestrator that there is a new version
        }
    }
}
