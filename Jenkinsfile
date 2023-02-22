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
                        sh "git config user.email ediguy@ediguy-devops.com"
                        sh "git config user.name Edi Guy"
                        //sh "git switch master"
                        sh "cat deployments/mysql-deployment.yaml "
                        sh "cat deployments/polling-app-server.yaml"
                        sh "cat deployments/polling-app-client.yaml"
                        sh "sed -i 's+devtraining/server-app.*+devtraining/polling-app-server:${DOCKERTAG}+g' deployments/polling-app-server.yaml"
                        sh "sed -i 's+devtraining/client-app.*+devtraining/polling-app-client:${DOCKERTAG}+g' deployments/polling-app-client.yaml"
                        sh "cat deployments/mysql-deployment.yaml "
                        sh "cat deployments/polling-app-server.yaml"
                        sh "cat deployments/polling-app-client.yaml"
                        sh "git add ."
                        sh "git commit -m 'Done by Jenkins Job changemanifest: ${env.BUILD_NUMBER}'"
                        sh "git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/polling-app-deployment.git HEAD:main"
      }
    }
  }
}
}
