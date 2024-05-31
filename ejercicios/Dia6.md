# Trabajar con Remotos

Para poder colaborar en cualquier proyecto Git, necesitas saber cómo gestionar
repositorios remotos. Los repositorios remotos son versiones de tu proyecto que están
hospedadas en Internet o en cualquier otra red. Puedes tener varios de ellos, y en cada
uno tendrás generalmente permisos de solo lectura o de lectura y escritura. Colaborar
con otras personas implica gestionar estos repositorios remotos enviando y trayendo
datos de ellos cada vez que necesites compartir tu trabajo. Gestionar repositorios
remotos incluye saber cómo añadir un repositorio remoto, eliminar los remotos que ya
no son válidos, gestionar varias ramas remotas, definir si deben rastrearse o no y más.
En esta sección, trataremos algunas de estas habilidades de gestión de remotos.

## Añadir Repositorios Remotos

En secciones anteriores hemos mencionado y dado alguna demostración de cómo añadir
repositorios remotos. Ahora veremos explícitamente cómo hacerlo. Para añadir un remoto
nuevo y asociarlo a un nombre que puedas referenciar fácilmente, ejecuta
**git remote add [nombre] [url]**:

```bash
$ git remote
origin
$ git remote add pb https://github.com/paulboone/ticgit
$ git remote -v
origin https://github.com/schacon/ticgit (fetch)
origin https://github.com/schacon/ticgit (push)
pb https://github.com/paulboone/ticgit (fetch)
pb https://github.com/paulboone/ticgit (push)
```

A partir de ahora puedes usar el nombre pb en la línea de comandos en lugar de la
**URL** entera. Por ejemplo, si quieres traer toda la información que tiene Paul pero tú
aún no tienes en tu repositorio, puedes ejecutar **git fetch** pb:

```bash
$ git fetch pb
remote: Counting objects: 43, done.
remote: Compressing objects: 100% (36/36), done.
remote: Total 43 (delta 10), reused 31 (delta 5)
Unpacking objects: 100% (43/43), done.
From https://github.com/paulboone/ticgit
 * [new branch] master -> pb/master
 * [new branch] ticgit -> pb/ticgit
```

La rama maestra de Paul ahora es accesible localmente con el nombre pb/master -
puedes combinarla con alguna de tus ramas, o puedes crear una rama local en ese
punto si quieres inspeccionarla.

## Traer y Combinar Remotos

Como hemos visto hasta ahora, para obtener datos de tus proyectos remotos puedes
ejecutar:

```bash
$ git fetch [remote-name]
```

Si has configurado una rama para rastrear una rama remota, puedes usar el comando git pull para traer
y combinar automáticamente la rama remota con tu rama actual. Este flujo de trabajo es cómodo y
fácil, ya que al clonar un repositorio, git clone configura automáticamente la rama maestra local
para rastrear la rama maestra remota del servidor. Al ejecutar git pull, se traen datos del servidor
original y se intenta combinar automáticamente con el código en el que estás trabajando.

## Enviar a Tus Remotos

Para compartir un proyecto, debes enviarlo a un servidor usando el comando
**git push [nombre-remoto] [nombre-rama]**. Por ejemplo, para enviar tu rama master al servidor,
puedes usar

```bash
$ git push origin master.
```

Este comando funciona si tienes permisos de escritura en el servidor y si nadie más ha enviado datos
antes que tú. Si otro usuario envía información antes, tu envío será rechazado y tendrás que combinar
su trabajo con el tuyo antes de reenviar.

## Inspeccionar un Remoto

Si quieres ver más información acerca de un remoto en particular, puedes ejecutar el
comando git **remote show [nombre-remoto]**. Si ejecutas el comando con un nombre en
particular, como origin, verás algo como lo siguiente:

```bash
$ git remote show origin
* remote origin
  Fetch URL: https://github.com/schacon/ticgit
  Push URL: https://github.com/schacon/ticgit
  HEAD branch: master
  Remote branches:
  master tracked
  dev-branch tracked
  Local branch configured for 'git pull':
  master merges with remote master
  Local ref configured for 'git push':
  master pushes to master (up to date)
```

El comando lista la URL del repositorio remoto y la información del rastreo de ramas.
Indica que si estás en la rama maestra y ejecutas `git pull`, combinará automáticamente la
maestra remota con tu rama local después de traer toda la información. Además, lista todas las
referencias remotas de las que ha traído datos.

## Eliminar y Renombrar Remotos

Si quieres cambiar el nombre de la referencia de un remoto puedes ejecutar
**git remote rename.** Por ejemplo, si quieres cambiar el nombre de pb a paul, puedes hacerlo con
**git remote rename**:

```bash
$ git remote rename pb paul
$ git remote
origin
paul
```

Si por alguna razón quieres eliminar un remoto - has cambiado de servidor o no
quieres seguir utilizando un mirror o quizás un colaborador ha dejado de trabajar en el
proyecto - puedes usar **git remote rm** o **git remove**:

```bash
$ git remote rm paul
$ git remote
origin
```

## Resumen

- Trabajar con Remotos:

  > - Gestionar repositorios remotos es crucial para colaborar en proyectos Git.
  > - Implica añadir, eliminar y gestionar ramas remotas, además de definir si deben rastrearse.

- Añadir Repositorios Remotos:

  > - Usa `git remote add [nombre] [url]` para añadir un nuevo remoto.
  > - Permite referenciar el remoto por un nombre fácil en lugar de la URL completa.

- Traer y Combinar Remotos:

  > - Usa `git fetch [remote-name]` para obtener datos de un remoto.
  > - Si la rama está configurada para rastrear una rama remota, `git pull` combina automáticamente la rama remota con la local.

- Enviar a Tus Remotos:

  > - Usa `git push [nombre-remoto] [nombre-rama]` para enviar cambios a un servidor.
  > - Ejemplo: `git push origin master`.
  > - Necesitas permisos de escritura y que nadie más haya enviado cambios antes que tú.

- Inspeccionar un Remoto:

  > - Usa `git remote show [nombre-remoto]` para ver detalles de un remoto.
  > - Muestra la URL, el rastreo de ramas, y las referencias remotas.

- Eliminar y Renombrar Remotos:
  > - Usa `git remote rename` para cambiar el nombre de un remoto.
  > - Ejemplo: `git remote rename pb paul`.
  > - Usa `git remote rm` para eliminar un remoto.
  > - Ejemplo: `git remote rm paul`.

### El siguiente dia se vera :

> - Etiquetado
> - Listar Tus Etiquetas
> - Crear Etiquetas
> - Etiquetas Anotadas
> - Etiquetas Ligeras
> - Etiquetado Tardío
> - Compartir Etiquetas
> - Sacar una Etiqueta
