# 🌟 Node.js Hello World API - Jenkins Integration 🚀

Este repositorio muestra cómo integrar un pipeline de Jenkins con una aplicación Node.js básica, utilizando **GitHub Webhooks** y **ngrok**.

---

## ✅ **Prerrequisitos**
Antes de comenzar, asegúrate de contar con los siguientes elementos:
- 🛠️ **Cuenta activa en GitHub.**
- 🖥️ **Jenkins** instalado y configurado en tu máquina o servidor.
- 🌐 **ngrok** instalado en tu entorno local.

---

## 🛠️ **Pasos para Configurar**

### 1️⃣ **Forkear el Repositorio**
1. Accede al repositorio original: [Node.js Hello World API](https://github.com/edgaregonzalez/nodejs-helloworld-api).
2. Haz clic en el botón **Fork** para crear una copia en tu cuenta de GitHub.

### 2️⃣ **Configurar el WebHook**
1. Desde tu repositorio fork, accede a **Settings > Webhooks > Add Webhook**.
2. Completa el formulario:
   - **Payload URL**: Ingresa la URL pública generada por ngrok (ver siguiente paso).
   - **Content Type**: Selecciona `application/json`.
   - **Which events**: Marca las opciones **Push** y **Pull Request**.
3. Haz clic en **Add Webhook**.

### 3️⃣ **Configurar ngrok**
1. Instala **ngrok** desde su [sitio oficial](https://ngrok.com) según tu sistema operativo.
2. Agrega el token de autenticación:
   ```bash
   ngrok config add-authtoken <tu-token>
3. Despliega el túnel: ngrok http http://localhost:8080
4. Copia la URL pública proporcionada por ngrok y úsala como Payload URL en el WebHook (asegúrate de agregar /github-webhook/ al final).

### 4️⃣ **Configurar Jenkins**
1. Accede a Jenkins y crea un nuevo ítem seleccionando **Pipeline**.
2. En la configuración del pipeline:
   - Selecciona **Pipeline script** y pega el siguiente script:

```groovy
pipeline {
    agent any
    triggers {
        githubPush() // Trigger para eventos push desde GitHub
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
    post {
        success {
            echo 'Pipeline completed successfully! ✅'
        }
        failure {
            echo 'Pipeline failed. ❌ Please check the logs!'
        }
    }
}

3. En Build Triggers, selecciona la opción GitHub hook trigger for GITScm polling.
4. Guarda la configuración.

✅ Validar la Configuración
1. En Recent Deliveries del WebHook en GitHub, verifica que las solicitudes tienen un estado 200 OK.
2. Realiza un cambio en el archivo README.md y haz un commit.
3. Jenkins debería disparar automáticamente el pipeline.

🧪 Validación Final
1. Accede al pipeline en Jenkins y revisa la ejecución.
2. Observa los resultados en la consola para asegurarte de que las etapas se completaron con éxito.

🛠️ Tecnologías Utilizadas
⚙️ Node.js
🛠️ Jenkins
🌐 GitHub
🚀 ngrok

🎉 ¡Feliz Automatización! 🚀
