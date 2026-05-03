<h1 style="color:#0d47a1;">📘 Optimización Web: Nginx Reverse Proxy con Caché</h1>

<p><strong>Fecha de creación:</strong> 04-06-2025 | <strong>Última modificación:</strong> 04-06-2025</p>

---

## 🎯 Objetivo

<p style="color:#000000;">
  Implementar un sistema de caché web de alto rendimiento utilizando Nginx como Proxy Inverso. Se configurarán dos rutas diferenciadas (`/cached` y `/nocached`) apuntando al mismo backend Apache. Finalmente, se realizarán pruebas de estrés con <strong>Apache Benchmark (ab)</strong> desde un cliente Linux Desktop para comparar la latencia y el rendimiento.
</p>

---

## 🛠️ Tecnologías

- Docker, Nginx (Proxy & Cache), Apache HTTP Server (Backend), Apache Benchmark (`ab`), Linux Server.

---

## 📦 Dependencias

- Instalación de Docker en Linux Server. [Aquí](../linux/00%20Docker.md)
- Cliente Linux Desktop con acceso a red al servidor Docker.

---

## 🖥️ Entorno

- <strong>Servidor:</strong> Linux Server 24.04 (Docker Host).
- <strong>Cliente:</strong> Linux Desktop (Ubuntu/Debian).

---

## ▶️ Pasos

| #  | Paso       | Instrucciones       | Pantallazo    |
|----|------------|---------------------|---------------|
| 00 | Preparar directorios | Crear la estructura de carpetas para la configuración del proxy. Ejecutar: `mkdir -p practica_cache/proxy` y acceder: `cd practica_cache`. | ![img](./assets/22/00_estructura.png)   |
| 01 | Crear Red Docker | Crear una red aislada para la práctica. Comando: `docker network create --subnet=172.30.0.0/16 cache_net`. | ![img](./assets/22/01_red.png)   |
| 02 | Despliegue Backend (Apache) | Lanzar un servidor Apache estándar que servirá como "origen". Comando: `docker run -d --name web_backend --net cache_net --ip 172.30.0.10 httpd:latest`. | ![img](./assets/22/02_backend.png)   |
| 03 | Configurar Nginx Caché | Crear el fichero `default.conf` dentro de la carpeta `proxy`. Se debe definir la directiva `proxy_cache_path` y dos `locations` (`/cached` y `/nocached`) que apunten al backend 172.30.0.10. [Ver código de configuración](./code/22/nginx_cache.md) | ![img](./assets/22/03_config_nginx.png)   |
| 04 | Despliegue Proxy Nginx | Lanzar el contenedor Nginx exponiendo el puerto 80 y montando la configuración. Comando: `docker run -d --name nginx_proxy --net cache_net --ip 172.30.0.20 -p 80:80 -v $(pwd)/proxy/default.conf:/etc/nginx/conf.d/default.conf nginx:latest`. | ![img](./assets/22/04_deploy_proxy.png)   |
| 05 | Instalar Apache Benchmark (Cliente) | En la máquina **Cliente Linux Desktop**, instalar las herramientas de benchmarking. Comando: `sudo apt install apache2-utils -y`. | ![img](./assets/22/05_install_ab.png)   |

---

## ✅ Tests

| #  | Descripción       | Resultado esperado       | Pantallazo    |
|----|-------------------|--------------------------|---------------|
| 00 | Test SIN Caché (Línea Base) | Ejecutar desde el cliente: `ab -n 2000 -c 10 http://[IP_SERVIDOR]/nocached/`. Observar el valor **"Requests per second"** y **"Time per request"**. | ![img](./assets/22/00_test_nocached.png)   |
| 01 | Primer acceso a Caché (MISS) | Acceder con el navegador a `http://[IP_SERVIDOR]/cached/`. La primera petición llenará la caché (Estado: MISS). | ![img](./assets/22/01_test_browser.png)   |
| 02 | Test CON Caché (HIT) | Ejecutar de nuevo el benchmark a la ruta optimizada: `ab -n 2000 -c 10 http://[IP_SERVIDOR]/cached/`. El rendimiento (**Requests per second**) debería aumentar drásticamente (x10 o más) respecto al test 00. | ![img](./assets/22/02_test_cached.png)   |

---

## 📚 Referencias / Documentación

- 00 [Guía oficial de Nginx Content Caching](https://docs.nginx.com/nginx/admin-guide/content-cache/content-caching/)
- 01 [Manual de Apache Benchmark (ab)](https://httpd.apache.org/docs/2.4/programs/ab.html)

---

### 📝 Notas para el fichero de configuración (`nginx_cache.md`)
*Contenido sugerido para el fichero enlazado en el paso 03:*

```nginx
proxy_cache_path /var/cache/nginx/my_cache levels=1:2 keys_zone=my_cache:10m max_size=1g inactive=60m use_temp_path=off;

server {
    listen 80;

    # Ruta SIN caché: Pasa directamente al backend
    location /nocached/ {
        proxy_pass [http://172.30.0.10/](http://172.30.0.10/);
        proxy_set_header Host $host;
    }

    # Ruta CON caché
    location /cached/ {
        proxy_pass [http://172.30.0.10/](http://172.30.0.10/);
        proxy_cache my_cache;
        proxy_cache_valid 200 302 10m;
        proxy_cache_valid 404      1m;
        
        # Header para ver si es HIT o MISS desde el navegador
        add_header X-Cache-Status $upstream_cache_status;
    }
}