# Node.js Hello World API - Jenkins Integration

Este repositorio muestra cómo integrar un pipeline de Jenkins con una aplicación Node.js básica, utilizando GitHub Webhooks y ngrok.

---

## Prerrequisitos

1. Cuenta activa en **GitHub**.
2. Jenkins instalado y configurado en tu máquina o servidor.
3. ngrok instalado en tu entorno.

---

## Pasos para Configurar

### 1. Forkear el Repositorio
1. Accede al repositorio original: [Node.js Hello World API](https://github.com/edgaregonzalez/nodejs-helloworld-api).
2. Haz clic en el botón **Fork** para crear una copia en tu cuenta de GitHub.

### 2. Configurar el WebHook
1. Desde tu repositorio fork, accede a **Settings** > **Webhooks** > **Add Webhook**.
2. Completa el formulario:
   - **Payload URL**: Ingresa la URL pública generada por ngrok (ver siguiente paso).
   - **Content Type**: Selecciona `application/json`.
   - **Which events**: Marca las opciones **Push** y **Pull Request**.
3. Haz clic en **Add Webhook**.

### 3. Configurar ngrok
1. Accede al sitio oficial de [ngrok](https://ngrok.com) e instala según tu sistema operativo.
2. Agrega el token de autenticación con:
   ```bash
   ngrok config add-authtoken <tu-token>
3. Despliega el tunel con: ngrok http http://localhost:8080
4. Copia la URL pública proporcionada por ngrok y úsala como Payload URL en el webhook (asegúrate de agregar /github-webhook/ al final).

### 4. Configurar Jenkins
1. Accede a Jenkins y crea un nuevo item seleccionando Pipeline.
2. En la configuración del pipeline:

Selecciona Pipeline script y pega el siguiente script:
pipeline {
    agent any
    triggers {
        githubPush()
    }
    stages {
        stage('Clone Repository') {
            steps {
                git url: 'https://github.com/<tu-usuario>/nodejs-helloworld-api', branch: 'main'
            }
        }
        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }
        stage('Run Tests') {
            steps {
                sh 'npm test'
            }
        }
    }
}

En Build Triggers, selecciona la opción GitHub hook trigger for GITScm polling.

3. Guarda la configuracion.

### 5. Validar la Configuración
1. En Recent Deliveries del WebHook en GitHub, verifica que la solicitud tiene un estado 200 OK.
2. Realiza un cambio en el archivo README.md y haz un commit.
3. Jenkins debería disparar automáticamente el pipeline.

### Validacion Final.
1. Accede al pipeline en Jenkins y revisa la ejecución.
2. Observa los resultados en la consola para asegurarte de que las etapas se completaron con éxito.
   
Este proyecto se basa en la integración de tecnologías de código abierto como Node.js, Jenkins, GitHub, y ngrok para automatizar despliegues y pruebas de aplicaciones.

¡Feliz automatización! 🚀
   
   
