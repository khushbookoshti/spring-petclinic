pipeline {
    agent any
 
    triggers {
        cron('H/10 * * * 1')
    }
 
    stages {
        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage('Code Coverage') {
            steps {
                sh 'mvn jacoco:prepare-agent test jacoco:report'
            }
            post {
                always {
                    jacoco(execPattern: 'target/**.exec')
                    publishHTML(target: [reportDir: 'target/site/jacoco', reportFiles: 'welcome.html', reportName: 'JaCoCo Code Coverage Report'], keepAll: true)
                }
            }
        }
    }
}
