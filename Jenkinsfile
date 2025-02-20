pipeline {
    agent any

    tools {
        maven 'Maven'  // Ensure this matches the name configured in Jenkins Global Tool Configuration
    }

    stages {
        stage('Build') {
            steps {
                script {
                    sh 'mvn clean package'
                }
            }
        }

        stage('Test') {
            steps {
                script {
                    sh 'mvn test'
                }
            }
        }

        stage('Code Coverage') {
            steps {
                script {
                    sh 'mvn jacoco:report'
                }
            }
        }
    }

    post {
        always {
            node {  // Ensuring it runs inside a Jenkins node
                junit '**/target/surefire-reports/*.xml'
                archiveArtifacts artifacts: '**/target/*.jar', fingerprint: true
            }
        }
    }

    triggers {
        cron('H/3 * * * 4') // Runs every 3 minutes on Thursdays
    }
}
