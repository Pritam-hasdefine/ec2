def remote = [:]
remote.name = 'test'
remote.host = '3.216.133.85'
remote.port = 22
remote.allowAnyHosts = true


pipeline {
    agent any

     stages {
        stage('Git Clone') {
            steps {
                // Get some code from a GitHub repository
                git branch: '*/main', credentialsId: '7cc5f77a-81ae-48c8-8a34-07fc68f71414', url: 'https://github.com/Pritam-hasdefine/apache2.git'
            }
        }
     stage('Deployment'){
        steps {
            script {
             // move the new changed 
          
             withCredentials([usernamePassword(credentialsId: 'pritam-id', passwordVariable: 'pass', usernameVariable: 'user')]) {
             remote.user = user
             remote.password = pass
             sshPut remote: remote, from: "index.html", into: "/var/www/html"
            
             
             }
            }
            }
        }
    }
}
