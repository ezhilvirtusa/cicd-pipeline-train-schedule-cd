
pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo 'Running build automation'
                sh './gradlew build --no-daemon -debug'
                archiveArtifacts artifacts: 'dist/trainSchedule.zip'
            }
        }
        stage('Deploy stage'){
                      
              when {
               branch 'master'
                   }
               steps{
                withCredentials([usernamePassword(credentialsId: 'webserverlogin',usernameVariable:'USERNAME',passwordVariable:'PASSWORD')]){
                    sshPublisher(
                        publishers: [
                          sshPublisherDesc(
                              configName: 'stage',
                              sshcredentials: [
                               usernname:"$USERNAME", 
                               encryptedPassphrase:"$PASSWORD"
                              ],
                              transfers: [
                                  sshTransfer(
                                      sourcefiles:'dist/trainSchedule.zip',
                                      removePrefix:'dist/',
                                      remoteDirectory:'/tmp',
                                      execCommand: 'sudo /usr/bin/systemctl stop train-schedule && rm -rf /opt/train-schedule/* && unzip /tmp/trainSchedule.zip -d /opt/train-schedule && sudo /usr/bin/systemctl stop train-schedule'
									)
									]
									)
									]
									)
									}
									}
									
									}
									}
									}
										
