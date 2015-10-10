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
para distinguirla de
**interfaz gráfica de usuario**, o GUI (por graphical user interface),
que es la mas utilizadas en la actualidad.
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
El cual entonces se da cuenta cuales comandos correr y le ordena a la computadora ejecutarlos. Note que, el terminal se denomina *la concha* (the shell) porque cubre al sistema operativo con el fin de esconder algo de su complejidad y hace mas simple interactuar con este.

Un terminal es un programa como cualquier otro.
Lo que es especial de este es que su trabajo es ejecutar otros programas
en lugar de realizar cálculos por sí mismo.
El termina Unix mas popular es Bash,
el Bourne Again SHell
(llamado así porque está derivado del terminal escrito por Stephen Bourne --- esto
es lo que ocurre gracias al ingenio entre programadores).
Bash es el terminal por defecto en la mayoría de las impantaciones modernas de Unix
y en la mayoría de paquetes que proveen herramientas tipo Unix para Windows.

Using Bash or any other shell
sometimes feels more like programming than like using a mouse.
Commands are terse (often only a couple of characters long),
their names are frequently cryptic,
and their output is lines of text rather than something visual like a graph.
On the other hand,
the shell allows us to combine existing tools in powerful ways with only a few keystrokes
and to set up pipelines to handle large volumes of data automatically.
In addition, the command line is often the easiest way to interact with remote machines and supercomputers.
Familiarity with the shell is near essential to run a variety of specialised tools and resources including high-performance computing systems. As clusters and cloud computing systems become more popular for scientific data crunching,
being able to interact with them is becoming a necessary skill. We can build on the command-line skills covered here to tackle a wide range of scientific questions and computational challenges.

## Nelle's Pipeline: Starting Point

Nelle Nemo, a marine biologist,
has just returned from a six-month survey of the
[North Pacific Gyre](http://en.wikipedia.org/wiki/North_Pacific_Gyre),
where she has been sampling gelatinous marine life in the
[Great Pacific Garbage Patch](http://en.wikipedia.org/wiki/Great_Pacific_Garbage_Patch).
She has 300 samples in all, and now needs to:

1.  Run each sample through an assay machine
    that will measure the relative abundance of 300 different proteins.
    The machine's output for a single sample is
    a file with one line for each protein.
2.  Calculate statistics for each of the proteins separately
    using a program her supervisor wrote called `goostat`.
3.  Compare the statistics for each protein
    with corresponding statistics for each other protein
    using a program one of the other graduate students wrote called `goodiff`.
4.  Write up results.
    Her supervisor would really like her to do this by the end of the month
    so that her paper can appear in an upcoming special issue of *Aquatic Goo Letters*.

It takes about half an hour for the assay machine to process each sample.
The good news is that
it only takes two minutes to set each one up.
Since her lab has eight assay machines that she can use in parallel,
this step will "only" take about two weeks.

The bad news is that if she has to run `goostat` and `goodiff` by hand,
she'll have to enter filenames and click "OK" 45,150 times
(300 runs of `goostat`, plus 300x299/2 runs of `goodiff`).
At 30 seconds each,
that will take more than two weeks.
Not only would she miss her paper deadline,
the chances of her typing all of those commands right are practically zero.

The next few lessons will explore what she should do instead.
More specifically,
they explain how she can use a command shell
to automate the repetitive steps in her processing pipeline
so that her computer can work 24 hours a day while she writes her paper.
As a bonus,
once she has put a processing pipeline together,
she will be able to use it again whenever she collects more data.

