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

   
