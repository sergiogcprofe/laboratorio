# Ejemplo de configuración para una subred

```

subnet 192.168.10.0 netmask 255.255.255.0 {
  range 192.168.10.10 192.168.10.50;
  option domain-name-servers 8.8.8.8;
  option subnet-mask 255.255.255.0;
  option routers 192.168.10.1;
  option broadcast-address 192.168.10.255;
  default-lease-time 600;
  max-lease-time 7200;
}

```

| Palabra clave                | Descripción                                                                                                                                       |
| ---------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- |
| `subnet`                     | Define el identificador de red que se va a configurar con DHCP. En este caso, `192.168.10.0` es la red.                                           |
| `netmask`                    | Especifica la máscara de subred asociada a esa red. `255.255.255.0` indica una red con 256 direcciones IP.                                        |
| `{ ... }`                    | Llaves que agrupan las opciones y parámetros aplicables a esa subred.                                                                             |
| `range`                      | Define el rango de direcciones IP que el servidor DHCP puede asignar dinámicamente a los clientes.                                                |
| `option domain-name-servers` | Especifica la(s) dirección(es) IP del/los servidor(es) DNS que se proporcionan al cliente. Aquí se usa `8.8.8.8` (DNS de Google).                 |
| `option subnet-mask`         | Vuelve a declarar la máscara de subred para los clientes que reciben la IP. Es necesario aunque ya se indique arriba.                             |
| `option routers`             | Define la dirección IP de la puerta de enlace predeterminada (gateway) que se entregará a los clientes.                                           |
| `option broadcast-address`   | Dirección de broadcast de la red, enviada a los clientes para facilitar la comunicación con todos los hosts.                                      |
| `default-lease-time`         | Tiempo en segundos por defecto durante el cual un cliente puede usar una IP si no especifica un tiempo concreto. Aquí, 600 segundos (10 minutos). |
| `max-lease-time`             | Tiempo máximo en segundos que se puede conceder para una concesión de IP. Aquí, 7200 segundos (2 horas).                                          |
