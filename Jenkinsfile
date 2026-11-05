pipeline {
    agent { label 'docker-build' }

    stages {
        stage('Verify Agent') {
            steps {
                sh 'hostname'
                sh 'whoami'
                sh 'pwd'
                sh 'git --version'
            }
        }
    }
}
