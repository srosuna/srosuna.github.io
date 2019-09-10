---
layout: post
title: GNU Nano, Software Para Escribir Literatura y Manuales de forma Profesional Y Sin Distracciones en Linux.
date: 2019-09-03
author: Samuel R Osuna.
categories: Blogging, writing, literatura, software, libre, foss, distraction-free, nano, gnu
---
#### Escritura libre de distracciones, también llamado en inglés: #distraction-free con una herramienta en linea de comandos que solemos pasar por alto.

¡Usa lo más simple, no te compliques!

En nuestros sistemas libres como GNU/Linux, a veces tenemos instalados ciertos software que obviamos de lado por creer que son para cosas puntuales o extremadamente sencillas por ignorancia o bien porque nos enamoró otro editor y creemos que es lo mejor, y uno de ellos que usamos poco para cosas profesionales es GNU Nano.

Cuando se trata de escribir eficientemente, las herramientas que utilizamos son cruciales para nuestro éxito. Cuanto más simple, mejor.

Estoy probando algunas herramientas de escritura sin distracciones y después de jugar con ellas durante unos días, vuelvo regularmente a LibreOffice para hacer mi trabajo, pero para hacer la segunda fase de edición.

Como decía Hemingway,
> «*Escribe borracho, edita sobrio*»

Al escribir nuestros textos, muchos de ustedes saben que van apareciendo en la mente las escenas y uno  lo va describiendo en el teclado ─o en el papel─, y para ello no quieres ser molestado o distraído.

Recordé que siempre tuve una herramienta de línea de comandos instalada en mi estación de trabajo Linux que usaba poco para otras cosas como editar los archivos de configuración de otros programas, ediciones banales y sencillas, pero después de preguntarme si podría servirme para escribir de forma profesional y como es un software tan maduro, me dije ¡vamos a estudiarlo!, y luego de revisar sus opciones, me di cuenta que pudo haberme ahorrado y salvado de estallidos temporales de locura hace años...

Pero, después de leer la página de manual de nano, encontré algunas opciones interesantes.

En un terminal típico de UNIX / Linux, se puede escribir el siguiente comando y disfrutar de un entorno de escritura sin distracciones que realmente nos ayuda a lograr nuestro objetivo.

> $ nano -alMw$

#### ¿Pero, que es Nano?
O GNU/Nano, es un editor de texto simple que suelen traer nuestros sistema operativos por defecto, o está disponible en la mayoría de las distribuciones linux.

Mas información la puedes conseguir en [Wikipedia](https://es.wikipedia.org/wiki/GNU_Nano) es software libre, bajo la licencia pública general [GNU](https://es.wikipedia.org/wiki/Licencia_p%C3%BAblica_general_de_GNU)

La forma típica de instalar en sistema Debian y derivadas es la siguiente si usamos sudo.

> $ sudo apt install nano

#### Configurando GNU/Nano modo libre de distracciones para escritores.
La configuración se realiza pasando opciones de línea de comandos al programa.

> nano       -alMw$

 ![_config.yml]({{ site.baseurl }}/images/articulo-10-09-2019/nano3.png)


Las siguientes opciones son necesarias para crear el entorno de escritura libre de distracciones que puede ver en la captura de pantalla anterior.

>`-a líneas de ajuste en el espacio en blanco.`
>
> `-l mostrar números de línea.`
>
> `-M eliminar espacios en blanco al final de las líneas envueltas.`
>
> `-w deshabilita el ajuste de líneas largas.`
>
> `-$ enable soft-wrapping (continuar en varias líneas).`

Esta configuración podría guardarse de forma permanente en `~/.config/nano/nanorc` . Sin embargo, esto es opcional, en mi caso, necesito tener nano por defecto para otros fines que también uso a diario, pero en tu caso puedes hacerlo si te gusta.

#### Configurando la Terminal Linux.

Aquí vamos a colocar la forma que se nos presentará la terminal linux para escribir.
Dependiendo de tu entorno de trabajo, si es Gnome, KDE, esto puede variar, pero como este artículo está enfocado a usuarios que tienen equipos con bajos recursos, supongo que estás usando como escritorio o entorno de escritorio XFCE, LXQT, o bien LXDE, las opciones entre estos escritorios no son del otro mundo, son muy parecidas o muy básicas por lo cual serán muy intuitivas, y se ajustarán de acuerdo a tu pantalla, si usas doble monitor, o uno solo, si usas uno pequeño como el de las minilaptos o un monitor normal, en este caso solo mostraré las generales para que un ser humano común pueda trabajar.

 ![_config.yml]({{ site.baseurl }}/images/articulo-10-09-2019/terminal_preferencias.png)

 En mi caso escojo una fuente amarilla brillante sobre un fondo negro que pueden ver en la siguiente captura cuando estaba redactando este artículo.

  ![_config.yml]({{ site.baseurl }}/images/articulo-10-09-2019/nano1.png)

#### Trabajar con Nano.

Para crear un nuevo archivo:

> `$ nano -alMw$ archivo_nuevo.txt`

  ![_config.yml]({{ site.baseurl }}/images/articulo-10-09-2019/nano2.png)

Y así tenemos un entorno de redacción libre de distracciones, donde puedo resaltar algunas cosas que noté de primera mano.


* Nano consume minimo de recursos en comparación a otros editores de textos, supuestamente livianos.
* Si bien no se elimina las ventana del todo ni te ocupa el 100% de la pantalla del computador,  es claro que se apodera una gran parte de este.
* El menú inferior no es molesto.
* La tabulación fluirá libremente, lo que han trabajado con Nano con anterioridad saben que la linea de texto se irá hacia la salida derecha de la pantalla, pero gracias a la opcion `-w y -$` podemos escribir tranquilamente y el texto al finalizar la linea pasará a la linea siguiente en pantalla, aunque forme parte de la linea sin hacer el salto o la entrada con la tecla de entrada o «enter».

Generalmente Nano viene en el idioma del sistema, y solo debes acostumbrarte al uso de algunos de sus comandos que con la práctica se hace mas fácil cada día. Pero te describiré algunos rápidamente.

* Control+G o ^G: Ver Ayuda
* ^O Guardar :guardar documento
* ^W Buscar : buscar una palabra en sí, ubica al cursor en la primera letra o carácter del texto buscado.
* ^K Cortar txt: cortar texto, tambien puedes usarlo para copiar.
* ^U Pegar txt: pega el texto copiado/cortado.
* ^J Justificar (usar con cuidado, ajusta forzadamente todo el texto escrito en un parrafo, no recomendable para la literatura, se usa para otros fines)
* ^X Salir para salir del programa, si hicimos cambios nos preguntará una confirmación, y si no, se sale automáticamente.

#### Conclusiones.

 Creo que mas simple que esta herramienta, muy pocas existe, en verdad hay muchas opciones distraction-free o libre de distracciones tanto libres como privativas, pero tan livianas como estas ninguna, no es la mejor, estoy seguro, pero si la mas versátil.

 Para escribir artículos, capítulos de nuestras novelas, blog, y otras más de verdad es una herramienta a considerar, no ocupa mucho espacio ni consume tantos recursos.

 Tiene muchos trucos más, muchas opciones, por lo cual te recomiendo a que lo revises, y compartas, si tienes alguna duda, no olvides comentar.
