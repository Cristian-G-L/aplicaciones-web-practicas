# Instalacion Ubuntu Server

Primero descargamos la ISO desde la pagina web oficial 
una vez la tengamos ya instalada abrimos el virtualbox
una vez dentro en el menu principal seleccionamos nueva y le ponemos el nombre que queramos
en iso image ponemos la iso q nos hemos descargado ademas desmarcaremos el recuadro que dice instalacion desatendida
acontinuacion de memoria base ponemos 2048mb, 2 cpu y 25gb del espacio del disco y le damos a siguiente, con esto la maquina ya deberia de estar instalada

![Error VirtualBox](./home/vespre/Imatges/errorvirtualbox.png)

El error que nos sale es porque la version que tenemos del virtualbox no es compatible con la iso, para solucionarlo desinstalaremos el virtual box que tenemos y nos instalaremos una version compatible con la iso desde la pagina oficial de virtualbox,una vez ya instalado procedemos como lo hemos dicho antes



acontinuacion procedemos con la instalacion de Ubuntu server, nos preguntara por el idioma, ponemos español o el idioma que querais, lo mismo para el idioma del teclado, luego nos preguntara por el tipo de instalacion ahi marcamos la opcion ubuntu server normal, la opcion que pone ubuntu server (minimized) no, en la configuracion de red marcamos la opcion de DHCP ya que mas adelante lo configuraremos pero de momento no nos interesa, ahora nos pregunta por el proxy pero esa pestaña la dejaremos en blanco,acontinuacion configuraremos el almacenamiento que le daremos a usar el disco entero (el disco virtual que le hemos asigando a la maquina al principio) Ahora pondremos el nombre de usuario de la maquina y su respectiva contraseña, (es importante poner una contraseña que te acuerdes por ejempolo la fecha de cumpleaños), ahora viene un paso muy importante, nos pregunta si queremos activar la opcion de open SHH marcaremos que si, ya que queremos poder conectarnos a nuestra maquina virtual desde el pc anfitrion por ejemplo y para eso necesitamos el SSH, las snaps no marcaremos ninguna ya que instalaremos nosotros mismos las que queramos mas adelante para entender su funcionamiento, ahora solo queda darle a hecho y a esperar a que se instale.

EXPLICAR ADAPTADORES Y NETPLAN CONFIGURACION

para conectar las dos maquinas y que tengan salida a internet, vamos a la maquina virtual que hemos usado y le damos a configuracion, ahora nos vamos al apartado de red y en adaptadores el primer adaptador lo ponemos en red NAT y el adaptador 2 no nos dejara, por lo que arriba a la izquierda nos saldra una opcion que se llama archivo luego le damos a herramientas y a red, una vez dentro le damos a crear y se nos creara una red anfitrion, ahi configuramos nuestra ip, la que queriamos poner y desactivamos el DHCP una vez hecho volvemos a la pestaña de los adaptadores y en el 2 adaptador lo ponemos como solo anfitrion e iniciamos la maquina, una vez dentro hay que configurar el netplan que es para poner la ip en la maquina virtual, para entrar en el archivo netplan ponemos este coomando: ls /etc/netplan y sudo nano /etc/netplan/el archivo que nos ha salido con el ls x.ymal y entramos, acontinuacion hay que ponerlo de una forma concreta como la de esta imagen: "imagen de la configuracion del netplan"





