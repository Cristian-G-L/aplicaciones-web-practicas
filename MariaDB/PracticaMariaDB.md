# 🐬 Guía de Instalación: MariaDB

---

## 1. Preparación del sistema

Primero actualizamos la lista de paquetes y nos aseguramos de que Apache sigue activo:

```bash
sudo apt update
systemctl is-active apache2
```

> 💡 **Nota:** Si devuelve `active`, todo va bien.

---

## 2. Instalación de MariaDB

Instalamos el servidor de bases de datos con el siguiente comando:

```bash
sudo apt install mariadb-server -y
```

Comprobamos que se haya instalado la versión correcta:

```bash
mariadb --version
```

<details open>
<summary><b>❓ Pregunta: ¿Qué diferencia hay entre el paquete <code>mariadb-server</code> y el paquete <code>mariadb-client</code>? ¿Cuál de los dos has instalado?</b></summary>

<br>

* **`mariadb-server`**: Instala el motor completo para gestionar las bases de datos localmente (incluyendo las herramientas de cliente necesarias).
* **`mariadb-client`**: Solo instala las herramientas de línea de comandos para conectarse a un servidor MariaDB externo o remoto, sin levantar el servicio en la máquina local.

📌 **Respuesta:** Nosotros hemos instalado **`mariadb-server`**.
</details>

---

## 3. Comprobación del funcionamiento

Revisamos que el servicio esté corriendo y configurado para arrancar automáticamente al encender la máquina:

```bash
sudo systemctl status mariadb
systemctl is-enabled mariadb
```

> ℹ️ *Para salir de la pantalla de estado interactiva, pulsa la tecla <kbd>q</kbd>.*

Para probar que responde internamente, accedemos a la consola de la base de datos:

```bash
sudo mariadb
```

*(Para salir escribimos `exit` y pulsamos <kbd>Enter</kbd>).*

<details open>
<summary><b>❓ Pregunta: ¿Qué diferencia hay entre <code>active (running)</code> y <code>enabled</code>? ¿Qué pasaría con la web de WordPress si MariaDB estuviera <code>active</code> pero no <code>enabled</code> y se reiniciara el servidor?</b></summary>

<br>

* **`active (running)`**: Significa que el servicio está funcionando en ejecución en este preciso instante.
* **`enabled`**: Indica que el servicio está programado para arrancarse de forma automática cada vez que se encienda o reinicie el equipo.

📌 **Respuesta:** Si estuviera en estado *active* pero no *enabled*, al reiniciar el servidor por cualquier motivo (un mantenimiento, apagón, etc.), el servicio de MariaDB se quedaría detenido y la web de WordPress **caería mostrando un error de conexión con la base de datos** hasta que alguien iniciara el servicio manualmente.
</details>

---

## 4. Gestión del servicio

Comandos básicos para la administración del día a día:

| Comando | Descripción |
| :--- | :--- |
| `sudo systemctl start mariadb` | Arranca el servicio |
| `sudo systemctl stop mariadb` | Detiene el servicio |
| `sudo systemctl restart mariadb` | Reinicia el servicio |
| `sudo systemctl status mariadb` | Muestra su estado actual detallado |
| `sudo systemctl enable mariadb` | Configura el servicio para arrancar al iniciar el sistema |

---

## 5. Simulación de errores (¿Qué pasa si se para?)

Si paramos el servicio a propósito:

```bash
sudo systemctl stop mariadb
```

E intentamos acceder a la consola (`sudo mariadb`), nos devolverá el siguiente fallo porque el socket local no está disponible:

```text
ERROR 2002 (HY000): Can't connect to local server through socket...
```

Para solucionar el fallo y volver a la normalidad, simplemente arrancamos de nuevo el servicio:

```bash
sudo systemctl start mariadb
```

<details open>
<summary><b>❓ Pregunta: Si WordPress no pudiera conectar con la base de datos, ¿qué dos comandos de este apartado usarías para saber si el problema es que MariaDB está parado?</b></summary>

<br>

📌 **Respuesta:** Usaríamos los siguientes comandos:
1. `systemctl is-active mariadb` — Para comprobar de forma rápida si el servicio está en un estado distinto a `active`.
2. `sudo systemctl status mariadb` — Para ver el informe completo del estado, logs recientes y verificar exactamente por qué está detenido o fallando.
</details>

---
<sub>Guía de administración de sistemas y bases de datos.</sub>