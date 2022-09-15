# osTicket-Installation-Guide-Ubuntu
Guía de instalación de osTicket Core, v1.17-rc4 en Ubuntu 22.04

### 0.  PRERREQUISITOS

To install osTicket, your web server must have PHP 8.0 and MySQL 5.0 (or better) installed. If you are unsure whether your server meets these requirements, please check with your host or webmaster before proceeding with the installation.

You will need one MySQL database with valid user, password and hostname handy during installation. MySQL user must have FULL privileges on the database. If you are unsure whether you have these details or if the user has sufficient permissions, please consult your host or database admin before proceeding.

### 1. INSTALACIÓN DE APACHE

```shell
apt-get install apache2
```

![image](https://user-images.githubusercontent.com/20743678/190367570-093d6ac2-c0b4-4a21-b824-cae5bb0f524e.png)
