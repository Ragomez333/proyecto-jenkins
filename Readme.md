# Proyecto Jenkins + Docker

Este proyecto despliega un entorno con **Jenkins (última versión)** y un servidor **Nginx** que sirve una página estática (`index.html`).
La integración se maneja mediante **Docker Compose** y un **pipeline en Jenkins** definido en el archivo `Jenkinsfile`.

---

## 🚀 Requisitos previos

* [Docker Desktop](https://www.docker.com/products/docker-desktop) instalado y en ejecución
* [Git](https://git-scm.com/downloads) instalado
* Cuenta en [GitHub](https://github.com)

---

## 📂 Estructura del proyecto

```
proyecto-jenkins/
│── index.html
│── docker-compose.yml
│── Jenkinsfile
│── README.md
```

---

## ⚙️ Pasos para ejecutar el proyecto

### 1. Clonar el repositorio

```bash
git clone https://github.com/Ragomez333/proyecto-jenkins.git
cd proyecto-jenkins
```

### 2. Levantar los contenedores con Docker Compose

```bash
docker-compose up -d
```

Esto iniciará:

* **Jenkins** en `http://localhost:8080`
* **Nginx** en `http://localhost:8081`

Verifica los contenedores activos:

```bash
docker ps
```

---

## 🔑 Obtener la contraseña inicial de Jenkins

Ejecuta:

```bash
docker exec -it jenkins cat /var/jenkins_home/secrets/initialAdminPassword
```

O revisa los logs:

```bash
docker logs jenkins | Select-String "Please use the following password"
```

Con esa clave podrás iniciar sesión en `http://localhost:8080`.

---

## 📝 Configuración de Jenkins

1. Abre [http://localhost:8080](http://localhost:8080).
2. Ingresa la contraseña inicial de admin.
3. Instala los plugins recomendados.
4. Crea un usuario administrador.
5. Configura un nuevo **Pipeline** con tu repositorio de GitHub que contiene el `Jenkinsfile`.

---

## ⚡ Pipeline de Jenkins

El archivo `Jenkinsfile` realiza los siguientes pasos:

* Clona el repositorio desde GitHub
* Reconstruye los contenedores (`docker-compose up -d --build`)
* Verifica que Nginx responde correctamente

Ejemplo de verificación:

```bash
curl -I http://localhost:8081
```

---

## 🌐 Ver la página desplegada

Abre en tu navegador:

* [http://localhost:8081](http://localhost:8081) → muestra el `index.html`

---
