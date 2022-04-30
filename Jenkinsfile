node {
    def app

    stage('Clone repository') {
        checkout scm
    }

    stage('Update GIT') {
            script {
                catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                   // withCredentials([usernamePassword(credentialsId: 'github', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
                    withCredentials([string(credentialsId: 'git-personal', variable: 'SECRET')]) {
                        //def encodedPassword = URLEncoder.encode("$GIT_PASSWORD",'UTF-8')
                        sh "git config user.email vigneshajay.va@gmail.com"
                        sh "git config user.name VigneshAjay98"
                        //sh "git switch dev"
                        sh "cat simple-html.yml"
                        sh "sed -i 's+vigneshajay98/simple-html.*+vigneshajay98/simple-html:${DOCKERTAG}+g' simple-html.yml"
                        sh "cat simple-html.yml"
                        sh "git add ."
                        sh "git commit -m 'Done by Jenkins Job changemanifest: ${env.BUILD_NUMBER}'"
                        sh "git push https://${SECRET}@github.com/VigneshAjay98/argocd-source.git HEAD:deploy"
                    }
                }
            }
    }
}
