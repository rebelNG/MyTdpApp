pipeline {
    agent any

    stages {
        stage('Verify branch') {
            steps {
                echo "$GIT_BRANCH"
            }
        }

        stage('Docker Build') {
            steps {
                script {
                    dir('MyTdpApp') {
                        sh 'docker images -a'
                        sh 'docker build -t jenkins-pipeline .'
                        sh 'docker images -a'
                    }
                }
            }
        }
    }
}