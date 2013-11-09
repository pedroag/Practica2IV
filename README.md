Practica 2 IV
=============

Descripción
-----------

La práctica consiste en la creación de una jaula y la instalación dentro de apache para poder ejecutar una versión simple
del periódico de la priméra práctica.

Pasos a seguir
--------------

* En primer lugar creo la jaula, en este caso he utilizado la primera que se crea en los ejercicios con la siguiente orden:

        sudo debootstrap --arch=i386 quantal /home/jaulas/quantal/ http://archive.ubuntu.com/ubuntu

  ![captura1](https://dl.dropbox.com/s/fh7d1ckqlldqn44/creando%20jaula.png)


* Ahora accedo a la jaula mediante:

        sudo chroot /home/jaulas/quantal/


* Ya estamos dentro de la jaula. En mi caso tengo que instalar apache:

        apt-get install apache2
        
  Al instalarlo me da un error, indicándome que el puerto 80 de localhost ya está en uso. En ese caso como el editor de 
  texto que viene instaldo en la jaula es vi, lo utilizo para modificar el archivo /etc/apache2/ports.conf:
  
  ![captura2](https://dl.dropbox.com/s/eoz12diaonhz85h/modificando%20puerto)
  
  Susituyo por 8080 donde pone 80. Ya puedo acceder a los dos poniendo localhost:80 o localhost:8080 en el navegador según
  quiera.
  
* EL siguiente paso es copiar contenido del periódico dentro de la carpeta /var/www de la jaula para mostrar su funcionamiento.
  Para eso copio desde fuera de la jaula los archivos:

        sudo cp -r Periodico/* /home/jaulas/quantal/var/www
  
  Y reinicio apache:
  
        etc/init.d/apache2 restart
        
  Pero al ver localhost:8080 en el navegador veo que no se ve el css ni las imágenes, esto es debido que no tengo permisos
  sobre la jaula. Lo siguiente que hago es dar permisos con:
  
        sudo chmod -R 755 /home/jaulas/quantal/

  Y vuelvo a copiar todos los archivos del periódico.

* Ahora si, ya puedo acceder a la jaula con localhost:8080

  ![captura3](https://dl.dropbox.com/s/hdltrodb5to38pq/local%20puerto%208080)
  
  En cambio si pongo localhost:80
  
  ![captura4](https://dl.dropbox.com/s/4j3bsg5g7frzzr3/local%20puerto%2080)

Anotación: Los archivos del periódico no los adjunto, ya que no son de relevancia.
