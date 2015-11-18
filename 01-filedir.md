---
layout: page
title: El Terminal Unix
subtitle: Archivos y Directorios
minutes: 15
---
> ## Objetivos de Aprendizaje {.objectives}
>
> * Explicar las similitudes y diferencias entre un archivo y un directorio.
> * Traducir una ruta absoluta en una ruta relativa y viceversa.
> * Construir rutas absolutas y relativas que identifican a archivos y directorios específicos.
> * Explicar los pasos en el ciclo lectura-ejecución-impresión del terminal.
> * Identificar al comando actual, banderas, y nombres de archivo en una llamada de línea de comandos.
> * Demostrar el uso de la completación con el tabulador, y explicar sus ventajas.

La parte del sistema operativo responsable de la gestión de archivos y directorios
se llama **sistema de archivos**.
Organiza nuestros datos en archivos,
que mantienen la información,
y directorios (también llamados "carpetas"),
que mantienen archivos u otros directorios.

Se utilizan varios comandos con frecuencia para crear, revisar, renombrar y borrar archivos y directorios.
Para iniciar la exploración de ellos,
vamos a abrir una ventana de comandos:

~~~ {.bash}
$
~~~

El signo del dólar es un **apuntador**, que nos muestra que el terminal está esperando una entrada;
su terminal puede utilizar un carácter diferente, como apuntador y puede añadir información antes
del apuntador. Al escribir comandos, ya sea desde estas lecciones o de otras fuentes,
no escriba el apuntador, sólo los comandos que le siguen.

Escriba el comando `whoami`,
a continuación, pulse la tecla Intro (a veces marcada Return) para enviar el comando al terminal.
La salida del comando es el ID del usuario actual,
es decir,
nos muestra quien cree el terminal que somos:

~~~ {.bash}
$ whoami
~~~
~~~ {.output}
nelle
~~~

Mas específicamente, cuando escribimos `whoami` el terminal:

1.  encuentra un programa `whoami`,
2.  ejecuta ese programa,
3.  muestra la salida del programa, y entonces
4.  muestra un nuevo apuntador para decirnos que está listo para mas comandos.

A continuación,
encontremos dónde estamos ejecutando el programa llamado `pwd`
(que significa "imprimir el directorio de trabajo", de "print working directory").
En cualquier momento,
nuestro **directorio de trabajo actual**
es nuestro actual directorio por defecto,
es decir,
el directorio en el que el computador asume que queremos ejecutar los comandos 
a menos que explícitamente indiquemos algo mas.
Aquí,
la respuesta de la computadora es `/Users/nelle`,
el cual es el **directorio home** (o "carpeta personal") de Nell:

~~~ {.bash}
$ pwd
~~~
~~~ {.output}
/Users/nelle
~~~

> ## Directorio home {.callout}
>
> La ruta del directorio home se verá diferente en distintos sistemas operativos.
> En Linux se verá algo como `/home/nelle`,
> y en Windows será similar a `C:\Documents and Settings\nelle`.
> Note que podría verse ligeramente diferente para distintas versiones de Windows.


> ## Alphabet Soup {.callout}
>
> Si el comando para encontrar quienes somos es `whoami`, el comando para encontrar
> donde estamos debería llamarse `whereami`, entonces ¿porqué en su lugar es `pwd`?
> La respuesta usual es que a principios de los 70s, cuando Unix estaba
> siendo desarrollado por primera vez, cada pulsación contaba: los dispositivos de entonces
> eran lentos, y la tecla de retroceso en un teletipo era tan complicado que acortar
> el número de pulsaciones con el fin de reducir el número de errores de tipeo era
> en realidad una victoria de la usabilidad. La realidad es que los comandos fueron añadidos a
> Unix uno por uno, sin un plan maestro, por gente que estaba inmersa en
> su jerga. El resultado es tan inconsistente como biba tu hortografía
> kasteyana, pero estamos entrampados en esto ahora.

Para entender lo que es un "directorio home",
vamos a echar un vistazo a cómo está organizado el sistema de archivos como un todo.
En la parte superior es el **directorio root** (raíz)
que contiene todo lo demás.
Nos referimos a él mismo mediante un carácter de barra `/`;
esta es la barra inicial en `/Users/nelle`.

Dentro de ese directorio hay varios otros directorios:
`bin` (en el cual se almacenan varios programas incorporados),
`data` (para archivos de datos misceláneos),
`Users` (donde están localizadas las carpetas personales de los usuarios),
`tmp` (para archivos temporales que necesitan estar almacenados por mucho tiempo),
y así:

