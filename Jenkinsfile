pipeline {
    agent {label 'rishi12'}
    stages {
        stage('git'){
           steps {
                git branch: 'main', url: 'https://github.com/bravatjammu/node.git'
            }
        }

        stage('build'){
            steps {
                sh 'npm install'
                sh 'npm run build'
                sh 'npm pack'  
            }
        }        

    }
}