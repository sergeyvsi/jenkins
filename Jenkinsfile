pipeline {
    agent { label 'default' }
    parameters {
        string(name: 'MY_PARAM', defaultValue: 'world', description: 'A parameter for the pipeline')
    }
    triggers {
        cron('H 0 * * *')
    }

    environment {
        MY_CREDENTIALS = credentials('my-credentials-id')
    }

    stages {
        stage('Write File') {
            steps {
                script {
                    def content = "Hello+${params.MY_PARAM}"
                    writeFile(file: 'output.txt', text: content)
                }
            }
        }

        stage('Archive Artifacts') {
            steps {
                archiveArtifacts artifacts: 'result.txt', allowEmptyArchive: true
            }
        }
    }

    post {
        always {
            cleanWs()
        }
    }
}
