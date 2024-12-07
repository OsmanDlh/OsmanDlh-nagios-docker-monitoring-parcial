# Monitoreo de Servicios con Nagios en Docker

Este proyecto implementa un sistema de monitoreo con Nagios, utilizando Docker para gestionar los contenedores de servicios como MySQL y NGINX. Permite monitorear el estado y la disponibilidad de estos servicios en tiempo real.

## Requisitos

- **Docker**: Para la gestión de contenedores.
- **Docker Compose**: Para la orquestación de múltiples contenedores.
- **Ubuntu 24.04**: Este proyecto está probado en Ubuntu 24.04, aunque debería funcionar en otras distribuciones.

## Instalación de Docker y Docker Compose

1. **Instalar Docker**:

   ```bash
   sudo apt update
   sudo apt install -y apt-transport-https ca-certificates curl software-properties-common
   curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
   sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
   sudo apt update
   sudo apt install -y docker-ce docker-ce-cli containerd.io
   ```

2. **Instalar Docker Compose**:
   ```bash
   sudo curl -L "https://github.com/docker/compose/releases/download/v2.24.0/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
   sudo chmod +x /usr/local/bin/docker-compose
   ```

## Configuración de Nagios

1. **Clonar el Repositorio**:

   ```bash
   git clone https://github.com/tuusuario/nagios-docker-monitoring.git
   cd nagios-docker-monitoring
   ```

2. **Crear Directorios Necesarios**:

   ```bash
   mkdir -p nagios/config/objects
   mkdir -p nagios/plugins
   mkdir -p data/mysql
   mkdir -p nginx/conf.d
   ```

3. **Configurar los Archivos de Nagios**:
   El repositorio ya incluye todos los archivos de configuración necesarios. Estos están ubicados en:

   - `nagios/config/nagios.cfg`
   - `nagios/config/objects/commands.cfg`
   - `nagios/config/objects/contacts.cfg`
   - `nagios/config/hosts.cfg`
   - `nagios/config/services.cfg`

4. **Iniciar los Contenedores**:
   Una vez que tengas todo configurado, inicia los contenedores de los servicios:
   ```bash
   sudo docker-compose up -d
   ```

## Acceso a la Interfaz Web de Nagios

- **URL de acceso**: [http://localhost:8080/nagios/](http://localhost:8080/nagios/)
- **Usuario**: nagiosadmin
- **Contraseña**: nagios123

## Servicios Monitoreados

### MySQL

- **Puerto**: 3307 (externo), 3306 (interno)
- **Credenciales**:
  - Usuario: testuser
  - Contraseña: testpass
  - Base de datos: testdb

### NGINX

- **Puerto**: 8081 (externo), 80 (interno)
- **Acceso Web**: [http://localhost:8081](http://localhost:8081)

## Verificación de los Servicios

### Verificar MySQL

Para probar MySQL desde el host:

```bash
mysql -h localhost -P 3307 -u testuser -p'testpass'
```
