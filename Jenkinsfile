pipeline {
    agent any

    environment {
        DOCKER_HOST = "tcp://docker:2375"
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'master', url: 'https://github.com/Ragomez333/proyecto-jenkins.git'
            }
        }

        stage('Build & Run Web') {
            steps {
                // Detener contenedor anterior si existe
                sh 'docker rm -f web_html || true'

                // Construir imagen desde el repo
                sh 'docker build -t web_html:latest .'

                // Levantar contenedor en el puerto 8081
                sh 'docker run -d --name web_html -p 8081:80 web_html:latest'
            }
        }

        stage('Verificar despliegue') {
            steps {
                // Verificar respuesta HTTP del index
                sh 'curl -I http://localhost:8081 || true'
            }
        }
    }
}