![El Sistema de Archivos](fig/filesystem.svg)

Sabemos que nuestro directorio home actual `/Users/nelle` está almacenado dentro de` /Users`
porque `/Users` es la primera parte de su nombre.
Del mismo modo,
sabemos que `/Users` está almacenado dentro del directorio raíz `/`
debido a que su nombre comienza con `/`.

Debajo de `/Users`,
nos encontramos con un directorio para cada usuario con una cuenta en esta máquina.
Los archivos de la momia se almacenan en `/Users/imhotep`,
Los del hombre lobo en `/Users/larry`,
y la nuestra en `/Users/nelle`,
es por ello que `nelle` es la última parte del nombre del directorio.

![Directorios Home](fig/home-directories.svg)

> ## Path {.callout}
>
> Tenga en cuenta que hay dos significados para el carácter `/`.
> Cuando aparece en la parte delantera de un nombre de archivo o directorio,
> Se refiere al directorio raíz. Cuando aparece *dentro de* un nombre,
> Es tan sólo un separador.

Veamos lo que hay en el directorio home de Nelle ejecutando `ls`,
que significa "listar":

~~~ {.bash}
$ ls
~~~
~~~ {.output}
creatures  molecules           pizza.cfg
data       north-pacific-gyre  solar.pdf
Desktop    notes.txt           writing
~~~

![El directorio home de Nelle](fig/homedir.svg)

`ls` imprime los nombres de los archivos y directorios en el directorio actual en orden alfabético,
dispuestos ordenadamente en columnas.
Podemos hacer su salida más comprensible mediante el uso de la **bandera** `-F`,
que le pide a `ls` añadir al final un `/ `para los nombres de directorios:

~~~ {.bash}
$ ls -F
~~~
~~~ {.output}
creatures/  molecules/           pizza.cfg
data/       north-pacific-gyre/  solar.pdf
Desktop/    notes.txt            writing/
~~~

Aquí,
podemos ver que `/Users/nelle` contiene seis **subdirectorios**.
Los nombres que no tienen barras al final,
como `notes.txt`, `pizza.cfg`, y `solar.pdf`,
son archivos planos de toda la vida.
Y tenga en cuenta que hay un espacio entre `ls` y`-F`:
sin el,
el terminal cree que estamos tratando de ejecutar un comando llamado `ls-F`,
que no existe.

> ## ¿Qué es un nombre? {.callout}
>
> Podrías haber notado que todos los nombres de los archivos de Nelle 'son "algo punto
> algo". Esto es sólo una convención: podemos llamar a un archivo `mitesis` o
> casi cualquier otra cosa que queramos. Sin embargo, la mayoría de la gente usa nombres de dos-partes
> la mayor parte de su tiempo como ayuda propia (y para sus programas) para identificar diferentes tipos
> archivos. A la segunda parte de un nombre se le denomina
> **extensión de archivo**, e indica
> el tipo de datos que contiene el archivo: `.txt` señala un archivo de texto plano,`.pdf`
> indica un documento PDF, `.cfg` es un archivo de configuración lleno de parámetros
> para uno que otro programa, y así.
>
> Esto es sólo una convención, aunque una importante. Los archivos contienen
> bytes: nos toca a nosotros y a nuestros programas interpretar esos bytes
> de acuerdo a las normas de los documentos PDF, las imágenes, y así sucesivamente.
>
> Poner de nombre a la imagen PNG de una ballena `ballena.mp3` en todo caso no
> lo convierte mágicamente en la grabación de cantodeballena, a pesar de que *podría*
> hacer que el sistema operativo intente abrirla con un reproductor de música
> cuando alguien haga doble clic sobre él.

Ahora revisemos a lo que está en el directorio `data` de Nelle ejecutando `ls -F data`,
es decir.,
el comando `ls` con los **argumentos** `-F` y `data`.
El segundo argumento --- el que está *sin* un guión adelante --- le dice a `ls` que
queremos una lista de algo distinto de nuestro directorio de trabajo actual:

~~~ {.bash}
$ ls -F data
~~~
~~~ {.output}
amino-acids.txt   elements/     pdb/	        salmon.txt
animals.txt       morse.txt     planets.txt     sunspot.txt
~~~

