# Raspberry Datalogger ModBus

# Desafio 
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
  - [balenaEtcher](url)
  - [Raspberrry Pi 32-bits with Desktop](https://downloads.raspberrypi.org/raspios_full_armhf_latest)
  
###### Instalacion incial paso a paso:
1. Descargar SO que se utilizara (en este caso se ocupara Raspberry Pi OS 32-bits with Desktop)

2. Descargar la ISO

3. Descomprimir el archivo .rar

4. Quemar la ISO en la SD con tu quemador favorito, yo use balenaEtcher

5. Conectar la Raspberrry a Internet mediante WLAN o Ethernet y ver la IP en la terminal con el comando if-config

6. Abrir PuTTy y ingresar con la IP de nuestra Raspberrry

7. Habilitar la conexion con VNC viewer con el comando 
```
sudo raspi-config
```
   opcion 5, P3, Yes (imagen)

8. Establecer IP fija en raspi-config

9. Expander SD en raspi-config
