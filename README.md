
# 📥 Setup qBittorrent with Docker Compose

Este proyecto proporciona una configuración lista para usar de **qBittorrent** con **Docker Compose**.

---

## 🚀 Instalación

### 1️⃣ Clonar el repositorio
```sh
git clone https://github.com/giarf/setup-qbittorrent.git
cd setup-qbittorrent
```

### 2️⃣ Configurar los volúmenes y permisos (Opcional)
Si deseas configurar los volúmenes manualmente:

```sh
mkdir -p config downloads
chmod -R 777 config downloads
```

### 3️⃣ Levantar el contenedor con Docker Compose
```sh
docker-compose up -d
```

Esto ejecutará **qBittorrent** en segundo plano.

---

## 🛠️ Configuración

Por defecto, el servicio usa:

- **Puerto WebUI:** `8082`
- **Usuario:** `admin`
- **Contraseña:** `adminadmin`

Puedes cambiar estos valores en el archivo `docker-compose.yml`.

Para verificar los logs del contenedor:

```sh
docker logs -f qbittorrent
```

Para reiniciar el contenedor:

```sh
docker-compose restart
```

Para detener y eliminar los contenedores:

```sh
docker-compose down
```

---

## 📁 Estructura del Proyecto

```
setup-qbittorrent/
│── docker-compose.yml   # Configuración del contenedor
│── config/              # Configuración persistente de qBittorrent
│── downloads/           # Carpeta de descargas
```

---

## 🐳 **docker-compose.yml**
Este es el contenido del archivo `docker-compose.yml`:

```yaml
services:
  qbittorrent:
    image: lscr.io/linuxserver/qbittorrent:latest
    container_name: qbittorrent
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=Amrica/Santiago
      - WEBUI_PORT=8080
      - TORRENTING_PORT=6881
    volumes:
      - ./config:/config
      - ./downloads:/downloads #optional
    ports:
      - 8082:8080
      - 6881:6881
      - 6881:6881/udp
    restart: unless-stopped
```

---

## ⚡ Acceder a qBittorrent

Después de ejecutar `docker-compose up -d`, puedes acceder a **qBittorrent** desde tu navegador:

🌍 **http://localhost:8082**

Usuario: `admin`  
Contraseña: `adminadmin` (puedes cambiarla en la configuración web)

---

## ❓ Solución de Problemas

### 🔹 Permisos de carpetas
Si tienes problemas con permisos, intenta:

```sh
sudo chown -R 1000:1000 config downloads
sudo chmod -R 777 config downloads
```

### 🔹 Contenedor no inicia
Verifica los logs con:

```sh
docker logs qbittorrent
```

---

## 📜 Licencia
Este proyecto está bajo la licencia **MIT**.

---

### 🎯 ¡Disfruta de qBittorrent con Docker! 🚀
```

---
