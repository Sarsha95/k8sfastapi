node {
    def app

    stage('Clone repository') {
        checkout scm
    }

    stage('Update GIT') {
        script {
            catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                withCredentials([usernamePassword(credentialsId: 'github', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
                    // Fetch the latest Docker tag from Docker Hub or your registry
                    def DOCKERTAG = sh(script: 'curl -sS "https://registry.hub.docker.com/v2/repositories/narsimha2580/test/tags/" | jq -r ".results[0].name"', returnStdout: true).trim()

                    sh "git config user.email chnarsimha2580@gmail.com"
                    sh "git config user.name Narsi12"
                    sh "cat deployment.yaml"
                    sh "sed -i 's+narsimha2580/test.*+narsimha2580/test:${DOCKERTAG}+g' deployment.yaml"
                    sh "cat deployment.yaml"
                    sh "git add ."
                    sh "git commit -m 'Done by Jenkins Job changemanifest: ${env.BUILD_NUMBER}'"
                    sh "git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/k8sfastapi.git HEAD:main"
                }
            }
        }
    }
}
