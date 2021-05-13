def remote = [:]
remote.name = 'test'
remote.host = '18.209.87.84'
remote.port = 22
remote.allowAnyHosts = true


pipeline {
    agent any

     stages {
        stage('Git Clone') {
            steps {
                // Get some code from a GitHub repository
                git branch: 'main', credentialsId: '4af18a21-3317-4da0-85bc-1fbffb60821b', url: 'https://github.com/akashmukh/Jenkins.git'
            }
        }
     stage('Deployment'){
        steps {
            script {
             // move the new changed 
             sh '''
                echo "echo hello world" >> test.sh
                cat test.sh
             '''
             sh 'ls'
             withCredentials([usernamePassword(credentialsId: 'sayanid', passwordVariable: 'pass', usernameVariable: 'user')]) {
             remote.user = user
             remote.password = pass
             sshPut remote: remote, from: "index.html", into: "/tmp"
             sshPut remote: remote, from: "test.sh", into: "/tmp"
             sshCommand remote: remote, command: "ls /var/www/html && chmod +x /tmp/test.sh"
             sshScript remote: remote, script: 'test.sh'
             }
            }
            }
        }
    }
}
