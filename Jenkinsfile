pipeline {
    agent {
        label 'core'
    }

    options {
        disableConcurrentBuilds()
        ansiColor('xterm')
        buildDiscarder(logRotator(numToKeepStr: '5'))
    }

    tools {
        maven 'apache-maven-3.5.0'
        jdk 'openjdk_11.0.8'
    }

    stages {
        stage('GIT'){
            steps {
                checkout scm
            }
        }
    }

    post {
        always {
            deleteDir()
        }
    }
}
