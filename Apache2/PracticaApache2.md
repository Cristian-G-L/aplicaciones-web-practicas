# 🌐 Práctica: Configuración de Servidor Web Apache2, VirtualHosts y Autenticación Básica

**Asignatura:** Aplicaciones Web · 2º SMR  
**Objetivo:** Desplegar y configurar un servidor web Apache2 en Ubuntu Server, implementando VirtualHosts basados en nombre y puertos, gestión de directorios protegidos por contraseña (Intranet) y la simulación de resolución DNS local.

---

## 📌 1. Qué es Apache2
Apache HTTP Server es uno de los servidores web más populares y utilizados a nivel mundial. Es un software libre que se encarga de procesar las peticiones HTTP realizadas por los navegadores de los clientes (usuarios) y devolverles los recursos solicitados, tales como páginas HTML, imágenes y otros ficheros estáticos o dinámicos.

---

## ⚙️ 2. Instalación de Apache2 y Utilidades
Para poner en marcha el servidor web en nuestro entorno Linux, actualizamos los repositorios e instalamos el paquete principal junto con las herramientas de utilidad (como `htpasswd`):

```bash
sudo apt update
sudo apt install apache2 apache2-utils -y
```

**Ficheros y directorios clave de Apache2:**
- `/etc/apache2/ports.conf`: Archivo donde se configuran los puertos de escucha del servidor (por defecto el puerto 80).   
- `/etc/apache2/sites-available/`: Directorio que almacena los ficheros de configuración de los sitios web disponibles, aunque no estén activados todavía.   
- `/etc/apache2/sites-enabled/`: Directorio que contiene enlaces simbólicos hacia los ficheros de *sites-available* que se encuentran activos y operativos en el servidor.   

---

## 📁 3. Creación de Directorios y Estructura Web
Para alojar los contenidos de nuestros sitios web, creamos la estructura de carpetas necesaria mediante el comando `mkdir` con la opción `-p` para subdirectorios:   

```bash
sudo mkdir -p /var/www/smr/web /var/www/smr/intranet
```

Una vez creadas, procedemos a inicializar los archivos HTML principales para cada sitio:   

- **Para la web pública:**
  ```bash
  cd /var/www/smr/web
  sudo touch index.html
  ```

- **Para la intranet privada:**
  ```bash
  cd /var/www/smr/intranet
  sudo touch intranet.html
  ```

---

## 🔑 4. Configuración del Directorio Protegido (Auth-Basic)
Para restringir el acceso a la intranet, creamos un archivo cifrado de credenciales de usuario utilizando la utilidad `htpasswd`:   

```bash
sudo htpasswd -c /etc/apache2/.htpasswd alumno
```
*(Se introducirá y confirmará la contraseña deseada para el usuario alumno)*

---

## 👂 5. Configuración de Puertos en Apache (`ports.conf`)
Para permitir que Apache escuche peticiones tanto por el puerto estándar HTTP como por un puerto alternativo para la intranet, modificamos el fichero de puertos:

```bash
sudo nano /etc/apache2/ports.conf
```

Aseguramos que incluya las siguientes líneas de escucha:

```apache
Listen 80
Listen 9999
```

---

## 📄 6. Configuración del VirtualHost (Por Nombre y Puerto)
Un VirtualHost es la funcionalidad de Apache que permite alojar y gestionar múltiples sitios web independientes dentro de un mismo servidor físico o virtual.

Editamos el archivo de configuración unificado para ambos sitios:   

```bash
sudo nano /etc/apache2/sites-available/smr.conf
```

Añadimos la siguiente estructura de configuración:   

```apache
<VirtualHost *:80>
    ServerName www.smr.com
    DocumentRoot /var/www/smr/web
</VirtualHost>

<VirtualHost *:9999>
    ServerName www.smr.com
    DocumentRoot /var/www/smr/intranet
    DirectoryIndex intranet.html
    
    <Directory /var/www/smr/intranet>
        AuthType Basic
        AuthName "Intranet SMR"
        AuthUserFile /etc/apache2/.htpasswd
        Require valid-user
    </Directory>
</VirtualHost>
```

---

## 🔄 7. Activación del Sitio y Gestión del Servicio
Para habilitar la configuración del VirtualHost, desactivar el sitio por defecto, comprobar errores de sintaxis y reiniciar el servicio, ejecutamos la siguiente secuencia de comandos:   

```bash
sudo a2ensite smr.conf
sudo a2dissite 000-default.conf
sudo apachectl configtest
sudo systemctl restart apache2
```

---

## 🌐 8. Modificación del Fichero hosts (Simulación DNS)
Como no disponemos de un servidor DNS dedicado en nuestra red local para resolver el dominio `www.smr.com`, debemos falsear la resolución de nombres directamente en el sistema operativo de la máquina cliente (en su archivo `hosts`):   

```bash
sudo nano /etc/hosts
```

Añadimos la línea que vincula la IP estática del servidor web con el nombre de dominio:   

```text
192.168.56.10   www.smr.com
```

---

## 🧪 9. Comprobación y Pruebas de Funcionamiento
Desde el navegador web de la máquina cliente conectada en la red local, realizamos las comprobaciones finales:   

1. **Sitio Web Público:** Al navegar a `http://www.smr.com`, el servidor responde sirviendo la página principal alojada en el puerto 80.   
2. **Intranet Protegida:** Al navegar a `http://www.smr.com:9999`, el servidor despliega una ventana emergente de autenticación HTTP Basic solicitando las credenciales (`alumno` y su respectiva contraseña) para conceder el acceso al contenido de la intranet.