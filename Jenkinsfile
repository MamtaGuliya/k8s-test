node {
    def app

    stage('Clone repository') {
      

        checkout scm
    }

    stage('Update GIT') {
            script {
                catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                    withCredentials([usernamePassword(credentialsId: 'github_token', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
                        //def encodedPassword = URLEncoder.encode("$GIT_PASSWORD",'UTF-8')
                        sh "git config user.email mamta.guliya@onecom.co.uk"
                        sh "git config user.name MamtaGuliya"
                        //sh "git switch master"
                        sh "cat deployment.yaml"
                        sh "sed -i 's+${REGISTRY_NAME}/${IMAGE_NAME}:.*+${REGISTRY_NAME}/${IMAGE_NAME}:${IMAGE_TAG}+g' deployment.yaml"                        sh "cat deployment.yaml"
                        sh "git add ."
                        sh "git commit -m 'Done by Jenkins Job changemanifest: ${env.BUILD_ID}'"
                        sh "git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/k8s-test.git HEAD:main"
      }
    }
  }
}
}
