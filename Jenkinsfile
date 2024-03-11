pipeline {
    agent any

    triggers {
        cron('H/10 * * * 1')
    }

    stages {
        stage('Build') {
            steps {
                bat 'mvn clean package'
            }
        }
        stage('Code Coverage') {
            steps {
                bat 'mvn jacoco:prepare-agent test jacoco:report'
            }
            post {
                always {
                    jacoco(execPattern: 'target/**/*.exec')
                    publishHTML(target: [reportDir: 'target/site/jacoco', reportFiles: 'index.html', reportName: 'JaCoCo Code Coverage Report'], keepAll: true)
                }
            }
        }
    }
}
