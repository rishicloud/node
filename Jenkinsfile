pipeline {
    agent { label 'rishi12' }
    triggers { 
        cron('45 23 * * 1-5')
        pollSCM('*/5 * * * *')
    }


    stages {
        stage('scm') {
            steps {

                git url: 'https://github.com/rishicloud/node.git', branch: 'main'
            }
        }
        stage('build') {
            steps {
                 withSonarQubeEnv(installationName: 'SONAR_9.3', envOnly: true, credentialsId: 'SONAR_TOKEN') {
                    sh 'npm install  sonar:sonar'  
                    echo "${env.SONAR_HOST_URL}"
                                
                }
            }
        }
		stage("Quality Gate") {
            steps {
                timeout(time: 1, unit: 'HOURS') {
                    // Parameter indicates whether to set pipeline to UNSTABLE if Quality Gate fails
                    // true = set pipeline to UNSTABLE, false = don't
                    waitForQualityGate abortPipeline: true
                }
            }
        }
    }
}