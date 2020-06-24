pipeline {
    agent any
    options {
        buildDiscarder logRotator(numToKeepStr: '5')
    }
    stages {
        stage('Zip') {
            steps {
                zip archive: true, dir: './', glob: '', zipFile: 'WebPage.zip'
            }
        }
        stage('Docker Build') {
            steps {
                sh encoding: 'UTF-8', label: '', returnStdout: true, script: '''
                docker build -t jenkins-basic:1.0.0-${BUILD_NUMBER} .
                docker tag jenkins-basic:1.0.0-${BUILD_NUMBER} jenkins-basic:latest
                '''
            }
        }
        stage('Docker Run') {
            steps {
                sh encoding: 'UTF-8', label: '', returnStdout: true, script: '''
                /usr/bin/docker-compose down
                /usr/bin/docker-compose up -d
                '''
            }
        }
    }
}