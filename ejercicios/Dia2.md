# Fundamentos de Git

## Copias instantáneas, no diferencias

Git no maneja ni almacena sus datos de esta forma. Git maneja sus datos como
un conjunto de copias instantáneas de un sistema de archivos miniatura. Cada vez que
confirmas un cambio, o guardas el estado de tu proyecto en Git, él básicamente toma
una foto del aspecto de todos tus archivos en ese momento y guarda una referencia a
esa copia instantánea. Para ser eficiente, si los archivos no se han modificado Git
no almacena el archivo de nuevo, sino un enlace al archivo anterior idéntico que ya
tiene almacenado. Git maneja sus datos como una secuencia de copias instantáneas.

## Casi todas las operaciones son locales

La mayoría de las operaciones en Git sólo necesitan archivos y recursos locales para
funcionar. Por lo general no se necesita información de ningún otro computador de tu
red. Si estás acostumbrado a un CVCS donde la mayoría de las operaciones tienen el
costo adicional del retardo de la red, este aspecto de Git te va a hacer pensar que
los dioses de la velocidad han bendecido Git con poderes sobrenaturales. Debido a
que tienes toda la historia del proyecto ahí mismo, en tu disco local, la mayoría de las
operaciones parecen prácticamente inmediatas.

## Git tiene integridad

Todo en Git es verificado mediante una suma de comprobación (checksum en inglés)
antes de ser almacenado, y es identificado a partir de ese momento mediante dicha
suma. Esto significa que es imposible cambiar los contenidos de cualquier archivo o
directorio sin que Git lo sepa. Esta funcionalidad está integrada en Git al más
bajo nivel y es parte integral de su filosofía. No puedes perder información durante su
transmisión o sufrir corrupción de archivos sin que Git sea capaz de detectarlo.

El mecanismo que usa Git para generar esta suma de comprobación se conoce como
hash SHA-1. Se trata de una cadena de 40 caracteres hexadecimales (0-9 y a-f), y se
calcula con base en los contenidos del archivo o estructura del directorio en Git. Un
hash SHA-1 se ve de la siguiente forma:

```
24b9da6552252987aa493b52f8696cd6d3b00373
```

## Los Tres Estados

Ahora presta atención. Esto es lo más importante que debes recordar acerca de Git
si quieres que el resto de tu proceso de aprendizaje prosiga sin problemas. Git
tiene tres estados principales en los que se pueden encontrar tus archivos: confirmado
(committed), modificado (modified), y preparado (staged). Confirmado: significa que los
datos están almacenados de manera segura en tu base de datos local. Modificado:
significa que has modificado el archivo pero todavía no lo has confirmado a tu base de
datos. Preparado: significa que has marcado un archivo modificado en su versión actual
para que vaya en tu próxima confirmación.

Esto nos lleva a las tres secciones principales de un proyecto de Git: El directorio de
Git (Git directory), el directorio de trabajo (working directory), y el área de
preparación (staging area).

![Estados de git](/imagenes/Estados%20de%20git%20-%20dia%20dos.jpg)

El flujo de trabajo básico en Git es algo así:

- Modificas una serie de archivos en tu directorio de trabajo.
- Preparas los archivos, añadiéndolos a tu área de preparación.
- Confirmas los cambios, lo que toma los archivos tal y como están en el área de
  preparación y almacena esa copia instantánea de manera permanente en tu directorio
  de Git.

## Instalación de Git Para Windows

Antes de empezar a utilizar Git, tienes que instalarlo en tu computadora. Incluso si ya
está instalado, este es posiblemente un buen momento para actualizarlo a su última
versión. Puedes instalarlo como un paquete, a partir de un archivo instalador o bajando
el código fuente y compilándolo tú mismo.

