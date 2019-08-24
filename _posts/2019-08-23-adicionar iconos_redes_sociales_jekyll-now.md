---
layout: post
title: Añadir íconos Redes Sociales o boton de pago PayPal.me en Jekyll-Now
date: 2019-08-23
author: Samuel R Osuna.
categories: Bloging, Jekyll-now, botones Redes Sociales, Botón PayPal
---

Añadir botones de otras Redes Sociales al footer de Jekyll-now o un botón de pago como PayPal.me

![_config.yml]({{ site.baseurl }}/images/redes-sociales.png)

Cuando comenzamos a hacer blogging, y elegimos a Jekyll, muchas veces lo primero que queremos hacer es personalizar nuestro sitio web estático a nuestro gusto, es cierto que Jekyll-now cuenta con las redes sociales mas populares configuradas por defecto como Facebook, Twitter, Github, YouTube y otras más, muchas veces están todas las que no requerimos, y no se encuentran las que necesitamos.

En mi caso particular, yo estoy incursionando en otros sitios y desearía que mis lectores me siguieran por esas redes sociales o bien colocar un botón para poder recibir aportes de dinero por amigos o colocar un botón de pago que dirija al visitante a una página de pagos, como PayPal.me por si quiero recibir donaciones u ofrecer algún artículo o servicio a la venta a través del sitio web.

En este artículo mostraremos como colocar un botón de pago, aunque sive para colocar el botón de una red social de preferencia personalizada, para el objeto de este artículo mostraré el botón de pagos de PayPal.me que pueden ver en el footer o parte inferior de esta web estática.

**Requerimientos**
* Tener un blog en Github con Jekyll-now.
* Nociones básicas de html5.
* Nociones básicas de Git.
* Nociones básicas de manejo de programa de edición de gráficos vectoriales como Inkscape en caso de ser requerido.
* Manejo de consola Linux.
* Nociones de edición en lenguaje de marcado ligero como Markdown.

Trataré de ser lo más explicativo posible para que una persona con poco conocimientos en computación, pueda entender este tutorial. Si tienes alguna duda por favor no olvides comentar.

**Comencemos**

* Lo primero que debemos hacer es buscar la imagen del botón  PayPal que nos entregan en su web, o preferiblemente hacer una búsqueda en Google, bajo el formato SVG que bien nos parezca más cómodo, sin embargo este no debe exceder en el tamaño los 40px de alto ni de ancho, si pasa de este tamaño, deben usar alguna herramienta de diseño como Inskcape[1] y modificar el tamaño del archivo.

 + Una vez modificada la imagen a la medida requerida, tenemos que convertir el archivo imagen.svg (el nombre que conseguiste tu botón en ese formato) a un formato de texto **Base64** que serán agregadas al archivo `_svg-icons.scss` que se encuentra ubicado en la raíz dentro de la carpeta `_sass/` . 

 >~/Mi_proyecto_repositorio_github/_sass/_sass.scss 

* Resumiendo, debemos convertir la imagen a texto ASCII, esto permite que nuestro Jekyll-now se mantenga liviano para cargar rápido mejorando la experiencia del usuario que visita nuestra página web o blog. Si no sabes que es base64, revisa en la Wikipedia sobre este tema[2].

* Ahora que sabes que es Base64, para convertir el archivo hay muchos portales, te sugiero ir a esta web, llamada Base64 Image Encoder[3]. Los pasos para convertirlos son muy intuitivos, pero igual los voy a describir.

* Cargar el archivo imagen según se indica en la imagen, bien sea arrastrando con el ratón o cargando con el uploader:

 ![_config.yml]({{ site.baseurl }}/images/articulo23-08-2018/imagen_base64.png)

* Seguidamente, te mostrará rápidamente un encoding por medio de una barra de progreso que se pondrá de color verde cuanto termine, en la parte derecha te mostrará 3 botones llamados `|show code|`, `|copy image|` y `|copy css|` en este caso escogeremos `|show code|` y nos mostrará una nueva ventana donde veremos la información de la conversión de la imagen.

 ![_config.yml]({{ site.baseurl }}/images/articulo23-08-2018/showcode.png)

- Escogemos la segunda opción, la que dice **For use as CSS background:** primero hacemos click en `|select all|` y luego `|copy to clipboard|`

* Llegados a este punto, aquí tenemos que tener mucho cuidado con este paso, haz exactamente como lo indico, cabe recordar que no me hago responsable de cualquier problema causado. Lo que haremos es abrir el archivo  `_sass.scss` ubicado en la carpeta `_svg-icons.sass/` con nuestro editor de texto favorito, yop uso VIM, pero puedes usar el que mas te guste, como uso Linux como sistema operativo, para este artículo y mostrarlo de forma gráfica, lo haré con el editor Geany pero repito, pueden usar el que más les guste. Una vez abierto, podrán observar la configuración del archivo y cuidadosamente, casi al final insertarán una linea nueva justamente debajo de la ultima linea, de la ultima red social, que en este caso es YouTube en otros puede ser el extinto Google+. 

