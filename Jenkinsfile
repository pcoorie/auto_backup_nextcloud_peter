#!groovy

ansiColor('xterm') {
  echo "TERM=${env.TERM}"
  // prints out TERM=xterm
}
pipeline {
    agent any


    stages {
        stage('Build') {
            steps {
                echo 'Building..'
            }
        }
        stage('Adding') {
            steps {
                echo 'Checking system..'
                echo "You are about to backup the data for user peter "
            }
        }
        stage('Deploy') {
            steps {
                echo 'Starting backups....'
                sshPublisher(publishers: [sshPublisherDesc(configName: 'hub', transfers: [sshTransfer(excludes: '', execCommand: "mc mirror --overwrite --exclude *Music/ /nexthub/data/peter/files/ s3-gateway/msc-data-store/next-cloud-coorie-net/peter/files/", execTimeout: 0, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '', remoteDirectorySDF: false, removePrefix: '', sourceFiles: '')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: true)])
            }
        }
    }
    post {
        always {
            echo 'Just for the record..'
            
            emailext body: "${currentBuild.currentResult}: Job ${env.JOB_NAME} build ${env.BUILD_NUMBER}\n More info at: ${env.BUILD_URL}",
                recipientProviders: [[$class: 'DevelopersRecipientProvider'], [$class: 'RequesterRecipientProvider']],
                subject: "Jenkins Build ${currentBuild.currentResult}: Job ${env.JOB_NAME}"
                
        }
    }
}
