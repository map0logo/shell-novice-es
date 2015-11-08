---
layout: page
title: El Terminal Unix
subtitle: Introducción al Terminal
minutes: 5
---
> ## Objetivos de Aprendizaje {.objectives}
>
> *   Explicar como el terminal se relaciona con el teclado, la pantalla, el sistema operativo, y los programas del usuario.
> *   Explicar cuando y porque la interfaz de línea de comandos deben utilizarse en lugar de las interfaces gráficas.

A un alto nivel, las computadoras hacen cuatro cosas:

-   ejecutan programas
-   almacenan datos
-   se comunican entre ellas
-   interactúan con nosotros

Pueden hacer la última de muchas formas diferentes,
incluyendo enlaces directos cerebro-computador y las interfaces de voz.
Debido a que estas están todavía en su infancia,
la mayoría de nosotros utilizamos ventanas, iconos, ratones y apuntadores.
Estas tecnologías no se habían difundido hasta los 80s,
pero sus raíces se remontan a la obra de Doug Engelbart en los 60s,
que se puede ver en lo que se ha llamado
"[La Madre de Todos los Demos](http://www.youtube.com/watch?v=a11JDLBXtPQ)".

Yendo aún más atrás,
la única forma de interactuar con las primeras computadoras era volver a cablearlas.
Pero mientras tanto,
desde los años 50s hasta los 80s,
la mayoría de las personas utilizaban impresoras de línea.
Estos dispositivos sólo permitían la entrada y salida de letras, números y puntuación que se encontraba en un teclado estándar,
así que los lenguajes de programación e interfaces tuvieron que ser diseñados bajo esa restricción.

Este tipo de interfaz se denomina
**interfaz de línea de comandos**, o CLI (por command line interface),
para distinguirla de la
**interfaz gráfica de usuario**, o GUI (por graphical user interface),
que es la mas utilizada en la actualidad.
El corazón de un CLI es un **bucle de lectura-evaluación-impresión**, o REPL (por read-evaluate-print loop):
cuando el usuario escribe un comando y presiona la tecla intro (o enter, o return),
la computadora la lee,
la ejecuta,
e imprime su salida.
El usuario entonces escribe otro comando,
y así hasta que el usuario cierra su sesión.

Según esta descripción parece que el usuario envía comandos directamente a la computadora, 
y la computadora envía salida directamente al usuario.
De hecho,
hay usualmente un programa en el medio llamado
**terminal de comandos**.
Lo que el usuario escribe va al terminal,
El cual entonces se da cuenta cuales comandos correr y le ordena a la computadora ejecutarlos. Note que, el terminal se denomina también *la concha* (the shell) porque cubre al sistema operativo con el fin de esconder algo de su complejidad y hace mas simple interactuar con este.

Un terminal es un programa como cualquier otro.
Lo que es especial de este es que su trabajo es ejecutar otros programas
en lugar de realizar cálculos por sí mismo.
El terminal Unix mas popular es Bash,
el Bourne Again SHell
(llamado así porque está derivado del terminal escrito por Stephen Bourne --- esto
es lo que ocurre gracias al ingenio entre programadores).
Bash es el terminal por defecto en la mayoría de las implantaciones modernas de Unix
y en la mayoría de paquetes que proveen herramientas tipo Unix para Windows.

Usando Bash o cualquier otro terminal
a veces se siente más como programación que como usar un ratón.
Los comandos son concisos (a menudo de sólo un par de caracteres),
sus nombres son frecuentemente crípticos,
y su resultado es líneas de texto en lugar de algo visual como un gráfico.
Por otra parte,
el terminal nos permite combinar las herramientas existentes en formas poderosas con sólo unas pocas teclas
y crear tuberías para manejar grandes volúmenes de datos de forma automática.
Además, la línea de comandos es con frecuencia la más fácil de interactuar con las máquinas remotas y supercomputadoras.
La familiaridad con el terminal es casi esencial para ejecutar una gran variedad de herramientas y recursos especializados, incluidos los sistemas de computación de alto rendimiento. En la medida que los clusters y sistemas de computación en la nube se vuelven más populares para el procesamiento de datos científicos,
ser capaz de interactuar con ellos se está convirtiendo en una destreza necesaria. Podemos construir sobre las destrezas con la línea de comandos cubiertas aquí abordar una amplia gama de cuestiones científicas y retos computacionales.

## La secuencia de Nell: Punto de inicio

Nelle Nemo, una bióloga marino,
acaba de regresar de un estudio de seis meses del
[Giro del Pacífico Norte] (http://en.wikipedia.org/wiki/North_Pacific_Gyre),
donde ha estado tomando muestras de vida marina gelatinosa en el
[Gran Parche de Basura del Pacífico] (http://en.wikipedia.org/wiki/Great_Pacific_Garbage_Patch).
Ella tiene 300 muestras en total, y ahora tiene que:

1.  Ejecute cada muestra a través de una máquina de ensayo
    que medirá la abundancia relativa de 300 proteínas diferentes.
    La salida de la máquina para una sola muestra es
    un archivo con una línea para cada proteína.
2.  Calcular estadísticas para cada una de las proteínas por separado
    utilizando un programa que escribió su supervisor llamado `goostat`.
3.  Comparar las estadísticas para cada proteína
    con las estadísticas correspondientes para cada otra proteína
    utilizando un programa llamado `goodiff` que escribió otro estudiante de postgrado.
4.  Redactar resultados.
    A su supervisora realmente le gustaría que ella lo tuviese listo al final del mes
    para que su artículo pueda aparecer en un próximo número especial de *Cartas Goo Acuáticas*.
 
La máquina de ensayo se tarda una media hora para procesar cada muestra.
La buena noticia es que
sólo le toma dos minutos para ajustar cada una.
Dado que su laboratorio cuenta con ocho máquinas de ensayo que puede utilizar en paralelo,
este paso "sólo" le tomará unas dos semanas.

La mala noticia es que si ella tiene que ejecutar `goostat` y `goodiff` a mano,
tendrá que introducir los nombres de archivo y hacer clic en "OK" 45.150 veces
(300 ejecuciones de `goostat`, además de 300x299/2 ejecuciones de`goodiff`).
A 30 segundos cada uno,
que le tomará más de dos semanas.
No solamente perderá el plazo para la entrega del artículo,
las posibilidades de que escriba todos los comandos sin errores es prácticamente cero.

Las próximas lecciones explorarán lo que debe hacer en su situación.
Mas específicamente,
explica cómo puede utilizar un terminal de comandos
para automatizar los pasos repetitivos en su secuencia de procesamiento
de modo que su computadora puede trabajar 24 horas al día, mientras escribe su artículo.
Como beneficio adicional,
una vez haya confeccionado una secuencia de procesamiento,
ella será capaz de volver a utilizarla cada vez que recoja más datos.

