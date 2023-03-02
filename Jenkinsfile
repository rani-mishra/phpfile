pipeline {
    agent any
    stages {
        stage('Environment') {
            environment {
            AWS_ACCESS_KEY_ID = credentials('AKIAWPWJDKD5FY7QDU7A')
            AWS_SECRET_ACCESS_KEY = credentials('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')
            AWS_DEFAULT_REGION = 'ap-south-1'
            ASG_NAME = 'Php-Autoscaling-Group'
            DESIRED_CAPACITY = 1
            MIN_CAPACITY = 1
            MAX_CAPACITY = 1
          }
        }
        
    
        stage('Checkout') {
            steps {
               sshPublisher(publishers: [sshPublisherDesc(configName: 'Myphp', transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: 'sudo cp /home/ec2-user/index.php  /var/www/html/', execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '/', remoteDirectorySDF: false, removePrefix: '', sourceFiles: '**/*.php')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])
            }
        }
        
        stage('Update ASG') {
            steps {
                script {
                    // Set ASG capacity
                    sh "aws autoscaling update-auto-scaling-group --auto-scaling-group-name ${ASG_NAME} --desired-capacity ${DESIRED_CAPACITY} --min-size ${MIN_CAPACITY} --max-size ${MAX_CAPACITY}"
                    // Wait for capacity update to complete
                    sh "aws autoscaling wait auto-scaling-group-in-service --auto-scaling-group-name ${ASG_NAME}"
                }
            }
        }
    }
}  
