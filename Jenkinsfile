pipeline {
    agent any
    
    stages {
        stage('Checkout') {
            steps {
               sshPublisher(publishers: [sshPublisherDesc(configName: 'Myphp', transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: '', execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '/var/www/html/', remoteDirectorySDF: false, removePrefix: '', sourceFiles: '**/*.php')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])
            }
        }
        
        
    }  
}
