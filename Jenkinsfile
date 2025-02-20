pipeline {
    agent any

    stages {
        // Stage 1: Compile and build the project
        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        // Stage 2: Generate JaCoCo Code Coverage Report
        stage('Code Coverage (JaCoCo)') {
            steps {
                sh 'mvn test' // Runs tests and generates JaCoCo report
            }
            post {
                always {
                    // Archive the JaCoCo report
                    jacoco(
                        execPattern: '**/target/jacoco.exec',
                        classPattern: '**/target/classes',
                        sourcePattern: '**/src/main/java'
                    )
                }
            }
        }
    }

    // Pipeline will trigger every 3 minutes on Thursdays
    triggers {
        cron('H/3 * * * 4') // Cron syntax: every 3 minutes on Thursdays
    }
}