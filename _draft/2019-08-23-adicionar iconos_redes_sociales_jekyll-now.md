---
layout: post
title: Añadir Íconos Redes Sociales en Jekyll-Now
date: 2019-08-23
author: Samuel R Osuna.
categories: Bloging, Jekyll-now, botones Redes Sociales, boton paypal
---

¿Por qué usar Linux para escribir literatura?

![_config.yml]({{ site.baseurl }}/redes-sociales.png)

Cuando comenzamos a hacer bloggins, y elegimos a Jekyll, muchas veces lo primero que hacemos es personalizar nuestro sitio, si bien es cierto que Jekyll-now cuenta con las redes sociales mas populares configuradas por defecto como Facebook, Twitter, Github, YouTube y otras más, a veces estan todas las que no nos sirven y no estan todas las que necesitamos.

En mi caso particular, yo estoy incursionando en otros sitios y desearía que mis lectores me siguieran por esas redes sociales o bien colocar un boton para poder recibir aportes de dinero por amigos o colocar un boton de pago que dirijha al visitante a una página de pagos, como PayPal.me.

En este artículo mostraremos como colocar un boton de pago, o el boton de una red social de preferencia personalizada, para el objeto de este ariculo mostraré el botón de pagos de PayPal.me que está en el footer o en el pié de página de esta web estática.

Lo primero que debemos hacer es buscar el botón que PayPal nos entrega en su web, o en una búsqueda por Google, buscar el botón bajo el formato SVG que bien nos parezca más cómodo, sin embargo este no debe exceder los 40px de ancho ni de alto, si pasa de este tamaño, deben usar alguna herramienta de diseño como Inskcape[1] y modificar el tamaño del archivo.

Una vez modificado el archivo en cuestión, tenemos que convertir el archivo a un formato de texto **Base64** que tenemos que agregar a un archivo en nuestro archivo *_svg-icons.scss* que se encuentra ubicado en la raíz dentro de la carpeta _sass/ en otras palabras o resumiendo, debemos convertir la imagen a texto ASCII, esto permite que nuestro Jekyll-now se mantenga liviano para cargar rápido mejorando la experiencia del usuario que visita nuestra página. Si no sabes que es base64, revisa en la Wikipedia sobre este tema[2]
 >~/proyecto.github.io_/_sass/_sass.scss 

Ahora que sabes que es Base64, para convertir el archivo hay muchos portales, te sugiero ir a este web, llamada Base64 Image Encoder[3]. Los pasos para convertirlos son muuy intuitivos, pero igual los voy a describir.
* Cargar la imagen según se indica en la imagen:
 ![_config.yml]({{ site.baseurl }}/articulo23-08-2018/imagen_base64.png)

- Seguidamente, te mostrará rapidamente un encoding por medio de una barra de progreso que se pondrá de color verde cuanto termine, en la parte derecha te mostrará 3 botones llamados `show code` `copy image` y `copy css` en este caso escogeremos `show code` y nos mostrará una nueva ventana donde podremos apreciar la información de la conversión de la imagen.

 ![_config.yml]({{ site.baseurl }}/articulo23-08-2018/showcode.png)

- Escogeremos la segunda opción, la que dice **For use as CSS background: ** primero hacemos click en `select all` y luego `copy to clipboard`

* Aqui tenemos que tener mucho cuidado con este paso, haz exactamente como lo indico, cabe recordar que no me hago responsable de cualquier problema causado si no lo haces bien. Lo que haremos en con el editor de texto preferido abrimos el archivo  `_sass.scss` ubicado en la carpeta `_svg-icons.sass/` para este artículo lo haré con el editor geany. Una vez abierto, podrán observar la configuración del archivo y cuidadosamente, casi al final insertarán una liena nueva justamente debajo de la ultima linea de la ultima red social, que en este caso es YouTube, ahora colocarán su información, en mi caso colocaré la de PayPal **Note que al final hay una llave cerrada, "}" déjenla como está** 

	  &.paypal        { background-image: 
Recuerden que copiaron el código base64 de la opción ** For use as CSS background:** y que comienza con `url('data:image/svg+xml;base64` dejen un espacio y peguen todo el codigo a partir de url y todo el resto. Este irá quedando así.
&.paypal        { background-image: url('data:image/svg+xml;base64,PD94bWwgdmVyc2...  ...noten que al final queda así...ICA8L2c+Cjwvc3ZnPgo=')
* inmediatamente luego del paréntesis cerrado del código base64, agregaremos en esa misma línea estos signos `; }`

 ![_config.yml]({{ site.baseurl }}/articulo23-08-2018/geany.png)
 
 y al final 
 ![_config.yml]({{ site.baseurl }}/articulo23-08-2018/geany2.png)

 Guardamos y cerramos el archivo pero aún queda dos cosas algo por hacer

 **Modificar el archivo `svg-icons.html` ubicado en la raiz del proyecto en la carpeta `_includes/`
 podemos copiar la anterior linea, y sustituimos los datos con el de nuestra red social o bien con el portal que queramos enlazar, en este caso es mi paypal.me
 que quedaría así:
>`  {% if site.footer-links.paypal %} <a href="https://paypal.me/{{ site.footer-links.paypal }}" target="_blank"><i class="svg-icon paypal"></i></a>{% endif %}`

Con esta modificación del archivo `svg-icons.html` el archivo principal _config.yml está siendo informado que existe otro botón en el footer de la página y que vamos a informarle ahora con los datos finales.
Abrimos nuestro archivo `_config.yml` y modificamos lo siguiente en la sección *# Includes an icon in the footer for each username you enter*
le indicamos ahora esto:
`paypal: srojas1974` 
Indicamos la red social que configuramos antes y el usuario a visitar cuando nuestro visitante te haga click te llevará al destino que configuras, en mi caso, al boton de cobro de PayPal
Nuestro Footer de la página quedaría así finalmente:

 ![_config.yml]({{ site.baseurl }}/articulo23-08-2018/footer2.png)

Y listo, así como esta caso, podemos agregar los botones de los logos de nuesrtos perfiles en las otras redes sociales para que nos visiten o sigan, o bien nos colaboren como en este caso, un boton de cobro para recibir pagos o bien si vendes tu servicio usando jekyll-now

 Y eso es todo, si te gustó o no, por favor no olvides comentar y compartir, si algo no te funciona, para poder ayudarte en lo que pueda, y también si lo consideras, me puedes invitar un café para poder seguir escribiendo estos articulos para ayudarte a mejorar tu sitio web en Jekyll-now colaborando en el  botón de PayPal.me.




**Referencias**
* [1] [Inkscape.](https://inkscape.org/)
* [2] [Wikipedia Base64](https://es.wikipedia.org/wiki/Base64)
* [3] [Base64 Image Encoder](https://www.base64-image.de/)