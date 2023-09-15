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
                // Use the configured PowerShell tool
                powershell script: 'docker images -a'
                powershell script: """
                    docker images -a
                    docker build -t jenkins-pipeline .
                    docker images -a
                    cd ..
                """
            }
        }

        stage('Push Container') {
            steps {
                echo "Workspace is $WORKSPACE"
                dir("$WORKSPACE/") {
                    script {
                        docker.withRegistry('https://index.docker.io/v1/', 'DockerHub'){
                            def image = docker.build('rebelng/jenkins-tutorial:latest')
                            image.push()
                        }
                    }
                }
            }
        }
    }
}