# Fundamentos de Git

Este dia junto a los siguientes cubre todos los comandos básicos que necesitas
para hacerla gran mayoría de cosas a las que eventualmente vas a dedicar tu
tiempo mientras trabajas con Git.

## Obteniendo un repositorio Git

Puedes obtener un proyecto Git de dos maneras. La primera es tomar un proyecto
o directorio existente e importarlo en Git. La segunda es clonar un repositorio existente
en Git desde otro servidor

### Inicializando un repositorio en un directorio existente

Si estas empezando con git la forma de inicializar un **repo** es con :

```
$ git init
```

Esto crea un subdirectorio nuevo llamado .git, el cual contiene todos los archivos
necesarios del repositorio

probablemente deberías comenzar el seguimiento de esos archivos y
hacer una confirmación inicial. Puedes conseguirlo con unos pocos comandos **git add**
para especificar qué archivos quieres controlar, seguidos de un **git commit** para confirmar
los cambios:

```
$ git add LICENSE
$ git commit -m 'initial project version'
```

### Clonando un repositorio existente

Si deseas obtener una copia de un repositorio Git existente — por ejemplo, un
proyecto en el que te gustaría contribuir — el comando que necesitas es **git clone**. Si
estás familizarizado con otros sistemas de control de versiones como Subversion, verás
que el comando es **"clone"** en vez de **"checkout"**. Es una distinción importante, ya que
Git recibe una copia de casi todos los datos que tiene el servidor. Cada versión de
cada archivo de la historia del proyecto es descargada por defecto cuando ejecutas
**git clone**.

Puedes clonar un repositorio con **git clone [url]**. Por ejemplo, si quieres clonar la
librería de Git llamada **libgit2** puedes hacer algo así:

```
$ git clone https://github.com/libgit2/libgit2
```

Esto crea un directorio llamado libgit2, inicializa un directorio .git en su interior,
descarga toda la información de ese repositorio y saca una copia de trabajo de la
última versión. Si te metes en el directorio libgit2, verás que están los archivos del
proyecto listos para ser utilizados.

Si quieres clonar el repositorio a un directorio con
otro nombre que no sea libgit2, puedes especificarlo con la siguiente opción de línea
de comandos:

```
$ git clone https://github.com/libgit2/libgit2 mylibgit
```

Ese comando hace lo mismo que el anterior, pero el directorio de destino se llamará
mylibgit.

## Guardando cambios en el Repositorio

Ya tienes un repositorio Git y un checkout o copia de trabajo de los archivos de
dicho proyecto. El siguiente paso es realizar algunos cambios y confirmar instantáneas
de esos cambios en el repositorio cada vez que el proyecto alcance un estado que
quieras conservar.

Mientras editas archivos, Git los ve como modificados, pues han sido cambiados
desde su último commit. Luego preparas estos archivos modificados y finalmente
confirmas todos los cambios preparados, y repites el ciclo.
![ciclo de cambios de un repo](/imagenes/ciclo%20de%20cambios%20de%20un%20repo%20-%20dia%20tres.jpg)

## Resumen :

- Obtener un repositorio Git:

> - Puedes iniciar un nuevo repositorio en un directorio existente con git init.
> - También puedes obtener una copia de un repositorio existente usando git clone [url].

- Guardar cambios en el repositorio:
  > - Realiza cambios en los archivos.
  > - Utiliza git add para preparar los cambios y git commit para confirmarlos en el repositorio.

### El dia siguiente se vera :

> - Revisando el Estado de tus Archivos
> - Rastrear Archivos Nuevos
> - Preparar Archivos Modificados
> - Estado Abreviado
> - Ignorar Archivos
> - Confirmar tus Cambios
> - Eliminar Archivos
> - Ver el Historial de Confirmaciones
