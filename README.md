# osTicket-Installation-Guide-Ubuntu
Guía de instalación de osTicket Core, v1.17-rc4 en Ubuntu 22.04

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

##### Warning -> Crea un Snapshot

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


<kbd>![image](https://user-images.githubusercontent.com/20743678/190387299-3073b3fd-5a0a-4459-a70b-636a71235819.png)</kbd>

<kbd>![image](https://user-images.githubusercontent.com/20743678/190387369-244be5d6-7fa4-431d-b3a7-a24812f77573.png)</kbd>

<kbd>![image](https://user-images.githubusercontent.com/20743678/190387504-0bedf993-52c4-4373-a2e7-36666a559f74.png)</kbd>
