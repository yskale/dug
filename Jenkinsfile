pipeline {
    agent {
        kubernetes {
            cloud 'kubernetes'
            label 'agent-docker'
            defaultContainer 'agent-docker'
        }
    }
    stages {
        stage('Install') {
            steps {
                sh '''
                make install
                '''
            }
        }
        stage('Test') {
            steps {
                sh '''
                make test
                '''
            }
        }
        stage('Publish') {
            when {
                tag "release-*"
            }
            steps {
                sh '''
                make build
                make publish
                '''
            }
        }
    }
}