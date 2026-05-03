<h1 style="color:#0d47a1;">📘 Despliegue de Proxy Inverso y Balanceador de Carga con Docker</h1>

<p><strong>Fecha de creación:</strong> 04-06-2025 | <strong>Última modificación:</strong> 04-06-2025</p>

---

## 🎯 Objetivo

<p style="color:#000000;">
  Implementar una arquitectura de red contenerizada utilizando Docker. Se desplegarán dos servidores web Apache y un servidor Nginx configurado como Proxy Inverso y Balanceador de Carga (algoritmo Round Robin) para distribuir las peticiones entre los backends.
</p>

---

## 🛠️ Tecnologías

- Docker, Docker Compose, Nginx, Apache HTTP Server, Linux Server.

---

## 📦 Dependencias

- Instalación y configuración de Docker en Linux Server. [Aquí](../linux/00%20Docker.md)

---

## 🖥️ Entorno

- <strong>Nombre:</strong> Linux Server 24.04 (o entorno de laboratorio Docker).

---

## ▶️ Pasos

| #  | Paso       | Instrucciones       | Pantallazo    |
|----|------------|---------------------|---------------|
| 00 | Preparar estructura de directorios | Crear carpetas para alojar los ficheros HTML de los servidores y la configuración del proxy. Ejecutar: `mkdir -p practica_lb/{web1,web2,proxy}` y acceder al directorio `cd practica_lb` | ![img](./assets/21/00_estructura.png)   |
| 01 | Crear la red Docker personalizada | Crear una red tipo bridge llamada `aq_red` con direccionamiento específico. Comando: `docker network create --subnet=172.28.0.0/16 aq_red` | ![img](./assets/21/01_red_docker.png)   |
| 02 | Crear contenido Web 1 | Crear un fichero `index.html` en la carpeta `web1`. Contenido: `<h1>Servidor WEB 1</h1>`. [Ver código](./code/21/web1_html.md) | ![img](./assets/21/02_web1.png)   |
| 03 | Desplegar Servidor Apache 1 (aq_web1) | Lanzar el contenedor Apache con IP fija y volumen montado. Comando: `docker run -d --name aq_web1 --net aq_red --ip 172.28.0.10 -v $(pwd)/web1:/usr/local/apache2/htdocs/ httpd:latest` | ![img](./assets/21/03_deploy_web1.png)   |
| 04 | Crear contenido Web 2 | Crear un fichero `index.html` en la carpeta `web2`. Contenido: `<h1>Servidor WEB 2</h1>`. [Ver código](./code/21/web2_html.md) | ![img](./assets/21/04_web2.png) |
| 05 | Desplegar Servidor Apache 2 (aq_web2) | Lanzar el segundo contenedor Apache con IP fija. Comando: `docker run -d --name aq_web2 --net aq_red --ip 172.28.0.20 -v $(pwd)/web2:/usr/local/apache2/htdocs/ httpd:latest` | ![img](./assets/21/05_deploy_web2.png)   |
| 06 | Configurar Nginx (Balanceador) | Crear el fichero `default.conf` en la carpeta `proxy`. Se debe definir el `upstream backend` con las IPs 172.28.0.10 y 172.28.0.20. [Ver código de configuración](./code/21/nginx_conf.md) | ![img](./assets/21/06_config_nginx.png)   |
| 07 | Desplegar Proxy Nginx (aq_proxy) | Lanzar el contenedor Nginx exponiendo el puerto 80 y montando la configuración. Comando: `docker run -d --name aq_proxy --net aq_red --ip 172.28.0.50 -p 80:80 -v $(pwd)/proxy/default.conf:/etc/nginx/conf.d/default.conf nginx:latest` | ![img](./assets/21/07_deploy_proxy.png)   |

---

## ✅ Tests

| #  | Descripción       | Resultado esperado       | Pantallazo    |
|----|-------------------|--------------------------|---------------|
| 00 | Verificar contenedores en ejecución | Ejecutar `docker ps`. Deben aparecer 3 contenedores: `aq_proxy`, `aq_web1` y `aq_web2` en estado "Up". | ![img](./assets/21/00_test_ps.png)   |
| 01 | Comprobar balanceo de carga | Acceder desde el navegador o mediante `curl http://localhost`. Al recargar la página varias veces, el contenido debe alternar entre "Servidor WEB 1" y "Servidor WEB 2" (Round Robin). | ![img](./assets/21/01_test_curl.png)   |

---

## 📚 Referencias / Documentación

- 00 [Documentación oficial de Nginx Reverse Proxy](https://docs.nginx.com/nginx/admin-guide/web-server/reverse-proxy/)
- 01 [Documentación oficial de Docker Networking](https://docs.docker.com/network/)