* Ahora colocarán su información, en mi caso colocaré la de PayPal **Note que al final hay una llave cerrada, "}" déjenla como está**  

* Para que lo puedan ver mejor, vean con cuidado las dos imágenes siguientes antes de seguir.

	  &.paypal        { background-image: 

* Recuerden que copiaron el código base64 de la opción **For use as CSS background:** y que comienza con `url('data:image/svg+xml;base64` dejen un espacio y peguen todo el codigo a partir de url y todo el resto. Este irá quedando así:

>&.paypal        { background-image: url('data:image/svg+xml;base64,PD94bWwgdmVyc2...  ...**noten que al final queda así**...ICA8L2c+Cjwvc3ZnPgo=')

* Inmediatamente luego del paréntesis cerrado del código base64, agregaremos en esa misma línea estos signos `; }` quedando cerrado de esta forma:

> ...Pgo=') ; }

 ![_config.yml]({{ site.baseurl }}/images/articulo23-08-2018/geany.png)
 
 y al final 
 
 ![_config.yml]({{ site.baseurl }}/images/articulo23-08-2018/geany2.png)

 Guardamos y cerramos el archivo pero aún queda dos cosas por hacer

- Modificar el archivo `svg-icons.html` ubicado en la raiz del proyecto en la carpeta `_includes/`
 podemos copiar la anterior linea, y sustituimos los datos con el de nuestra red social o bien con el portal que queramos enlazar, en este caso es mi paypal.me
 que quedaría así:
>`  {% if site.footer-links.paypal %} <a href="https://paypal.me/{{ site.footer-links.paypal }}" target="_blank"><i class="svg-icon paypal"></i></a>{% endif %}`

Con esta modificación del archivo `svg-icons.html` el archivo principal de Jekyll-now el `config.yml` está siendo informado que existe otro botón en el footer de la página y que vamos a informarle ahora con los datos finales.

- Abrimos nuestro archivo `_config.yml` y lo modificamos añadiendo la siguiente información de nuestro usuario de PayPal.me en la sección *# Includes an icon in the footer for each username you enter* y le indicamos ahora esto:


`paypal: srojas1974`  

* Y así quedaría finalmente:

 ![_config.yml]({{ site.baseurl }}/images/articulo23-08-2018/config_yml.png) 
 
 >«Para efecto de este tutorial la imagen indica la primera linea de la sección, pero realmente debe ser la última, sin embargo, es opcional para usted donde lo ponga. Sólo no elimine las demás que estaban previamente ahí»

Con esto, ya estamos indicando a nuestros usuarios que nos sigan o visiten en las redes sociales o que nos hagan pagos/contribuciones/donaciones a la plataforma de pago preferida por medio del botón de pago que acabamos de configurar, cuando nuestro visitante haga clic en ese botón lo llevará al destino que configuramos previamente, en mi caso, al boton de cobro de PayPal.me.


Nuestro Footer de la página quedaría así finalmente:
 ![_config.yml]({{ site.baseurl }}/images/articulo23-08-2018/footer2.png)
 
*  Un ultimo paso es que una vez revisado en nuestro sistema local, a través de jekyll server, ahora es momento de subir los cambios a Github desde la carpeta raiz de nuestro proyecto

>$ git add .
>
>$ git commit -m "subir botón PayPal.me"
>
>$ git push origin master

Y listo, así es como podemos agregar los botones de plataformas de pago, y tambien los logos de nuestros perfiles en las otras redes sociales que no estén en jekyll-now, para que nos visiten o sigan, o bien nos colaboren como en este caso, un botón de cobro para recibir pagos o bien si vendes tu servicio usando jekyll-now en Github.

 Y eso es todo, si te gustó o no, por favor no olvides comentar y compartir, si algo no te funciona escribe para poder ayudarte en lo que pueda, y también si lo consideras, me puedes invitar un café ya que me gusta escribir y lo que me motiva es una buena taza de té, café o una gaseosa, y poder seguir generando contenido, y publicar algunos tips que iré descubriendo para mejorar tu sitio web en Jekyll-now y sobre herramientas libres para escritores con equipos de bajos recursos.

**Enlaces Externos**
* [1] [Inkscape.](https://inkscape.org/)
* [2] [Wikipedia Base64](https://es.wikipedia.org/wiki/Base64)
* [3] [Base64 Image Encoder](https://www.base64-image.de/)