La salida nos muestra que hay cuatro archivos de texto y dos sub-sub-directorios.
organizando las cosas jerárquicamente de esta manera nos ayuda a mantener un seguimiento de nuestro trabajo:
es posible poner cientos de archivos en nuestro directorio personal,
del mismo modo que es posible acumular cientos de papeles impresos en nuestro escritorio,
pero es una estrategia contraproducente.

Noten, por la forma en que deletreó el nombre del directorio `data`.
No tiene una barra final:
que se agrega a los nombres de directorio por `ls` cuando usamos la bandera `-F` que nos ayuda a separar las cosas.
Y no comienza con una barra porque es una **ruta relativa**,
es decir, le dice a `ls` cómo encontrar algo desde donde estamos,
en lugar de hacerlo desde la raíz del sistema de archivos.

> ## Parametros vs. Argumentos {.callout}
>
> De acuerdo a la [Wikipedia](https://en.wikipedia.org/wiki/Parameter_(computer_programming)#Parameters_and_arguments),
> los términos argumento y **parametro**
> significan cosas ligeramente diferentes.
> En la práctica,
> de todas maneras,
> la mayoría los utiliza de forma indistinta e inconsistente,
> así que nosotros también lo haremos.

Si corremos `ls -F /data` (*con* una barra al principio) obtenemos una respuesta diferente,
porque `/data` es una **ruta absoluta**:

~~~ {.bash}
$ ls -F /data
~~~
~~~ {.output}
access.log    backup/    hardware.cfg
network.cfg
~~~

The leading `/` tells the computer to follow the path from the root of the file system,
so it always refers to exactly one directory,
no matter where we are when we run the command.

What if we want to change our current working directory?
Before we do this,
`pwd` shows us that we're in `/Users/nelle`,
and `ls` without any arguments shows us that directory's contents:

~~~ {.bash}
$ pwd
~~~
~~~ {.output}
/Users/nelle
~~~
~~~ {.bash}
$ ls
~~~
~~~ {.output}
creatures  molecules           pizza.cfg
data       north-pacific-gyre  solar.pdf
Desktop    notes.txt           writing
~~~

We can use `cd` followed by a directory name to change our working directory.
`cd` stands for "change directory",
which is a bit misleading:
the command doesn't change the directory,
it changes the shell's idea of what directory we are in.

~~~ {.bash}
$ cd data
~~~

`cd` doesn't print anything,
but if we run `pwd` after it, we can see that we are now in `/Users/nelle/data`.
If we run `ls` without arguments now,
it lists the contents of `/Users/nelle/data`,
because that's where we now are:

~~~ {.bash}
$ pwd
~~~
~~~ {.output}
/Users/nelle/data
~~~
~~~ {.bash}
$ ls -F
~~~
~~~ {.output}
amino-acids.txt   elements/     pdb/	        salmon.txt
animals.txt       morse.txt     planets.txt     sunspot.txt
~~~

We now know how to go down the directory tree:
how do we go up?
We could use an absolute path:

~~~ {.bash}
$ cd /Users/nelle
~~~

but it's almost always simpler to use `cd ..` to go up one level:

~~~ {.bash}
$ pwd
~~~
~~~ {.output}
/Users/nelle/data
~~~
~~~ {.bash}
$ cd ..
~~~

`..` is a special directory name meaning
"the directory containing this one",
or more succinctly,
the **parent** of the current directory.
Sure enough,
if we run `pwd` after running `cd ..`, we're back in `/Users/nelle`:

~~~ {.bash}
$ pwd
~~~
~~~ {.output}
/Users/nelle
~~~

The special directory `..` doesn't usually show up when we run `ls`.
If we want to display it, we can give `ls` the `-a` flag:

~~~ {.bash}
$ ls -F -a
~~~
~~~ {.output}
./                  creatures/          notes.txt
../                 data/               pizza.cfg
.bash_profile       molecules/          solar.pdf
Desktop/            north-pacific-gyre/ writing/
~~~

`-a` stands for "show all";
it forces `ls` to show us file and directory names that begin with `.`,
such as `..` (which, if we're in `/Users/nelle`, refers to the `/Users` directory).
As you can see,
it also displays another special directory that's just called `.`,
which means "the current working directory".
It may seem redundant to have a name for it,
but we'll see some uses for it soon.
Finally, we also see a file called `.bash_profile`. This file usually contains settings to customize the shell (terminal). For this lesson material it does not contain any settings. There may also be similar files called `.bashrc` or `.bash_login`. The `.` prefix is used to prevent these configuration files from cluttering the terminal when a standard `ls` command is used.

> ## Orthogonality {.callout}
>
> The special names `.` and `..` don't belong to `ls`;
> they are interpreted the same way by every program.
> For example,
> if we are in `/Users/nelle/data`,
> the command `ls ..` will give us a listing of `/Users/nelle`.
> When the meanings of the parts are the same no matter how they're combined,
> programmers say they are **orthogonal**:
> Orthogonal systems tend to be easier for people to learn
> because there are fewer special cases and exceptions to keep track of.

## Nelle's Pipeline: Organizing Files

Knowing just this much about files and directories,
Nelle is ready to organize the files that the protein assay machine will create.
First,
she creates a directory called `north-pacific-gyre`
(to remind herself where the data came from).
Inside that,
she creates a directory called `2012-07-03`,
which is the date she started processing the samples.
She used to use names like `conference-paper` and `revised-results`,
but she found them hard to understand after a couple of years.
(The final straw was when she found herself creating
a directory called `revised-revised-results-3`.)

> ## Output sorting {.callout}
>
> Nelle names her directories "year-month-day",
> with leading zeroes for months and days,
> because the shell displays file and directory names in alphabetical order.
> If she used month names,
> December would come before July;
> if she didn't use leading zeroes,
> November ('11') would come before July ('7'). Similarly, putting the year first 
> means that June 2012 will come before June 2013.

Each of her physical samples is labelled according to her lab's convention
with a unique ten-character ID,
such as "NENE01729A".
This is what she used in her collection log
to record the location, time, depth, and other characteristics of the sample,
so she decides to use it as part of each data file's name.
Since the assay machine's output is plain text,
she will call her files `NENE01729A.txt`, `NENE01812A.txt`, and so on.
All 1520 files will go into the same directory.

If she is in her home directory,
Nelle can see what files she has using the command:

~~~ {.bash}
$ ls north-pacific-gyre/2012-07-03/
~~~

This is a lot to type,
but she can let the shell do most of the work through what is called **tab completion**.
If she types:

~~~ {.bash}
$ ls nor
~~~

and then presses tab (the tab key on her keyboard),
the shell automatically completes the directory name for her:

~~~ {.bash}
$ ls north-pacific-gyre/
~~~

If she presses tab again,
Bash will add `2012-07-03/` to the command,
since it's the only possible completion.
Pressing tab again does nothing,
since there are 1520 possibilities;
pressing tab twice brings up a list of all the files,
and so on.
This is called **tab completion**,
and we will see it in many other tools as we go on.

![File System for Challenge Questions](fig/filesystem-challenge.svg)

> ## Relative path resolution {.challenge}
>
> If `pwd` displays `/Users/thing`, what will `ls ../backup` display?
>
> 1.  `../backup: No such file or directory`
> 2.  `2012-12-01 2013-01-08 2013-01-27`
> 3.  `2012-12-01/ 2013-01-08/ 2013-01-27/`
> 4.  `original pnas_final pnas_sub`

> ## Many ways to do the same thing - absolute vs relative paths {.challenge}
>
> For a hypothetical filesystem location of /home/amanda/data/, 
> select each of the below commands that Amanda could use to navigate to her home directory, 
> which is /home/amanda 

>1.  `cd .`
>2.  `cd /`
>3.  `cd /home/amanda`
>4.  `cd ../..`
>5.  `cd ~`
>6.  `cd home`
>7.  `cd ~/data/..`
>8.  `cd`
>9.  `cd ..`

> ## `ls` reading comprehension {.challenge}
>
> If `pwd` displays `/Users/backup`,
> and `-r` tells `ls` to display things in reverse order,
> what command will display:
>
> ~~~
> pnas-sub/ pnas-final/ original/
> ~~~
>
> 1.  `ls pwd`
> 2.  `ls -r -F`
> 3.  `ls -r -F /Users/backup`
> 4.  Either \#2 or \#3 above, but not \#1.

> ## Default `cd` action {.challenge}
>
> What does the command `cd` without a directory name do?
>
> 1.  It has no effect.
> 2.  It changes the working directory to `/`.
> 3.  It changes the working directory to the user's home directory.
> 4.  It produces an error message.

> ## Exploring more `ls` arguments {.challenge}
>
> What does the command `ls` do when used with the `-s` and `-h`
> arguments?
