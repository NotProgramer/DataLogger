# Raspberry Datalogger ModBus

## Desafio: 
Levantar un servidor LAMP para un Datalogger ModBus con cliente TCP 

###### Hadware utilizado para este proyecto:

 - **Raspberry pi 3 b+:** 
 - *Ficha tecnica:*
 - *CPU + GPU: Broadcom BCM2837B0, Cortex-A53 (ARMv8) 64-bit SoC @ 1.4GHz*
 - *RAM: 1GB LPDDR2 SDRAM*
 - *Wi-Fi + Bluetooth: 2.4GHz y 5GHz IEEE 802.11.b/g/n/ac, Bluetooth 4.2, BLE*
 - *Ethernet: Gigabit Ethernet sobre USB 2.0 (300 Mbps)*
 - *GPIO de 40 pines*
 - *HDMI*
 - *4 puertos USB 2.0*
 - *Puerto CSI para conectar una cámara.*
 - *Puerto DSI para conectar una pantalla táctil*
 - *Salida de audio estéreo y vídeo compuesto*
 - *Micro-SD*
 - *Power-over-Ethernet (PoE)*

 - Tarjeta microSD 16GB clase10.
 - Teclado, mouse, Monitor con entrada HDMI.
 - Notebook para bajar y quemar la imagen ISO a la microSD.
 - Adaptador microSD a USB.

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

5. Conectar la Raspberrry a Internet mediante WLAN o Ethernet y ver la IP en la terminal con el comando
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