También hay varias maneras de instalar Git en Windows. La forma más oficial está
disponible para ser descargada en el sitio web de Git. Solo tienes que visitar ![http://gitscm.com/download/win](http://gitscm.com/download/win) y la descarga empezará automáticamente.

## Configurando Git por primera vez

Ahora que tienes Git en tu sistema, vas a querer hacer algunas cosas para
personalizar tu entorno de Git. Es necesario hacer estas cosas solamente una vez en tu
computadora, y se mantendrán entre actualizaciones. También puedes cambiarlas en
cualquier momento volviendo a ejecutar los comandos correspondientes.

Git trae una herramienta llamada git config, que te permite obtener y establecer
variables de configuración que controlan el aspecto y funcionamiento de Git. Estas
variables pueden almacenarse en tres sitios distintos:

1. Archivo /etc/gitconfig: Contiene valores para todos los usuarios del sistema y todos
   sus repositorios. Si pasas la opción --system a git config, lee y escribe
   específicamente en este archivo.

2. Archivo ~/.gitconfig o ~/.config/git/config: Este archivo es específico de tu usuario.
   Puedes hacer que Git lea y escriba específicamente en este archivo pasando la
   opción --global.

3. Archivo config en el directorio de Git (es decir, .git/config) del repositorio que
   estés utilizando actualmente: Este archivo es específico del repositorio actual.
   Cada nivel sobrescribe los valores del nivel anterior, por lo que los valores de
   .git/config tienen preferencia sobre los de /etc/gitconfig.

En sistemas Windows, Git busca el archivo .gitconfig en el directorio $HOME (para
mucha gente será (C:\Users\$USER)). También busca el archivo /etc/gitconfig, aunque esta
ruta es relativa a la raíz MSys, que es donde decidiste instalar Git en tu sistema
Windows cuando ejecutaste el instalador.

### Tu Identidad

Lo primero que deberás hacer cuando instales Git es establecer tu nombre de
usuario y dirección de correo electrónico. Esto es importante porque los "commits" de
Git usan esta información, y es introducida de manera inmutable en los commits
que envías:

```
$ git config --global user.name "John Doe"
$ git config --global user.email johndoe@example.com
```

### Comprobando tu Configuración

Si quieres comprobar tu configuración, puedes usar el comando git config --list para
mostrar todas las propiedades que Git ha configurado:

```
$ git config --list
user.name=John Doe
user.email=johndoe@example.com
color.status=auto
color.branch=auto
color.interactive=auto
color.diff=auto
...
```

Si alguna vez necesitas ayuda usando Git puedes usar el comando git help

```
$ git help
```

## Resumen :

- Git maneja sus datos como un conjunto de copias instantáneas de un sistema de archivos miniatura, lo que significa que cada vez que confirmas un cambio, Git toma una foto del estado de todos tus archivos en ese momento.
  > - Esto asegura eficiencia, ya que Git no almacena nuevamente archivos idénticos, sino un enlace a la copia anterior.
- La mayoría de las operaciones en Git son locales, lo que significa que no necesitas información de otros equipos en tu red, lo que otorga una velocidad notable a las operaciones.
- La integridad en Git se garantiza mediante checksums, lo que significa que todo cambio en los archivos es verificado y registrado por Git. Esto previene la corrupción de archivos o la pérdida de información durante la transmisión.
  > - Git utiliza el hash SHA-1 para generar estas sumas de comprobación.
- Los tres estados principales en los que se pueden encontrar tus archivos en Git son: confirmado, modificado y preparado. Esto refleja si los cambios están almacenados, han sido modificados pero no confirmados, o están listos para ser confirmados en la próxima versión.
  > - Estos estados corresponden al directorio de Git, el directorio de trabajo y el área de preparación.
  > - El flujo de trabajo básico en Git incluye la modificación de archivos, la preparación de los cambios y la confirmación de los mismos en el directorio de Git.
- La instalación de Git en Windows puede realizarse desde el sitio web oficial de Git, ofreciendo opciones como paquetes de instalación o descarga del código fuente.
- Es importante personalizar la configuración de Git según tus preferencias y necesidades. Esto se puede hacer mediante el comando git config, que establece variables de configuración en diferentes niveles: sistema, usuario o repositorio actual.
  > - Configurar tu identidad en Git, incluyendo tu nombre de usuario y dirección de correo electrónico, es fundamental para identificar tus contribuciones al proyecto.
  > - Puedes verificar tu configuración en cualquier momento con el comando git config --list y obtener ayuda adicional con git help.
