pipeline {
    agent any

    stages {
        stage('Iniciando a pipeline') {
            steps {
                echo 'Iniciando a pipeline'
            }
        }

        stage ('Buildando a imagem Docker') {
            steps {
                script {
                    dockerapp = docker.build("pereirafmauro/desafio-devops:${env.BUILD_TAG}", '-f ./src/Docker/Dockerfile ./src/Docker')
                }
            }
        }
    }
}
