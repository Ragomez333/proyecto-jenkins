pipeline {
    agent any

    environment {
        DOCKER_HOST = "tcp://dind:2375"
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'master', url: 'https://github.com/Ragomez333/proyecto-jenkins.git'
            }
        }

        stage('Build Web Image') {
            steps {
                sh 'docker rm -f web_html || true'
                sh 'docker build -t web_html:latest -f Dockerfile .'
                sh 'docker run -d --name web_html -p 8081:80 web_html:latest'
            }
        }

        stage('Verificar despliegue') {
            steps {
                sh 'curl -I http://localhost:8081 || true'
            }
        }
    }
}
