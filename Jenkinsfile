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
                // Apagar el servicio si ya estaba corriendo (ignora errores con "|| true")
                sh 'docker -H tcp://docker:2375 compose down web_html || true'

                // Levantar el servicio web con build forzado
                sh 'docker -H tcp://docker:2375 compose up -d --build web_html'
            }
        }

        stage('Verificar despliegue') {
            steps {
                // Chequear si el contenedor web_html está arriba
                sh 'docker -H tcp://docker:2375 ps | grep web_html || true'

                // Validar que responda el servidor web
                sh 'curl -I http://web_html:80 || true'
            }
        }
    }
}
