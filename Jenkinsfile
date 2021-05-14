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
                
                git branch: '*/main', credentialsId: 'pritam-id2', url: 'https://github.com/Pritam-hasdefine/apache2.git'
                sh 'ls -l index.html'
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
