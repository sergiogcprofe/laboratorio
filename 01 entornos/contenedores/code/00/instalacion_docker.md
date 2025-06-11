# Actualizar el sistema
```
sudo apt update
sudo apt upgrade -y
```

# Instalar paquetes necesarios para la instalación
```
sudo apt install -y ca-certificates curl gnupg
```

# Añadir la clave oficial de docker al gestor de paquetes
```
sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | \
  sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
sudo chmod a+r /etc/apt/keyrings/docker.gpg
```

# Añadir el repositorio al gestor de paquetes
```
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] \
  https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

# Actualizar paquetes e instalar Docker
```
sudo apt update
sudo apt install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

# Dar permisos al usuario
```
sudo usermod -aG docker $USER
```

# Comprobar versiones
```
docker --version
docker compose version
```