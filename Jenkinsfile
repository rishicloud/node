pipeline {
    agent { label 'rishi12' }
    options { 
        timeout(time: 1, unit: 'HOURS')
        retry(2) 
    }
    triggers {
        cron('0 * * * *')
    }
    parameters {
        choice(name: 'GOAL', choices: ['install', 'pack', 'run build'])
    }
    stages {
        stage('Source Code') {
            steps {
                git url: 'https://github.com/rishicloud/node.git', 
                branch: 'main'
            }

        }
        stage('Build the Code and sonarqube-analysis') {
            steps {
                withSonarQubeEnv('SONAR_9.3') {
                    sh script: "npm ${params.GOAL} sonar:sonar"
                }

            }
        }
        stage('reporting') {
            steps {
                junit testResults: 'target/surefire-reports/*.xml'
            }
        }

    }

}