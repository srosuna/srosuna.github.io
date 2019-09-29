---
layout: post
title: Como arreglar el problema de la descarga fallida en WAMP LAMP XAMP para actualizar tu WordPress.
date: 2019-09-29
author: Samuel R Osuna.
categories: Wordpress, xamp, lamp, php, actualizar, descarga, fallida.
---

Hoy vengo con un articulo un poco fuera de la temática del blog, pero que me paso esta falla de nuevo no hace mucho, y recordé que escribí algo al respecto en mi perfil de linkedin, que dejé de usarlo porque al tener una máquina con bajos recursos, esa página (linkedin) se ha puesto muy pesada para mi gusto, así que me traje el artículo técnico para este portal en github donde la sencillez y lo liviano es lo que reina.


Muchas veces tenemos el problema en WordPress Joomla, Drupal, etc, cuando lo instalamos y vamos a actualizar a la nueva versión del CMS o algún plugins del mismo no sale el siguiente error:

>  There are no HTTP transports available which can complete the requested request

También nos puede salir en español, ingles o combinación de ambos:

*  **ing**
 
*  **transports**

*  **found**

Esto no se debe generalmente a un problema en tu CMS o algún archivo en tu carpeta **www/** esto se debe a una configuración en tu archivo **php.ini**, no obstante para arreglar este problema es sumamente sencillo, más de lo que piensas.

Este aviso de error ocurre, porque unas extensiones en nuestro PHP están inhabilitadas y solo tenemos que habilitarlas, para ello, solo necesitaremos algun editor de texto, para este articulo estoy usando un servidor local Windows y el servicio de WAMP, en Linux el servicio sería Lamp, pero es igual en todo caso.

Un Linux, abundan muchos editores de textos fiables y eficientes, como GNU/Nano, VIM, o gráfico como Geany. En Windows, recomendaría usar Geany, es software libre y muy bien editor de texto plano.


Las extensiones PHP a habilitar son **Curl** y **OpenSSL**.


#### **Pasos para arreglar el problema:**

*  Buscamos con nuestro navegador en la carpeta www/ el archivo phpinfo.php (si lo tienes sigue al paso 2) en caso que no lo tengas creamos un nuevo archivo con el nombre **phpinfo.php** y le colocamos esto, guardamos y cerramos iniciamos los servicios de WAMP:
  
	<?php
	
	  phpinfo();
	
	?>

*  Abrimos http://localhost/phpinfo.php y vamos hasta "Loaded Configuration File " ahí nos muestrará la ruta donde se encuentra, en mi caso esta en C:\wamp\bin\apache\apache2.2.22\bin\php.ini

*  Con nuestro editor de texto buscamos donde se encuentra la linea:
> 	;extension=php_curl.dll

*  Eliminamos el principio el signo de punto y coma ";" y nos queda así:

> 	 extension=php_curl.dll

*	Buscamos la siguiente linea:
> 	;extension=php_openssl

*	De igual forma eliminamos el signo de punto y coma ";" para quedarnos así
> 	extension=php_openssl

* Guardas, cierras, reinicias los servicios de Apache, esto solucionaria el problema y no deberías tenerlos tampoco para actualizar tu WordPress u otro CMS y sus plugins.

Este articulo deriva de una versión en ingles llamada [How to fix: There are no HTTP transports available which can complete the requested request](http://wpgyan.com/how-to-fix-there-are-no-http-transports-available-which-can-complete-the-requested-request/) que me sirvió de guía para resolver este problema.

Este post, está originalmente publicado en mi perfil en [Linkedin](https://www.linkedin.com/pulse/como-arreglar-el-problema-de-la-descarga-fallida-en-wamp-r-osuna/) el cual lo estoy republicando aquí en mi nuevo hosting en Github.

### Finalmente.

Por favor, si conoces otro método para arreglar el problema, puedes dejarlo en los comentarios, y si puedes, comparte en tus redes para que esta información llegue a otras personas. Si gustas y deseas apoyarme, te acepto un café, para seguir investigando y sacar nuevos tips, al final de esta página encontrarás un boton de [PayPal](https://paypal.me/srojas1974) donde puedas enviarme una contribución para tomar un café.
