# 🌐 NGINX Optimizado para Caché y Alto Rendimiento

<p align="center">
  <img src="https://www.nginx.com/wp-content/uploads/2019/10/NGINX-logo-rgb-large.png" width="200" alt="NGINX Logo">
</p>

Este proyecto proporciona una configuración optimizada para **NGINX** que incluye caché eficiente para imágenes, archivos CSS, y optimizaciones para conexiones **HTTP/2** y **SSL**. Ideal para aplicaciones de alto tráfico o sitios web que requieren un rendimiento elevado y un manejo eficiente de recursos.

---

## 🚀 Características principales

- **Procesamiento eficiente**: Configuración para aprovechar al máximo los recursos del sistema, ajustando automáticamente los procesos de trabajo según la cantidad de CPUs disponibles.
- **Optimización de caché**: Manejo inteligente de caché para imágenes, CSS, HTML y otros archivos estáticos.
- **Compresión Gzip**: Compresión habilitada para reducir el tamaño de las respuestas y mejorar los tiempos de carga.
- **Soporte SSL y HTTP/2**: Certificados SSL configurados para mejorar la seguridad, junto con soporte para HTTP/2 para una entrega más rápida de recursos.
- **Control de acceso a archivos estáticos**: Cacheado eficiente para reducir la carga del servidor y mejorar la experiencia del usuario final.

---

## 🛠️ Configuración

### 📋 Configuración básica

Esta configuración ajusta el número de **procesos de trabajo** y optimiza el manejo de conexiones:
```nginx
user nginx;
worker_processes auto;  # Ajusta automáticamente según el número de CPU
worker_rlimit_nofile 8192;  # Limitar el número de archivos abiertos
```

### ⚙️ Eventos optimizados
Utiliza el método epoll para un manejo eficiente de las conexiones en sistemas Linux:
```nginx
events {
    worker_connections 1024;
    multi_accept on;
    use epoll;
}
```

### 💾 Configuración de caché de archivos estáticos
El caché para imágenes y archivos CSS se configura para 30 días, mejorando la velocidad de respuesta para los usuarios:
```nginx
location ~* \.(jpg|jpeg|png|gif|ico|css)$ {
    expires 30d;
    add_header Cache-Control "public, no-transform";
}
```

### 🌐 Soporte para SSL/HTTP2
El soporte para SSL y HTTP/2 mejora la seguridad y la velocidad en la entrega de contenidos. Asegúrate de reemplazar los certificados con los tuyos propios:
```nginx
ssl_certificate /path/to/your/certificate.crt;
ssl_certificate_key /path/to/your/certificate.key;
ssl_protocols TLSv1.2 TLSv1.3;
ssl_prefer_server_ciphers on;
listen 443 ssl http2;
```

## 📈 Optimización para rendimiento

### 📦 Caché de archivos abiertos
NGINX mantiene en caché hasta 1000 archivos abiertos para mejorar el rendimiento en servidores que manejan grandes volúmenes de tráfico:
```nginx
open_file_cache max=1000 inactive=20s;
open_file_cache_valid 30s;
open_file_cache_min_uses 2;
open_file_cache_errors on;
```

### ⚡ Compresión Gzip habilitada
La compresión Gzip reduce el tamaño de las respuestas, optimizando el uso del ancho de banda y acelerando la carga de la página:
```nginx
gzip on;
gzip_vary on;
gzip_proxied any;
gzip_comp_level 6;
gzip_types text/plain text/css application/json application/javascript text/xml application/xml;
```


## 📂 Estructura del proyecto
```
.
├── nginx.conf         # Archivo de configuración optimizado para NGINX
├── README.md          # Este archivo
└── ssl/               # Directorio para almacenar tus certificados SSL
    ├── nginx.crt      # Certificado SSL
    └── nginx.key      # Clave privada del certificado SSL
```


## **🔧 Instrucciones de instalación**
1. Clona el repositorio:
```bash
git clone https://github.com/Tagomata/Prueba-Tecnica-B2B-2.git
cd Prueba-Tecnica-B2B-2
```

2. Asegúrate de que tu entorno de NGINX esté instalado y configurado correctamente. Para instalar NGINX, usa el siguiente comando en distribuciones basadas en Ubuntu:
```bash
sudo apt-get install nginx
```

3. Reemplaza los certificados SSL en el directorio ssl/ con tus propios certificados.

4. Copia el archivo nginx.conf al directorio de configuración de NGINX:
```bash
sudo cp nginx.conf /etc/nginx/nginx.conf
```

5. Reinicia NGINX para aplicar la nueva configuración:
```bash
sudo systemctl restart nginx
```

## 🎯 Buenas prácticas incluidas
- Auto-ajuste de workers: El número de procesos de trabajo se ajusta automáticamente al número de núcleos de CPU disponibles en tu máquina.
- Caché de archivos estáticos: Mantiene en caché imágenes y CSS por 30 días para reducir la carga del servidor y mejorar la experiencia del usuario.
- Compresión Gzip: Acelera la entrega de contenido al comprimir los archivos enviados a los usuarios.
- Soporte SSL con HTTP/2: Aumenta la seguridad de las conexiones y mejora el rendimiento mediante el uso de HTTP/2.

  
## **📝 Licencia**
Este proyecto está bajo la Licencia MIT. ¡Siéntete libre de modificarlo y adaptarlo a tus necesidades!

<p align="center"> Con ❤️ por <a href="https://github.com/Tagomata">Tagomata</a> </p>

## **🌟 Contribuye**
¿Tienes ideas para mejorar la configuración? ¡No dudes en enviar un pull request o crear un issue!



