# Raspberry Datalogger ModBus

## Desafio: 
Levantar un servidor LAMP para un Datalogger ModBus con cliente TCP 

###### Hadware utilizado para este proyecto:

 - **Raspberry pi 3 b+:** 
 - *Ficha tecnica:*
 - *CPU + GPU: Broadcom BCM2837B0, Cortex-A53 (ARMv8) 64-bit SoC @ 1.4GHz.*
 - *RAM: 1GB LPDDR2 SDRAM.*
 - *Wi-Fi + Bluetooth: 2.4GHz y 5GHz IEEE 802.11.b/g/n/ac, Bluetooth 4.2, BLE.*
 - *Ethernet: Gigabit Ethernet sobre USB 2.0 (300 Mbps).*
 - *GPIO de 40 pines.*
 - *HDMI.*
 - *4 puertos USB 2.0.*
 - *Puerto CSI para conectar una cámara.*
 - *Puerto DSI para conectar una pantalla táctil.*
 - *Salida de audio estéreo y vídeo compuesto.*
 - *Micro-SD.*
 - *Power-over-Ethernet (PoE).*
 
 ![raspi](https://user-images.githubusercontent.com/68520248/89323116-41a23300-d653-11ea-83a9-f71f60ba87de.png)

 - **Tarjeta microSD 16GB clase10.**
 - **Teclado, mouse, Monitor con entrada HDMI.**
 - **Notebook para bajar y quemar la imagen ISO a la microSD.**
 - **Adaptador microSD a USB.**

###### Software utilizado en el proyecto:
  - [PuTTy](https://www.putty.org/)
  - [VNC viewer](https://www.realvnc.com/es/connect/download/viewer/)
  - [balenaEtcher](https://www.balena.io/etcher/)
  - [Raspberrry Pi 32-bits with Desktop](https://downloads.raspberrypi.org/raspios_full_armhf_latest)
  
###### **Instalacion incial paso a paso:**
1. Descargar SO que se utilizara en este caso se ocupara Raspberry Pi OS 32-bits with Desktop [Click Descarga directa](https://downloads.raspberrypi.org/raspios_full_armhf_latest) 

2. Descargar la ISO

3. Descomprimir el archivo .rar

4. Quemar la ISO en la SD con tu quemador favorito, yo use balenaEtcher

![1](https://user-images.githubusercontent.com/68520248/89311342-db61e400-d643-11ea-9bed-35979164ce23.PNG)

5. Conectar la Raspberry a Internet mediante WLAN o Ethernet y ver la IP en la terminal con el comando
```
if-config
```
6. Habilitar conexion con SSH y VNC viewer

![2](https://user-images.githubusercontent.com/68520248/89311346-dc931100-d643-11ea-9719-284e9eb0145b.PNG)

![3](https://user-images.githubusercontent.com/68520248/89311349-ddc43e00-d643-11ea-86c4-8216bca9ef47.PNG)

7. Establecer IP fija

![4](https://user-images.githubusercontent.com/68520248/89312130-e0736300-d644-11ea-864d-2add08fd2bb9.PNG)

![5](https://user-images.githubusercontent.com/68520248/89312133-e1a49000-d644-11ea-9fdd-f164cdc9ea67.PNG)

8. Conectarce a VNC viewer

![6](https://user-images.githubusercontent.com/68520248/89312665-8757ff00-d645-11ea-8df9-15a08f4a9806.png)

![7](https://user-images.githubusercontent.com/68520248/89312675-8a52ef80-d645-11ea-8ae7-af2397d6b38a.PNG)

9. Expander SD en raspi-config

![8](https://user-images.githubusercontent.com/68520248/89313137-1fee7f00-d646-11ea-852a-6d32c377bec7.PNG)

![9](https://user-images.githubusercontent.com/68520248/89313142-211fac00-d646-11ea-920a-f871478a4869.PNG)

![10](https://user-images.githubusercontent.com/68520248/89313144-21b84280-d646-11ea-8b60-166efafceb5c.PNG)

**Una vez que terminemos estos pasos ya estamos listo para empezar a montar nuestro servidor LAMP.**

Comenzaremos actualizando nuestra Raspberrry, para esto abriremos nuestra terminal o PuTTy y ejecutaremos los siguientes comandos:
```
sudo apt update && sudo apt upgrade -y
```
![11](https://user-images.githubusercontent.com/68520248/89315062-6644dd80-d648-11ea-891a-914350e4178f.PNG)

Actulizada nuestra Raspi, instalaremos apache
```
sudo apt install apache2
```
![12](https://user-images.githubusercontent.com/68520248/89315068-66dd7400-d648-11ea-9333-0c3ad48c3a92.PNG)

Ya finalizada la instalacion tendremos que dar permisos a el directorio
```
sudo a2enmod rewrite
sudo systemctl restart apache2
sudo chown -R pi:www-data /var/www/html/
sudo chmod -R 770 /var/www/html/
```

Y tendremos que modificar el .conf de apache
```
sudo nano /etc/apache2/apache2.conf
```
![13](https://user-images.githubusercontent.com/68520248/89315521-f2ef9b80-d648-11ea-9dad-25a1cf657eda.PNG)

Buscamos la siguiente linea con Ctrl+W 
```
/var/
```
Y remplazamos en <Directory /> la opcion AllowOverride a All

![14](https://user-images.githubusercontent.com/68520248/89315528-f420c880-d648-11ea-86f0-fb10ff3698c0.PNG)

Por ultimo guardamos el edit con
```
Crtl + O
```
Y Cerramos el archivo con
```
Ctrl + X
```

Realizados todos estos pasos procederemos a instalar la libreria libapache2-mod-php junto con php
```
sudo apt install libapache2-mod-php
```
![15](https://user-images.githubusercontent.com/68520248/89317434-567ac880-d64b-11ea-9f77-57e7f5ace9c5.PNG)

Reiniciamos el servicio apache
```
sudo service apache2 restart
```

Terminando esto ya tendriamos apache2 y php instalado funcionando con nuestra libreria libapache.

Para poder comprobar si php se instalo de manera correcta haremos la siguiente prueba:
1. creamos un archivo php con el comando
```
sudo nano /var/www/html/pruebaphp.php
```
2. le añadimos el siguiente texto:
```
<?php phpinfo(); ?>
```
Si todo funciono, abriremos nuestro navegador y en la url colocamos el IP de nuestra Raspberry mas /pruebaphp.php

![16](https://user-images.githubusercontent.com/68520248/89318561-f1c06d80-d64c-11ea-82b6-89d37229d65d.PNG)

Se abrira una ventana con la info de la version de php que se instalo

![17](https://user-images.githubusercontent.com/68520248/89318563-f2f19a80-d64c-11ea-97e8-464e290ccea9.PNG)

Ya con php y Apache instalaremos nuestra base de datos, en este proyecto se utilizo MariaDB, por su optimizacion y soporte brindado por su comunidad,
ocuparemos el comando
```
sudo apt-get install mariadb-server
```
![18](https://user-images.githubusercontent.com/68520248/89319165-bffbd680-d64d-11ea-85ce-8d38034d5b25.PNG)

Terminada la instalacion eliminamos la configuracion por defecto y problemas de seguridad, con el siguiente script
```
sudo mysql_secure_installation
```
Nos dira que ingresemos la contraseña de root, como nostros aun no se la asignabamos apretaremos Enter, echo esto podremos generar nuestra nueva contraseña

![19](https://user-images.githubusercontent.com/68520248/89319690-7790e880-d64e-11ea-9d9c-8f71d3c5fedb.PNG)

Finalizado esto nos saldran mas opciones, aca les dejo una foto de como lo deben hacer

![20](https://user-images.githubusercontent.com/68520248/89319691-78297f00-d64e-11ea-9f6b-400e1ca1a9bf.PNG)

Continuando con la instalacion de MariaDB tendremos que crear nustro usuario que ocuparemos mas adelante para ingresar a phpmyadmin o de nuestra terminal sin problemas, para esto volvemos a nuestra terminal o PuTTy e ingrasamos con el comando
```
sudo mysql -u root
```

![21](https://user-images.githubusercontent.com/68520248/89321683-4239ca00-d651-11ea-9895-241531f17195.PNG)

Posteriormente debemos de generar un nuevo Usuario, Para esto ejecutamos las siguiente sentencia
```
CREATE USER 'usuario'@'localhost' IDENTIFIED BY 'contraseña';
```
Y le asignamos permisos
```
GRANT ALL PRIVILEGES ON *.* TO 'usuario'@'localhost';
```
Una vez hayamos finalizado con los permisos, el último paso será refrescarlos
```
FLUSH PRIVILEGES;
```
Para salir de MariaDB podemos apretar Crtl + C o \q

![22](https://user-images.githubusercontent.com/68520248/89321686-42d26080-d651-11ea-99d9-a61b59f6f165.PNG)

Ya como ultimo paso instalamos phpmyadmin
```
sudo apt-get install phpmyadmin
```
![23](https://user-images.githubusercontent.com/68520248/89324311-191b3880-d655-11ea-8f7c-b44dfd7f3174.PNG)

En el proceso de intalacion nos aparecera un recuadro donde tendremos que seleccionar nuestro motor, en nuestro caso apache2,
lo seleccionamos con la tecla espacio, tabulamos y apretamos enter

![24](https://user-images.githubusercontent.com/68520248/89324314-19b3cf00-d655-11ea-8051-3baf06235bfc.PNG)

luego nos preguntara si queremos crear la base de datos predeterminada de phpmyadmin, si eres un usuario inexperto te recomiendo
darle a si.

![25](https://user-images.githubusercontent.com/68520248/89324315-1a4c6580-d655-11ea-9e0b-5bf59cee4c6f.PNG)

Terminado esto nos pedira asignar una contraseña para ingresar con el usuario root

![26](https://user-images.githubusercontent.com/68520248/89324316-1a4c6580-d655-11ea-9b0c-d0428b6b27c2.PNG)

Y luego confirmamos

![27](https://user-images.githubusercontent.com/68520248/89324319-1ae4fc00-d655-11ea-9d2e-51a841f90c9e.PNG)

Listo!, ya tenemos nuestro LAMP levantado y operando sin problemas
