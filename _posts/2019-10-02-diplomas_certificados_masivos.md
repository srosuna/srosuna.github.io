---
layout: post
title: Generando Certificados y Diplomas con Python más Rst2pdf Para Eventos En Venezuela 
date: 2019-10-02
author: Samuel R Osuna.
categories: Flisol, certificados, diplomas, impresion, masiva, python2, python3, gnu, software, libre, foss
---
Modificación de  la fuente original publicada por Ramiro Algozino.

Hace un tiempo atrás, me vi en la necesidad de realizar un evento de Software Libre, que necesitaba emitir certificados de asistencia a dicho evento, gracias a el amigo [Ralgozino](http://twitter.com/ralgozino) y su [blog](https://ralgozino.wordpress.com/2012/04/20/generando-certificados-diplomas-con-python-rst2pdf/) donde esta la fuente de esta script Generando Certificados / Diplomas con Python + rst2pdf pude crear una adaptación para Venezuela de dicha script, ya que, aunque no es necesario, en los Eventos de cualquier índole en Venezuela, se requiere colocar el numero de cédula o pasaporte para su debida validez.

Es bien sabido que algunos de estos eventos los asistentes exigen o bien los organizadores emiten algun certificado de asistencia, pero hay pocos manuales en la web bajo software libre documentados para hacerlo, esta ejemplo, [pyploma](https://bioinformatiquillo.wordpress.com/2011/07/07/pyploma-generador-de-diplomas-en-latex-a-patir-de-una-lista-de-datos/) otro que se hace con [python + Apache OpenOffice](https://forum.openoffice.org/es/forum/viewtopic.php?f=50&t=8818) entre otros, algunos complicados dependiendo del nivel del programador y que exigen algun conocimiento más avanzado.

Este tutorial esta realizado para venezolanos, aunque no es limitativo ya que es software libre y cualquiera lo puede modificar y redistribuir bajo los términos de la licencia GPL v3. 

Este tutorial está orientado para personas que tengan una necesidad de emitir certificados de forma masiva sea por ejemplo:
- Eventos de software libre
- Cursos
- Formación y
- cualquier actividad que requiera una impresión masiva de certificados.

#### Requerimientos

* Uso de GNU/Linux.
* Conocimiento de uso de terminal. (no es complicado)
* Conocimiento de Git. (preferible que tengas claro esto, por lo que requiere una cuenta en github)
* Python2.x instalado y funcional (pronto exportaré a python3)
* Conocimiento del lenguaje de marcado rst.
	- Para esto debes tener instalado rst2pdf, en sistemas basados en Debian ejecutar.
	
>  	$ sudo aptitude install rst2pdf

* Es posible que algo de conocimiento de diseño gráfico, aunque existen aplicaciones como [Canva](canva.com) o bien contrata tu diseñador gráfico favorito para crear tu diploma y/o certificado. En tal caso en formato png, jpg, jpeg.

#### Comenzamos:

Clona o descarga desde mi repositorio en [github](https://github.com/srosuna/certificados-en-python) en tu pc. en el destino de tu preferencia.

> $ git clone https://github.com/srosuna/certificados-en-python

y quedaría algo así:

 ![_config.yml]({{ site.baseurl }}/images/certificados/ls.png)
 
 Los archivos importantes son los siguientes:
*  **asistentes.csv** : Contiene el listado de nuestros participantes y el tipo de participación, ya sea como exponentes, colaboradores o asistentes, o el que se nos ocurra.

* **certificado.rst**: Es el archivo que contiene la forma de como estará estructurada y será distribuida la información de la script.
*  **estilo.style**: un archivo en css para configurar junto con el rst la impresión de salida del diploma.
*  **generar_certificado.py**: Nuestra script en python

* **certificado.png**: Este es el nombre del archivo de imagen base que irá de fondo en el pdf generado. El nombre puede ser cualquiera, pero ten en cuenta que si usas otro nombre, tendrás que hacer modificaciones al archivo estilo.style, de todos modos sigue este tutorial.
* La carpeta **Samples/** que contiene la fuente del archivo pns, llamado **certificado.svg**, es la fuente en svg que puede ser modificado en el programa [Inkscape](http://inkscape.org), si sabes modificar estos archivos te lo dejo para tu facilidad.
* La carpeta **pdf/** es donde se guardarán los archivos generados en pdf como resultado de la impresión digital con la script

Una vez llegados aquí veamos los archivos como están estructurados, veamos a **asistentes.csv.**

> $ cat asistentes.csv 
> Exponente,Lea,Grabriela,V-12.823.321
> Asistente,Romero,Ingrid,E-82.345.678
> Colaborador,Belice,Marika,V-99.765.432

 ![_config.yml]({{ site.baseurl }}/images/certificados/asistentes.png)
 
Como observamos en este ejemplo, vemos a 3 asistentes, hubiera podido ser más, como un listado de 500 personas, pero como esta es una prueba ustedes lo harán con pocas personas, con tres roles distintos cada uno.
* Un *Ponente* u orador, o speaker, etc,
* Una persona del publico como *Asistente* quien fue el participante que pago su entrada.
* Finalmente un *Colaborador*  quien trabaja para la parte organizativa y quería su certificado como colaborador.

Vamos a asignar mentalmente un valor para cada campo, separados con comas, y podríamos enumerarlas cada una así:
- calidad = asistente[0] ahí se aprecia si es ponente, asistente o colaborador.
- apellido = asistente[1] Apellido de la persona.
- nombre = asistente[2] Nombre de la persona.
- cédula = asistente[3] Su documento de identidad.

 Veamos el archivo *certificado.rst* este es quien nos dará los parametros para generar el certificado de asistencia:

>  $ cat certificado.rst
> 
>  {1} {2}, *Cédula* {3}
>  .. raw:: pdf
>     Spacer 0,55
> 
>  {0}

 
*  certificado.png es un archivo de imagen, nuestro certificado modelo que necesita el siguiente archivo para informar a la script a fin de generar el certificado. Adjunto la imagen para que ustedes si no quieren modificar (pueden hacerlo en el svg que está en la carpeta Samples/), es para que sepan donde van los campos a usar.
 
  ![_config.yml]({{ site.baseurl }}/images/certificados/certificado.png)
  
  En teoría pueden usar cualquier archivo de imagen, yo solo hasta ahora he usado archivos con extensión png y jpg.
  
#### Preparando el archivo de css o estilo.style
El archivo *estilo.style* es solo un simple archivo de texto que nos ayudara a colocar el fondo de la presentación, el transpondrá junto con la script el fondo de imagen, en este caso *certificado.png* o si bien tu archivo de imagen tiene otro nombre, modificas en este en la linea 17 el nombre del archivo, yo lo dejaré con "certificado.png".

> 12 "pageTemplates" : {
> 13     "Fondo": {
> 14         "frames": [
> 15             ["550px", "-810px", "100%", "100%"]
> 16         ],
> **17         "background" : "certificado.png"**

#### Archivo de Script en Python.
Solo revisamos que el archivo esté igual, como verán no tienen nada que hacer, no deben realizar muchos cambios, quizás, ninguno que altere el funcionamiento.

>  #!/usr/bin/env python
> #-*- encoding: utf-8 -*-
> 
>  from csv import reader
>  import subprocess
> 
>  print 'Abriendo listado...',
>  # Esto se puede poner feo...
>  listado = reader(open('asistentes.csv','r'))
>  total = len(list(listado))
>  listado = reader(open('asistentes.csv','r'))
>  print 'listo.'
> 
>  print 'Abriendo certificado...',
>  certificado = open('certificado.rst').read()
>  print 'listo.'
> 
>  print listado
>  print 'Encontrados', total, 'asistentes:'
>  for nro, asistente in enumerate(listado):
>      calidad = asistente[0]
>      apellido = asistente[1]
>      nombre = asistente[2]
>      cedula = asistente[3]
>      certificado_final = 
> certificado.format(calidad,apellido,nombre,cedula)
>
> print 'Generando certificado para', apellido.upper(), nombre + '...',
>  
> p = subprocess.Popen(['rst2pdf',
> '-s',
>                          'estilo.style,freetype-serif,a4-landscape,twelvepoint',
>  '--fit-background-mode=scale',
>  '-o',
>  './pdf/' + cedula + '.pdf'
>  ],
>  stdin=subprocess.PIPE
>  )
> p.stdin.write(certificado_final)
> p.communicate()
> print 'listo', str(nro+1), 'de', str(total) +'.'


#### Corriendo la Script

Para correr la script tenemos dos opciones:
* Dar permisos de operación (recomendado)

> $ sudo chmod +x generar_certificados.py

Luego la ejecutamos directamente:

> $./generar_certificados.py

*  O bien, la ejecutamos con python:

> $ python generar_certificados.py


Al final nos crea un archivo pdf por cada registro, en la carpeta del mismo nombre **pdf/** con el nombre del numero de cédula para facilitar la búsqueda del mismo si se tiene a la mano. 1234567x.pdf

Al final te muestra un reporte donde se aprecia cuantos archivos generó y como se ejecutó el proceso.

  ![_config.yml]({{ site.baseurl }}/images/certificados/Pantalla_terminal.jpeg)

Y el certificado y/o diploma generado, lo aprecias aquí:

  ![_config.yml]({{ site.baseurl }}/images/certificados/salida_certificado.png)

#### Conclusiones.

Si bien, parece un poco complicado, no lo es para nada, no cuesta leer un poco, y seguir los pasos poco a poco e intuir por ti mismo si necesitas hacer cambios específicos, igual te garantizo que si te llega un listado de 500 personas, o 100 o 50, tardarías mucho más haciendo certificado por certificado que lo que tardarías en leer y poner en práctica este tutorial.

Este tutorial la primera vez lo escribí hace años, en el año 2013 en mi anterior blog en [blogger](http://srosuna.blogspot.com/2014/09/generando-certificados-diplomas-con.html), pero no pierde efectividad, ahora está disponible para ser descargado desde Github.

Ahora bien, si necesitas mayor ayuda, no dudes en dejar tus comentarios, en tal caso si te salvo de un apuro, apreciaría mucho, si compartes este artículo en tus redes sociales, me regalas un like, comentas o bien si me invitas a un café, en el botón de PayPal al final de esta página.

Tambien si una organización necesita este servicio, puede contactarme en privado para algun trabajo al respecto, si necesita generar certificados y/o diplomas de forma masiva.
