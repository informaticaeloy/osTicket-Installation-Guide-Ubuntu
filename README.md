# osTicket-Installation-Guide-Ubuntu
Guía de instalación de osTicket Core, v1.17-rc4 en Ubuntu 22.04

### 0.666 CONCLUSIONES FINALES

Antes de que llegues al final del proceso de instalación, te comento aquí arriba mis impresiones trabajando con osTicket:

Es muy sencillo de instalar y de configurar para una primera toma de contacto. Es intuitivo y completo, ágil y completo, pero necesitaba poder integrarle un inventario de equipos que asociar a los tickets, algo así como este plugin:

(https://github.com/flotwig/osTicket-Equipment)

Este plugin y otros similares que he probado no son compatibles con la versión 1.17-rc4, por lo que una vez instalados y activados el software deja de funcionar. Al ser proyectos discontinuados desde 2014, no invierto más tiempo en pulir, por lo que opto a buscar alternativas como GLPI.

Si necesitas un sistema de tickets completo y ágil pero sin inventario de hardware y software, osTicket es una muy buena opción. A partir de aquí, prueba a instalarlo y saca tus propias conclusiones.

### 0.  PRERREQUISITOS

To install osTicket, your web server must have PHP 8.0 and MySQL 5.0 (or better) installed. If you are unsure whether your server meets these requirements, please check with your host or webmaster before proceeding with the installation.

You will need one MySQL database with valid user, password and hostname handy during installation. MySQL user must have FULL privileges on the database. If you are unsure whether you have these details or if the user has sufficient permissions, please consult your host or database admin before proceeding.

### 1. INSTALACIÓN DE APACHE

```shell
apt-get install apache2
```

<kbd>![image](https://user-images.githubusercontent.com/20743678/190367570-093d6ac2-c0b4-4a21-b824-cae5bb0f524e.png)</kbd>

En un navegador, accedemos a la URL de nuestro máquina virtual y comprobamos si funciona:

<kbd>![image](https://user-images.githubusercontent.com/20743678/190367841-1938c201-9728-45b7-85e6-ec12a9243a86.png)</kbd>

### 2. INSTALACIÓN DE PHP 8

```shell
sudo apt install ca-certificates apt-transport-https software-properties-common
```

<kbd>![image](https://user-images.githubusercontent.com/20743678/190368199-ff183676-8553-48b7-a5f1-d292dcc2c886.png)</kbd>

```shell
sudo add-apt-repository ppa:ondrej/php
```

<kbd>![image](https://user-images.githubusercontent.com/20743678/190368451-23265c03-e5ef-4f68-b0bf-31f9cd753b5d.png)</kbd>


```shell
sudo apt install php8.0 libapache2-mod-php8.0
```

<kbd>![image](https://user-images.githubusercontent.com/20743678/190368692-aac9c322-5e4f-49cc-8958-a81dd3dacc53.png)</kbd>


```shell
sudo systemctl restart apache2
```

```shell
php -v
```

<kbd>![image](https://user-images.githubusercontent.com/20743678/190368901-e0382902-a13d-4cd1-b787-579ea2a61183.png)</kbd>

#### 2.1 INSTALACIÓN DE LA EXTENSIÓN MYSQLI PARA PHP 8

```shell
sudo apt install php8.0-mysqli 
```

<kbd>![image](https://user-images.githubusercontent.com/20743678/190369709-a8a97c4f-1566-4406-b1f3-9002e1756e64.png)</kbd>

Para comprobar que funciona, creamos un fichero en /var/www/html llamado info.php por ejemplo

```shell
nano /var/www/html/info.php
```

y escribimos estas líneas:

 ```shell
<?php
phpinfo();
?>
```

<kbd>![image](https://user-images.githubusercontent.com/20743678/190370162-be39a198-143b-4dce-9141-5c5c39810069.png)</kbd>

Desde nuestro navegador, visitamos la URL de nuestro servidor Apache y añadimos el nombre del fichero que hemos creado:

```shell
http://192.168.46.214/info.php
```

Si todo está correcto hasta ahora, veremos algo similar a esto:

<kbd>![image](https://user-images.githubusercontent.com/20743678/190371854-5b08c8a9-bea8-4078-a629-b43c2156a28b.png)</kbd>

#### Warning - :skull: Haz un Snapshot :eyes:

### 3. INSTALACIÓN DE MYSQL DATABASE

```shell
sudo apt install mysql-server
```

<kbd>![image](https://user-images.githubusercontent.com/20743678/190381304-84dea3a9-69d8-4e68-8cda-6aca37be3508.png)</kbd>

#### 3.1 CONFIGURACIÓN DE MYSQL

```shell
sudo mysql_secure_installation
```

<kbd>![image](https://user-images.githubusercontent.com/20743678/190381413-b33bebe1-d0a4-474a-97ac-a24967ba3693.png)</kbd>

Si nos aparece este error:

<kbd>![image](https://user-images.githubusercontent.com/20743678/190382549-7923d3a9-928b-4ba9-ac7b-1f673b9f3916.png)</kbd>

```shell
mysql
```

```shell
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password by 'mynewpassword';
```

<kbd>![image](https://user-images.githubusercontent.com/20743678/190383805-69981a35-ec36-4a59-97b9-06e54cfcea03.png)</kbd>

Salimos con exit:

```shell
exit
```

Y probamos de nuevo el comando y seguimos el asistente:

```shell
sudo mysql_secure_installation
```

<kbd>![image](https://user-images.githubusercontent.com/20743678/190384498-6d7eaec6-cec5-4b84-8c30-7b9ea87c0510.png)</kbd>

Probamos si MySQL funciona:

```shell
systemctl status mysql.service
```

<kbd>![image](https://user-images.githubusercontent.com/20743678/190384728-a043ed3b-e1ab-4614-a8a2-96c50c9c8618.png)</kbd>

#### Warning - :skull: Haz un Snapshot :eyes:

### 4. DESCARGA E INSTALACIÓN DE OSTICKET

Accedemos a la web de descarga de osTicket:

(https://osticket.com/download)

Seleccionamos la versión deseada, en este caso

> osTicket Core, v1.17-rc4 - Released September 12, 2022 

<kbd> ![image](https://user-images.githubusercontent.com/20743678/190385174-e442b726-d21a-4b0e-91dd-bac8e29071b8.png) </kbd>

Podemos añadir los paquetes de idiomas que deseemos:

<kbd>![image](https://user-images.githubusercontent.com/20743678/190387299-3073b3fd-5a0a-4459-a70b-636a71235819.png)</kbd>

Podemos añadir los plugins que queramos:

<kbd>![image](https://user-images.githubusercontent.com/20743678/190387369-244be5d6-7fa4-431d-b3a7-a24812f77573.png)</kbd>

Y comeinza la descarga del fichero:

<kbd>![image](https://user-images.githubusercontent.com/20743678/190387504-0bedf993-52c4-4373-a2e7-36666a559f74.png)</kbd>

Abrimos el fichero con nuestro software de compresión y vemos que hay varios ficheros .phar que son los paquetes de idiomas y los plugins. Hemos de abrir el fichero osTicket-v1.17-rc4.zip y descomprimir el contenido de la carpeta upload en /var/html

<kbd>![image](https://user-images.githubusercontent.com/20743678/190391439-01dfea57-f11b-405f-93b7-a6da290adee2.png)</kbd>

<kbd>![image](https://user-images.githubusercontent.com/20743678/190391560-72652fd2-b35f-4a98-842a-449454fdcb59.png)</kbd>

Si no nos deja hacerlo directamente por permisos, creamos una carpeta en el escritorio, por ejemplo, descomprimimos en ella y luego desde el terminal copiamos con el comando:

```shell
sudo cp /home/usuario/Escritorio/upload/* /var/www/html/ -r
```

<kbd>![image](https://user-images.githubusercontent.com/20743678/190392617-efc737d7-b92f-4e0c-b02b-279a3357bb80.png)</kbd>

Y obtendremnos el siguiente resultado:

<kbd>![image](https://user-images.githubusercontent.com/20743678/190392752-20389d7c-8dd8-4d0a-a936-25cd43743232.png)</kbd>

Ahora podemos acceder a la URL de nuestro servidor y en la carpeta "setup", tendremos el instalador, que nos protestará de todos los errores que hemos de solucionar:

```shell
http://192.168.46.214/setup/
```

<kbd>![image](https://user-images.githubusercontent.com/20743678/190393090-cc78e389-330c-45d4-bde8-1a6c02bf57eb.png)</kbd>

En mi caso falta de activar la extensión MySQLi para PHP.

Editamos el fichero /etc/php/8.0/apache2/php.ini y sobre la línea 935 aproximan¡damente, descomentamos la que dice:

> extension=mysqli

<kbd>![image](https://user-images.githubusercontent.com/20743678/190394546-c57d11e8-be59-43ca-824f-feee0387171a.png)</kbd>

Reiniciamos el servicio apache con:

```shell
systemctl restart apache2
```

y comprobamos si arranca con :

```shell
systemctl status apache2
```

<kbd>![image](https://user-images.githubusercontent.com/20743678/190394891-a1e292b0-6770-4c60-a3c5-ff60acccd221.png)</kbd>

Actualizamos nuestro navegador y comprobamos si se ha solucionado. Para asegurarnos, cerramos el navegador y recargamos la página en modo incógnito para borrar caché:

<kbd>![image](https://user-images.githubusercontent.com/20743678/190395250-dcdc1273-a604-481a-bf6e-bcc1d0b455df.png)</kbd>

Vemos que los requisitos requeridos ya están OK, pero los recomendados no. Podemos continuar sin ellos, pero hacer esto no me deja dormir por las noches, así que antes de que muera algún gatito vamos a solucionarlo.

#### Warning - :skull: Haz un Snapshot :eyes:

Volvemos a editar el fichero /etc/php/8.0/apache2/php.ini y vamos descomentando las extensiones que tenemos en fallo:

<kbd>![image](https://user-images.githubusercontent.com/20743678/190577859-afe778a4-257d-4827-a4b3-d31da7656538.png)</kbd>

Luego vamos instalando las extensiones:

```shell
sudo apt install php8.0-gd
```

```shell
sudo apt install php8.0-imap
```

```shell
sudo apt install php8.0-mbstring
```

```shell
sudo apt install php8.0-intl
```

```shell
sudo apt install php8.0-apcu
```

<kbd>![image](https://user-images.githubusercontent.com/20743678/190579288-91438029-f793-48cc-8e9f-af0f2e466a89.png)</kbd>

Bien, esto pinta bien :muscle:

Siguente ventana de error:

<kbd>![image](https://user-images.githubusercontent.com/20743678/190580078-151e7f4e-d92a-4218-a3b0-3feee8c783ac.png)</kbd>

En la ruta /var/www/html/include copiamos el fichero ost-sampleconfig.php en uno nuevo llamado ost-config.php

```shell
cp ost-sampleconfig.php ost-config.php
```

Le asignamos los permisos necesarios:

```shell
chmod 0666 ost-config.php
```

Los comprobamos:

```shell
ls -la ost-config.php 
```

Y nos muestra algo parecido a esto:

> root@ubuntu:/var/www/html/include# ls -la ost-config.php 
> 
> -rw-rw-rw- 1 root root 5753 sep 16 09:21 ost-config.php

Y podemos continuar con la instalación:

<kbd>![image](https://user-images.githubusercontent.com/20743678/190581185-f2be51b7-cd4b-42d8-8f15-307b3c8300d5.png)</kbd>

#### Warning - :skull: Haz un Snapshot :eyes:

En esta ventana inicial no nos deja seleccionar otro idioma distinto al inglés. Para ñadir el español y francés que hemos descargado antes, descomprimimos los ficheros es_EN.phar y fr.phar en la ruta siguiente:

> /var/www/html/include/i18n

Debería quedarnos algo así:

<kbd>![image](https://user-images.githubusercontent.com/20743678/190591585-0edd5817-4ecb-43e6-a88e-a1ddb36ccee3.png)</kbd>

Ahora, refrescamos la ventana del navegador y ya nos deja seleccionar el español:

<kbd>![image](https://user-images.githubusercontent.com/20743678/190592913-e783082b-0826-4949-b27b-3b0b015f14da.png)</kbd>

<kbd>![image](https://user-images.githubusercontent.com/20743678/190597174-560239e0-25a3-4c88-a215-397fe693732f.png)</kbd>

Una vez terminado el proceso de instalación, no ofrece unas tareas a realizar para incrementar la seguridad y los enlaces a la herramienta:

<kbd>![image](https://user-images.githubusercontent.com/20743678/190597734-60659f83-1f97-4951-a51a-a3eafbbd61c7.png)</kbd>

Así pues, en la ruta:

> /var/www/html/include

Ejecutamos el siguiente comando:

```shell
chmod 0644 ost-config.php 
```

y comprobamos los permisos 

```shell
ls -la ost-config.php 
```

<kbd>![image](https://user-images.githubusercontent.com/20743678/190598373-bf778159-cb64-4b92-9cac-d12764098282.png)</kbd>

Accedemos desde un navegador a la URL de nuestro servidor y ya tenemos accedo al panel de control. No muestra un aviso de seguridad, que nos recomienda borrar la carpeta "setup". La borramos y ya tendríamos todo instalado y listo para trabajar con osTicket.

<kbd>![image](https://user-images.githubusercontent.com/20743678/190599015-d087fc3f-cfe1-4a17-945b-3c5681d9e1cc.png)</kbd>

Es importante borrar la carpeta setup para evitar tener una brecha de seguridad.

```shell
rm -r setup
```


