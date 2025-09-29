## Instalación de Servicio WordPress
En este README se explicará brevemente como realizar todos los pasos necesarios para realizar una puesta en marcha de un servicio WordPress.




## Índice

* [Descripción General](#Instalación-de-Servicio-WordPress)

* [Instalación de Dependencias](#Instalación-de-Dependencias)

* [Instalación de WordPress](#Instalación-de-WordPress)

* [Configurar Apache para WordPress](#descripción-del-proyecto)

* [Configurar la Base de Datos](#Estado-del-proyecto)

* [Configurar la conexión entre la BBDD y WordPress](#Características-de-la-aplicación-y-demostración)

* [Configurar el WordPress](#acceso-proyecto)

* [Realizar tu Primer Post!](#tecnologías-utilizadas)

* [Personas-Desarrolladores del Proyecto](#personas-desarrolladores)

* [Documentación](#conclusión)


## Instalación de Dependencias
Para instalar Apache y PHP se tienen que utilizar los siguientes comandos:
    
```bash
sudo apt update
sudo apt install apache2 \
                 ghostscript \
                 libapache2-mod-php \
                 mysql-server \
                 php \
                 php-bcmath \
                 php-curl \
                 php-imagick \
                 php-intl \
                 php-json \
                 php-mbstring \
                 php-mysql \
                 php-xml \
                 php-zip
```
Aquí una captura de pantalla de como debería verse la terminal mientras instalan las dependencias necesarias:

 ![Instalación de dependencias](imagenes/1.png)

## Instalación de WordPress
Crea el directorio de Instalación y descarga los archivos de **[WordPress.org](https://wordpress.org)**:

```bash
sudo mkdir -p /srv/www
sudo chown www-data: /srv/www
curl https://wordpress.org/latest.tar.gz | sudo -u www-data tar zx -C /srv/www
```

Captura de pantalla de como se ve el comando en la terminal:

 ![Instalación de WordPress](imagenes/2.png)

 ## Configurar Apache para WordPress

Creamos el sitio de Apache con el siguiente comando:

```bash
sudo nano /etc/apache2/sites-available/wordpress.conf
```

Dentro del editor inyectamos las siguientes lineas de codigo:

```bash
<VirtualHost *:80>
    DocumentRoot /srv/www/wordpress
    <Directory /srv/www/wordpress>
        Options FollowSymLinks
        AllowOverride Limit Options FileInfo
        DirectoryIndex index.php
        Require all granted
    </Directory>
    <Directory /srv/www/wordpress/wp-content>
        Options FollowSymLinks
        Require all granted
    </Directory>
</VirtualHost>
```

Guardamos con: Ctrl + O y cerramos con: Ctrl + X

Captura de pantalla de como se ve el editor de texto del terminal:

 ![Configuración de apache](imagenes/3.png)

Seguido modificaremos el archivo de configuración por defecto para agregar un Hostname al que el WordPress respondera sus llamadas. Este nombre de host debe estar mapeado a tu caja de alguna manera, por ejemplo, a través de DNS, o mediante ediciones en los sistemas del cliente. Hay que agregar ServerName como se ve el siguiente ejemplo:

```bash
<VirtualHost *:80>
    ServerName hostname.example.com
    ... # the rest of the VHost configuration
</VirtualHost>
```
Captura de pantalla agregando esta linea al archivo:

![Configuración de apache](imagenes/6.png)

Para finalizar la configuración del Apache, reiniciaremos el servicio para aplicar todos los cambios con el siguiente comando:

```bash
sudo service apache2 reload
```
Captura de pantalla aplicando el comando:

![Configuración de apache](imagenes/4.png)
