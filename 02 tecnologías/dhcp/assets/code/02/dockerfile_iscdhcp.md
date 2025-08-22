```

# Imagen base
FROM debian:stable-slim

# Variables de entorno necesarias para isc-dhcp-server
ENV DEBIAN_FRONTEND=noninteractive
ENV DHCP_CONFIG_FILE=/etc/dhcp/dhcpd.conf

# Instalamos isc-dhcp-server
RUN apt-get update && \
    apt-get install -y isc-dhcp-server && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# Creamos directorio para logs (opcional)
RUN mkdir -p /var/lib/dhcp

# Declaramos el volumen para la configuración externa
VOLUME ["/etc/dhcp"]

# Puerto estándar DHCP (UDP)
EXPOSE 67/udp

# Comando de inicio
CMD ["/usr/sbin/dhcpd", "-f", "-d", "--no-pid", "-cf", "/etc/dhcp/dhcpd.conf"]

```