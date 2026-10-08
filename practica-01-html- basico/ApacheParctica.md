APLICACIONES WEB · 2º SMR

Objetivo: el objetivo de esta pracitca es conectarse mediante nombre a las dos webs que crearemos desde otra maquina, una sera publica y la otra nos pedira el usuario y contraseña

Paso 1 · Crear las carpetas y las páginas

para crear las carpetas y las paginas usaremos estos comandos: sudo mkdir -p /var/www/smr/web /var/www/smr/intranet
este comando nos creara las dos carpetas que necesitamos en la ruta que le hemos puesto,ahora una vez hayamos creado las dos carpetas entraremos mediante el comando cd y crearemos los archivos html,
en la carpeta web haremos un touch index.html y en la carpeta intranet haremos un touch intranet.html, estos archivos seran los que necesitaremos para modificar nuestra pagina web

Paso 2 · Crear el usuario de la intranet

para crear el usuario y ponerle una contraseña usaremos este comando: sudo htpasswd -c /etc/apache2/.htpasswd alumno
la contraseña pondremos la que queramos

Paso 3 · Decirle a Apache que escuche en el puerto 9999

para decirle que escuche esos dos puertos hay que entrar en el archivo ports.conf mediante este comando: sudo nano /etc/apache2/ports.conf
una vez dentro le pondremos los dos Listen y el puerto que queramos que escuchen en nuestro caso el 80 y el 9999: Listen 80 Listen 9999

Paso 4 · Crear el virtualhost

Ahora le indicaremos a apache dos que el fichero smr.conf lo queremos modificar para que nuestra web funcione, para hacer esto utilizaremops este comando: sudo nano /etc/apache2/sites -available/smr.conf 

una vez dentro tenemos dos maneras de hacerlo, una es creando un fichero de configuracion para cada web o podemos usar un solo fichero para las dos webs, en este caso usaremos un fichero para las dos webs
la configuracion que tendriamos que poner se veria asi:
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

Paso 5 · Activar el sitio y reiniciar Apache


para activar el sitio y reiuniciar apache lo haremos con esta serie de comandos: sudo a2ensite smr.conf
sudo a2dissite 000-default.conf
sudo apachectl configtest
sudo systemctl restart apache2

Paso 6 · Comprobar que funciona

ahora para comprobar que todo funciona entraremos desde otra maquina virtual y en el buscador buscaremos nuestras webs, la primera lo haremos con http://www.smr.com y nos deberia de salir la web del puerto 80, ahora si buscamos http://www.smr.com:9999 nos deberia de salir la web de intranet, que nos pedira el usuario y la contraseña para entrar, y eso seria todo



