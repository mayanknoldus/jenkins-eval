pipeline {
    agent any

//     environment{
  
//     }

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
            steps {
                sh 'mvn package'
                }
        }
    }

    post {
        always {
            emailext attachLog: true, body: '$DEFAULT_CONTENT', subject: '$DEFAULT_SUBJECT', to: 'mayank.verma@knoldus.com'
        }
    }
}











// pipeline systax
