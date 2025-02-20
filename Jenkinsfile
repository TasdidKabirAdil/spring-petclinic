pipeline {
    agent any

    triggers {
        cron('H/3 * * * 4') // Runs every 3 minutes on Thursdays
    }

    environment {
        MAVEN_HOME = tool 'Maven' // Ensure Maven is installed in Jenkins
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/TasdidKabirAdil/spring-petclinic.git'
            }
        }

        stage('Build') {
            steps {
                sh '${MAVEN_HOME}/bin/mvn clean package'
            }
            post {
                success {
                    archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
                }
            }
        }

        stage('Run Tests with JaCoCo') {
            steps {
                sh '${MAVEN_HOME}/bin/mvn test jacoco:report'
            }
            post {
                success {
                    jacoco execPattern: 'target/jacoco.exec', classPattern: 'target/classes', sourcePattern: 'src/main/java', exclusionPattern: '**/generated/**'
                }
            }
        }
    }

    post {
        always {
            junit 'target/surefire-reports/*.xml'
        }
    }
}
 
