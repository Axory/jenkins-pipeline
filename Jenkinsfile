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

        stage('Generate Dirty Data'){
            steps {
                sh "${BUILD_TIMESTAMP} > demo.txt"
            }
        }

        stage('Commit'){
            withCredentials([usernamePassword(credentialsId: 'github-testing', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
                sh """
                    git commit -a -m 'Testing commit'
                    git push https://github.com/Axory/jenkins-pipeline.git HEAD:main
                """
            }
        }
    }

    post {
        always {
            deleteDir()
        }
    }
}
