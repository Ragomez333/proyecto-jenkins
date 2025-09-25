# Proyecto Jenkins + Docker

Este proyecto despliega un entorno con **Jenkins (última versión)** y un servidor **Nginx** que sirve una página estática (`index.html`).  
La integración se maneja mediante **Docker Compose** y un **pipeline en Jenkins** definido en el archivo `Jenkinsfile`.

---

## 🚀 Requisitos previos
- Docker Desktop instalado y en ejecución  
- Git instalado  
- Cuenta en GitHub  

---

## 📂 Estructura del proyecto
proyecto-jenkins/
│── index.html
│── Dockerfile
│── Dockerfile.JK
│── docker-compose.yml
│── Jenkinsfile
│── README.md

yaml
Copiar código

---

## ⚙️ Pasos para ejecutar el proyecto

### 1. Clonar el repositorio
```bash
git clone https://github.com/Ragomez333/proyecto-jenkins.git
cd proyecto-jenkins
2. Levantar los contenedores con Docker Compose
bash
Copiar código
docker-compose up -d --build
Esto iniciará:

Jenkins en 👉 http://localhost:8080

Nginx en 👉 http://localhost:8081

Verifica los contenedores activos:

bash
Copiar código
docker ps
🔑 Obtener la contraseña inicial de Jenkins
Ejecuta:

bash
Copiar código
docker exec -it jenkins cat /var/jenkins_home/secrets/initialAdminPassword
O revisa los logs:

bash
Copiar código
docker logs jenkins | grep "Please use the following password"
Con esa clave podrás iniciar sesión en 👉 http://localhost:8080.

📝 Configuración de Jenkins
Abre http://localhost:8080.

Ingresa la contraseña inicial de admin.

Instala los plugins recomendados.

Crea un usuario administrador.

Configura un nuevo Pipeline con tu repositorio de GitHub que contiene el Jenkinsfile.

⚡ Pipeline de Jenkins
El archivo Jenkinsfile realiza los siguientes pasos:

Clona el repositorio desde GitHub.

Construye la imagen web_html con el Dockerfile.

Ejecuta un contenedor Nginx en el puerto 8081.

Verifica que Nginx responde correctamente.

Ejemplo de verificación:

bash
Copiar código
curl -I http://localhost:8081
🌐 Ver la página desplegada
Abre en tu navegador:
👉 http://localhost:8081 → muestra el index.html.

bash
Copiar código
