pipeline {
    agent any
    parameters {
        string(name: 'MY_PARAM', defaultValue: 'world', description: 'A parameter for the pipeline')
    }
    triggers {
        cron('H 0 * * *') // Периодический запуск по расписанию (ежедневно в полночь)
    }
    environment {
        MY_CREDENTIALS = credentials('my-credentials-id')
    }
    stages {
        stage('Cleanup') {
            steps {
                cleanWs() // Очистка рабочего каталога
            }
        }
        stage('Write File') {
            steps {
                script {
                    def content = "Hello+${params.MY_PARAM}"
                    writeFile(file: 'result.txt', text: content)
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
            cleanWs() // Очистка рабочего каталога в конце
        }
    }
}
