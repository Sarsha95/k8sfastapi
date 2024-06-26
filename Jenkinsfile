node {
    def app
    environment {
        DOCKERTAG = 'latest'
    }

    stage('Clone repository') {
      

        checkout scm
    }

    stage('Update GIT') {
            script {
                catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                    withCredentials([usernamePassword(credentialsId: 'github', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
                        //def encodedPassword = URLEncoder.encode("$GIT_PASSWORD",'UTF-8')
                        sh "git config user.email tharayilsarsha1@gmail.com"
                        sh "git config user.name Sarsha95"
                        //sh "git switch master"
                        sh "cat deployment.yaml"
                        def DOCKERTAG = env.DOCKERTAG
                        sh "sed -i 's+sarsha1995/jenkinspipe.*+sarsha1995/jenkinspipe:${DOCKERTAG}+g' deployment.yaml"
                        sh "cat deployment.yaml"
                        sh "git add ."
                        sh "git commit -m 'Done by Jenkins Job changemanifest: ${env.BUILD_NUMBER}'"
                        sh "git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/k8sfastapi.git HEAD:main"
      }
    }
  }
}
}



