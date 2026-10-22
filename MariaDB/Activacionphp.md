Apartado 6. Instalación de PHP
WordPress está hecho en PHP. Instalamos PHP y las piezas que WordPress necesita:
sudo apt install php libapache2-mod-php php-mysql php-curl php-gd php-mbstring php-xml php-zip
php-intl -y
php -v
php -v debe mostrar PHP 8.3.x. Para qué sirve cada paquete:
Paquete Función
php El lenguaje PHP
libapache2-mod-php Permite a Apache ejecutar PHP
php-mysql Permite a PHP hablar con MariaDB (imprescindible)
php-curl Conexiones a otros servidores (actualizaciones, plugins)
php-gd Tratamiento de imágenes
php-mbstring Manejo de textos con tildes y caracteres especiales
php-xml Lectura y escritura de ficheros XML
php-zip Instalación y actualización de plugins y temas
php-intl Idiomas y formatos regionales
Reinicia Apache y comprueba que ha cargado PHP:
sudo systemctl restart apache2
Debes ver mpm_prefork_module y php_module.
Comprueba que PHP puede hablar con MariaDB:
php -m | grep -i mysql
Debe aparecer mysqli, mysqlnd y pdo_mysql. Son las piezas que usa WordPress para conectarse a la base
de datos.
Comprueba que Apache ejecuta PHP:
echo '<?php phpinfo();' | sudo tee /var/www/html/info.php

una vez que ya hemos creado el archivo de arriba, solo queda activarlo para que podamos entrar, para ello haremos lo siguiente: crearemos un archivo de configuracion dentro de apache, para eso entraremos a sites avaliable, y copiamos el archivo 000 default y le ponemos de nombre infophp.conf o el nombre que queramos, dentro del archivo lo unico que tendremos que pones es la ruta exacta del archivo que hemos creado antes, que esta en /var/www/html/info.php, una vez puesto eso guradamos y salimos y miramos que que servidores estan activos, si hay alguno lo desabilutamos con a2dissite y el nombre del sitio, una vez hecho eso habilitamos nuestro sitio web, con sudo a2ensite y el nombre en este caso info.php.conf y lo habilitamos, resetamos el server con sudo systemctl restart apache2 y ya podemos entrar
Abre http://IP_DE_TU_SERVIDOR/info.php en el navegador. Debe aparecer una página morada con la
versión de PHP.
