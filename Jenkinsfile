pipeline {
agent any

```
stages {
    stage('Clonar código') {
        steps {
            git branch: 'master',
                url: 'https://github.com/Ragomez333/proyecto-jenkins.git'
        }
    }

    stage('Construir contenedor') {
        steps {
            sh 'docker-compose down || true'
            sh 'docker-compose up -d --build'
        }
    }

    stage('Verificar despliegue') {
        steps {
            sh 'curl -I http://localhost:8081 || true'
        }
    }
}
```

}
