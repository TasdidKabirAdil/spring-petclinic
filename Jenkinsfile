pipeline {
    agent any

    stages {
        // Stage 1: Compile and build the project
        stage('Build') {
            steps {
                bat 'mvn clean package'  // Use "bat" for Windows instead of "sh"
            }
        }

        // Stage 2: Generate JaCoCo Code Coverage Report
        stage('Code Coverage (JaCoCo)') {
            steps {
                bat 'mvn test'  // Use "bat" here too
            }
            post {
                always {
                    jacoco(
                        execPattern: '**/target/jacoco.exec',
                        classPattern: '**/target/classes',
                        sourcePattern: '**/src/main/java'
                    )
                }
            }
        }
    }

    // Schedule every 3 minutes on Thursdays
    triggers {
        cron('H/3 * * * 4') 
    }
}