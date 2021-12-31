pipeline {
    agent any

    environment{
        --
        --
    }

    tools{
        maven 'mvn'
    }

    stages {

        stage("Cleanup")
        {
            steps
            {
                sh 'mvn clean'
            }
        }

        stage('Compile and Test the Code') {
            stages {
                stage('Compile the Code') {
                    steps {
                        sh 'mvn compile'
                    }
                }
                
                stage('Test the Code') {
                    steps {
                        sh 'mvn test'
                    }
                }
            }
        }

        stage('Deploy the Code') {
            when {
                branch 'Production'
            }
            stages {
                stage {
                    steps {
                        sh 'mvn package'
                    }
                }
                
                stage {
                    steps {
                        sshPublisher(publishers: [sshPublisherDesc(configName: 'deploy', transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: 'java -jar hello-0.0.1-SNAPSHOT.jar &', execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '/home/ubuntu', remoteDirectorySDF: false, removePrefix: '', sourceFiles: '**/*.jar ')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])
                    }
                }
            }
            
            
        }
    }

    post {
        always {
            mail bcc: '', body: 'Hi there,', cc: '', from: '', replyTo: '', subject: 'Test Email', to: 'mayankkverma1999@gmail.com'
        }
    }
}











// pipeline systax