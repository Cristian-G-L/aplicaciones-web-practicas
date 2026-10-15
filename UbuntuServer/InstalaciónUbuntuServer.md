<div align="center">

# 🐧 Práctica: Instalación y Configuración de Ubuntu Server y Acceso SSH

<p>
  <b>Asignatura:</b> Aplicaciones Web · 2º SMR<br>
  <b>Objetivo:</b> Desplegar y configurar un servidor Ubuntu Server sin interfaz gráfica en VirtualBox, estructurando el almacenamiento, estableciendo una red con doble adaptador (NAT y Host-Only), configurando una IP estática mediante Netplan y habilitando el acceso remoto seguro por SSH.
</p>

</div>

---

<details>
<summary><b>📋 Tabla de Contenidos</b></summary>

- [1. Instalar un Servidor Ubuntu sin Interfaz Gráfica](#1-instalar-un-servidor-ubuntu-sin-interfaz-gráfica)
  - [1.1. Detalles del SO Escogido](#11-detalles-del-so-escogido)
  - [1.2. Configuración de VirtualBox](#12-configuración-de-virtualbox)
  - [1.3. Proceso de Instalación](#13-proceso-de-instalación)
- [2. Gestionando un Servidor por SSH](#2-gestionando-un-servidor-por-ssh)
  - [2.1. Qué es SSH (Secure Shell)](#21-qué-es-ssh-secure-shell)
  - [2.2. Configuración SSH y Explicación de las Interfaces de Red](#22-configuración-ssh-y-explicación-de-las-interfaces-de-red)

</details>

---

## 🖥️ 1. Instalar un Servidor Ubuntu sin Interfaz Gráfica

### 1.1. Detalles del SO Escogido
* **Sistema Operativo:** Ubuntu Server 24.04 LTS (Long Term Support).
* **Características:** Es una distribución de Linux diseñada específicamente para entornos de servidor que no incluye interfaz gráfica de usuario (GUI). Esto permite optimizar al máximo los recursos de hardware (ahorrando memoria RAM y ciclos de CPU) y gestionar todas las tareas de administración mediante comandos en la terminal.

### 1.2. Configuración de VirtualBox
Para crear la máquina virtual de forma óptima, aplicamos los siguientes parámetros en VirtualBox:
* **Nombre y tipo:** `SMR-AplicacionesWeb`, tipo *Linux*, versión *Ubuntu (64-bit)*.
* **Memoria RAM:** Asignación de entre 2048 MB (2 GB) y 4096 MB (4 GB).
* **Disco Duro Virtual:** Formato VDI, reservado dinámicamente con un tamaño recomendado de 20 a 25 GB.
* **Configuración de Red (Doble Adaptador):**  
  * **Adaptador 1 (NAT):** Proporciona al servidor acceso a Internet para descargar paquetes, dependencias y actualizaciones del sistema.  
  * **Adaptador 2 (Host-only / Solo-anfitrión):** Crea una red privada y aislada entre el equipo físico anfitrión y la máquina virtual (habitualmente utilizando la interfaz `vboxnet0`).

### 1.3. Proceso de Instalación
1. Arrancar la máquina virtual seleccionando la imagen ISO correspondiente (`ubuntu-24.04-live-server-amd64.iso`).
2. Seleccionar el idioma del asistente de instalación y la distribución del teclado (Español).
3. Elegir el tipo de instalación estándar de Ubuntu Server (evitando opciones minimalistas).
4. En la configuración de red inicial, dejar las interfaces en modo DHCP temporalmente.
5. Seleccionar el disco duro completo asignado para realizar el particionamiento automático del sistema.
6. En el perfil de usuario, introducir los datos correspondientes (nombre completo, nombre de usuario, contraseña robusta y el *hostname* o nombre del servidor).
7. <kbd>🔑 Paso Clave</kbd> En la pantalla de configuración *SSH Setup*, marcar la casilla de verificación **Install OpenSSH server** para permitir el acceso remoto desde el primer momento.
8. Omitir la instalación de paquetes Snap adicionales en el asistente, finalizar la instalación (*Done*) y reiniciar la máquina virtual.

---

## 🔒 2. Gestionando un Servidor por SSH

### 2.1. Qué es SSH (Secure Shell)
**SSH** es un protocolo de red seguro que permite a los administradores conectarse de forma remota a la terminal de un servidor a través de la red. Su propósito principal es gestionar el sistema a distancia de forma cifrada, evitando la necesidad de interactuar directamente con la pantalla física o la consola de VirtualBox.

### 2.2. Configuración SSH y Explicación de las Interfaces de Red
Una vez dentro del servidor tras la instalación, debemos configurar las tarjetas de red para asegurar una comunicación estable con nuestro equipo anfitrión.

1. **Identificar las interfaces de red:**  
   Utilizamos el comando `ip a` para listar las tarjetas de red disponibles en el sistema:  
   * `enp0s3`: Tarjeta conectada a la red NAT (proporciona salida a Internet mediante DHCP).  
   * `enp0s8`: Tarjeta conectada a la red Host-only (utilizada para la comunicación directa con el equipo anfitrión mediante IP estática).

2. **Fijar la IP estática mediante Netplan:**  
   Editamos el fichero de configuración de Netplan correspondiente ubicado en `/etc/netplan/` (por ejemplo, el archivo `.yaml` existente):
   ```bash
   sudo nano /etc/netplan/01-netcfg.yaml
   ```

   Ajustamos la estructura con los parámetros correspondientes para que quede configurado de la siguiente manera:
   ```yaml
   network:
     version: 2
     ethernets:
       enp0s3:
         dhcp4: true
       enp0s8:
         dhcp4: false
         addresses:
           - 192.168.56.10/24
   ```
   > ⚠️ **Nota:** Los nombres de las interfaces `enp0s3` y `enp0s8` deben adaptarse a los nombres reales devueltos por el comando `ip a` en tu servidor.

3. **Aplicar los cambios de red:**  
   Guardamos el archivo y aplicamos la configuración ejecutando:
   ```bash
   sudo netplan apply
   ```

4. **Conexión remota por SSH:**  
   Desde la terminal de nuestro equipo físico anfitrión, establecemos la conexión remota escribiendo:
   ```bash
   ssh tu_usuario@192.168.56.10
   ```

---
<div align="center">
  <sub>Práctica de Sistemas en Red y Aplicaciones Web · SMR</sub>
</div>