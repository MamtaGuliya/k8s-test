node {
    def REGISTRY_NAME = params.REGISTRY_NAME // Get the parameter passed from the first pipeline
    def IMAGE_TAG = params.IMAGE_TAG
    def IMAGE_NAME = params.IMAGE_NAME

    stage('Clone repository') {
        checkout scm
    }

    stage('Update GIT') {
        script {
            catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                withCredentials([usernamePassword(credentialsId: 'github_token', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
                    sh "git config user.email mamta.guliya@onecom.co.uk"
                    sh "git config user.name MamtaGuliya"
                    sh "sed -i 's+${REGISTRY_NAME}/${IMAGE_NAME}:.*+${REGISTRY_NAME}/${IMAGE_NAME}:${IMAGE_TAG}+g' deployment.yaml"
                    sh "git add ."
                    sh "git commit -m 'Done by Jenkins Job changemanifest: ${env.BUILD_ID}'"
                    sh "git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/k8s-test.git HEAD:main"
                }
            }
        }
    }
}