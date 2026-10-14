# Guía de Instalación y Configuración de Ubuntu Server

Una guía paso a paso, limpia y directa para instalar **Ubuntu Server** en VirtualBox, configurar la red con doble adaptador (NAT + Host-Only) y establecer una IP estática mediante **Netplan**.

## 🛠️ 1. Requisitos y Creación de la Máquina Virtual

1. **Descarga la ISO:** Entra en la [web oficial de Ubuntu](https://ubuntu.com/download/server) y descarga la imagen ISO de Ubuntu Server.

2. **Crea la MV en VirtualBox:**
   * Abre **VirtualBox** y haz clic en **Nueva**.
   * Ponle el nombre que quieras.
   * En **Imagen ISO**, selecciona la que descargaste.
   * **Muy importante:** Desmarca la casilla **"Instalación desatendida"**.

3. **Hardware recomendado:**
   * **RAM:** `2048 MB` (2 GB)
   * **CPU:** `2` núcleos
   * **Disco Duro:** `25 GB`
   * Clic en **Siguiente** y finaliza.

> **Nota sobre compatibilidad:** Si la ISO no arranca por un conflicto con VirtualBox, desinstala tu versión actual e instala una compatible desde la [web oficial de VirtualBox](https://www.virtualbox.org/). Luego repite este paso.

## 📥 2. Proceso de Instalación

Arranca la máquina virtual y sigue estos pasos en el asistente:

* **Idioma y Teclado:** Elige tu idioma (ej. **Español**) y la distribución del teclado.
* **Tipo de instalación:** Selecciona **Ubuntu Server (normal)** (evita la opción *minimized*).
* **Red:** Déjalo temporalmente en **DHCP** (lo configuraremos después).
* **Proxy:** Déjalo en blanco.
* **Almacenamiento:** Selecciona **usar el disco entero** (el disco virtual de 25 GB).
* **Usuario y Contraseña:** Introduce tu usuario y una contraseña fácil de recordar (ej. fecha de cumpleaños).
* **OpenSSH Server:** **¡Clave!** Marca la casilla de **OpenSSH** para poder conectarte por remoto desde tu PC anfitrión.
* **Snaps:** No marques ninguno por ahora.
* **Finalizar:** Selecciona **Done (Hecho)** y espera a que termine la instalación y se reinicie.

## 🌐 3. Configuración de Adaptadores de Red

Para tener Internet y conexión con tu PC al mismo tiempo, usaremos dos adaptadores:

### Adaptador 1: Salida a Internet
1. Apaga la máquina virtual.
2. Ve a **Configuración** > **Red** > **Adaptador 1**.
3. Ponlo en modo **Red NAT** (o NAT).

### Adaptador 2: Conexión con el Anfitrión
1. Arriba a la izquierda en VirtualBox, ve a **Archivo** > **Herramientas** > **Red**.
2. Haz clic en **Crear** para generar una red *Solo anfitrión* (Host-Only).
3. Configura su IP y **desactiva el DHCP**.
4. Vuelve a las propiedades de tu máquina virtual, ve al **Adaptador 2**, actívalo como **Adaptador sólo anfitrión** y asígnale la red creada.
5. Vuelve a encender la máquina virtual.

## ⚙️ 4. Configuración de Netplan (IP Estática)

Una vez dentro de Ubuntu con tu usuario y contraseña, configura la red estática:

1. **Localiza el archivo de Netplan:**
   ```bash
   ls /etc/netplan
   ```

2. **Edita el archivo `.yaml`** que te aparezca (ej. `01-netcfg.yaml`):
   ```bash
   sudo nano /etc/netplan/01-netcfg.yaml
   ```

3. **Modifica el contenido** para que quede estructurado de esta forma (respetando los espacios):
   ```yaml
   network:
     version: 2
     renderer: networkd
     ethernets:
       enp0s3:
         dhcp4: no
         addresses:
           - 192.168.56.10/24
         gateway4: 192.168.56.1
         nameservers:
           addresses:
             - 8.8.8.8
             - 1.1.1.1
       enp0s8:
         dhcp4: yes
   ```

   > *Nota: Adapta `enp0s3` y `enp0s8` a los nombres reales de tus interfaces de red.*

4. Guarda los cambios pulsando `Ctrl + O` (Enter para confirmar) y sal con `Ctrl + X`.

5. **Aplica los cambios de red:**
   ```bash
   sudo netplan apply
   ```

¡Listo! Tu servidor Ubuntu ya está instalado, configurado y preparado para funcionar.
