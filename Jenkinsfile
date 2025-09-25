pipeline {
    agent any

    stages {
        stage('Clonar código') {
            steps {
                git branch: 'master',
                    url: 'https://github.com/Ragomez333/proyecto-jenkins.git'
            }
        }

        stage('Construir contenedor web') {
            steps {
                // Apagar el contenedor web si existe
                sh 'docker compose down web_html || true'

                // Levantar el servicio web_html
                sh 'docker compose up -d --build web_html'
            }
        }

        stage('Verificar despliegue') {
            steps {
                sh 'curl -I http://localhost:8081 || true'
            }
        }
    }
}
// Fin del Jenkinsfile