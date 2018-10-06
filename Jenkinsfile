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
            steps {                
              when {
               branch 'master'
                   }
               steps{
                withcredentials([Usernamepassword(credentialsId: 'webserverlogin',usernamevariable:'USERNAME',passwordvariable:'PASSWORD')]){
                    sshPublisher(publishers: [sshPublisherDesc(configName: 'stage',sshcredentials: [usernname:"$USERNAME", encryptedpassword:"$PASSWORD"] ,transfers: [sshTransfer(excludes: '', execCommand: 'sudo /usr/bin/systemctl stop train-schedule && rm -rf /opt/train-schedule/* && unzip /tmp/trainSchedule.zip -d /opt/train-schedule && sudo /usr/bin/systemctl stop train-schedule', execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '/tmp', remoteDirectorySDF: false, removePrefix: 'dist/', sourceFiles: 'dist/trainSchedule.zip')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: true)])
                }
               }
            }
    }

