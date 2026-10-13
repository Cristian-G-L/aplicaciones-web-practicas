Primero actualizamos los paquetes con sudo apt update y despues comprobamos que apache2 esta activo con el comando:systemctl is-active apache2 si te devuelve active es que apache esta activado
una vez comprobamos que ya esta activado procedemos a instalar mariadb con el siguiente comando: sudo apt install mariadb-server -y
comprobamos la version instalada con el comando:mariadb --version la version que deberiamos tener es: mariadb Ver 15.1 Distrib 10.11.14-MariaDB, for debian-linux-gnu (x86_64)
ahora comprobaremos que funciona con sudo systemctl status mariadb El primer comando debe mostrar active (running) (el servicio está funcionando ahora mismo) y systemctl is-enabled mariadb segundo enabled (arrancará solo cada vez que se encienda el equipo)
para entrar en la base de datos usaremos sudo mariadb y para salir escribiremos exit
