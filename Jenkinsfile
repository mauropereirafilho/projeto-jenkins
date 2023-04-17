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
                    dockerapp = docker.build("pereirafmauro/desafio-devops", '-f ./Docker/Dockerfile ./Docker')
                }
            }
        }

        stage ('Push para o Dockerhub') {
            steps {
                script {
                    docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
                        dockerapp.push('latest')
                        dockerapp.push("${env.BUILD_ID}")
                    }    
                }
            }
        }
        
        stage ('Deploy no Kubernetes') {
            steps {
                withKubeConfig ([credentialsID: 'kubeconfig']) {
                    sh 'kubectl create -f ./Kubernetes'
                }

            }
        }
    }
}