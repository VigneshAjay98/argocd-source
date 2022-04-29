node {
    def app

    stage('Clone repository') {
        checkout scm
    }

    stage('Update GIT') {
            script {
                catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                    withCredentials([usernamePassword(credentialsId: 'github', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
                        //def encodedPassword = URLEncoder.encode("$GIT_PASSWORD",'UTF-8')
                        sh "git config user.email vigneshajay.va@gmail.com"
                        sh "git config user.name VigneshAjay98"
                        //sh "git switch dev"
                        sh "cat simple-html.yaml"
                        sh "sed -i 's+vigneshajay98/simple-html.*+vigneshajay98/simple-html:${DOCKERTAG}+g' simple-html.yaml"
                        sh "cat simple-html.yaml"
                        sh "git add ."
                        sh "git commit -m 'Done by Jenkins Job changemanifest: ${env.BUILD_NUMBER}'"
                        sh "git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/argocd-source.git HEAD:deploy"
                    }
                }
            }
    }
}
