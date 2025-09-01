# DNS

**Bienvenid@s a la sección del servicio "DNS".**

El DNS (Domain Name Server) es un servicio que traduce nombres de dominio (como por ejemplo google.com) a direcciones IP de forma que permita la comunicación de dispositivos dentro de una red.

**Funciones pricipales:**
- Resolver nombres de dominio a direcciones IP.
- Facilitar la navegación en Internet (o cualquier otra red) con nombres fáciles de recordar.
- Permitir el funcionamiento de servicios como web, correo, etc.

**Registros DNS más comunes en un fichero de zona**

| Registro | Descripción | Ejemplo |
|----------|-------------|---------|
| **SOA** (Start of Authority) | Indica la autoridad principal de la zona. Contiene el servidor primario, correo del admin, número de serie y parámetros de actualización. | `@ IN SOA ns1.midominio.com. admin.midominio.com. (2025082301 3600 1800 1209600 86400)` |
| **NS** (Name Server) | Define los servidores DNS autorizados para la zona. | `@ IN NS ns1.midominio.com.` |
| **A** (Address) | Asocia un nombre de dominio con una dirección IPv4. | `www IN A 192.168.1.10` |
| **AAAA** (IPv6 Address) | Asocia un nombre de dominio con una dirección IPv6. | `www IN AAAA 2001:db8::1` |
| **CNAME** (Canonical Name) | Alias de otro dominio. El nombre indicado apunta al canónico. | `ftp IN CNAME www.midominio.com.` |
| **MX** (Mail Exchange) | Define los servidores de correo del dominio y su prioridad. | `@ IN MX 10 mail.midominio.com.` |
| **TXT** (Text) | Almacena información en texto. Usado para SPF, DKIM, verificaciones, etc. | `@ IN TXT "v=spf1 include:_spf.google.com ~all"` |
| **PTR** (Pointer) | Registro de resolución inversa: vincula una IP a un dominio. | `10.1.168.192.in-addr.arpa. IN PTR servidor.midominio.com.` |
| **SRV** (Service Record) | Define la ubicación (host y puerto) de servicios específicos como SIP, LDAP o Microsoft 365. | `_sip._tcp.midominio.com. IN SRV 10 60 5060 sipserver.midominio.com.` |


# Índice de pruebas de concepto

|# Id. | Prueba de concepto                                                 |
|----- |:---------------------------------------------------------:|
| 00   |  [DNS en Windows Server](./00%20DNS%20en%20Windows%20Server.md)|
| 01   |  [DNS en Ubuntu Server (Bind9)](./01%20DNS%20en%20Linux%20Server.md)|
| 02   |  [DNS en Docker](./02%20DNS%20en%20Docker.md)|