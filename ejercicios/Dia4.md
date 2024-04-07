# Fundamentos de Git

Este dia junto a los siguientes cubre todos los comandos básicos que necesitas
para hacerla gran mayoría de cosas a las que eventualmente vas a dedicar tu
tiempo mientras trabajas con Git.

## Revisando el Estado de tus Archivos

La herramienta principal para determinar qué archivos están en qué estado es el
comando **git status**. Si ejecutas este comando inmediatamente después de clonar un
repositorio, deberías ver algo como esto:

```java
git status
On branch master
nothing to commit, working directory clean
```

Esto significa que tienes un directorio de trabajo limpio - en otras palabras, que no hay
archivos rastreados y modificados. Además, Git no encuentra archivos sin rastrear,
de lo contrario aparecerían listados aquí. Finalmente, el comando te indica en cuál rama
estás y te informa que no ha variado con respecto a la misma rama en el servidor.
Por ahora, la rama siempre será **“master”**, que es la rama por defecto.

Supongamos que añades un nuevo archivo a tu proyecto, un simple README. Si el
archivo no existía antes y ejecutas git status, verás el archivo sin rastrear de la
siguiente manera:

```java
$ echo 'My Project' > README
$ git status
On branch master
Untracked files:
  (use "git add <file>..." to include in what will be committed)
  README
nothing added to commit but untracked files present (use "git add" to track)
```

Puedes ver que el archivo **README** está sin rastrear porque aparece debajo del
encabezado “Untracked files” (“Archivos no rastreados” en inglés) en la salida. Sin
rastrear significa que Git ve archivos que no tenías en el commit anterior. Git
no los incluirá en tu próximo commit a menos que se lo indiques explícitamente. Se
comporta así para evitar incluir accidentalmente archivos binarios o cualquier otro
archivo que no quieras incluir. Como tú sí quieres incluir **README**, debes comenzar a
rastrearlo.

## Rastrear Archivos Nuevos

Para comenzar a rastrear un archivo debes usar el comando **git add**. Para comenzar a
rastrear el archivo README, puedes ejecutar lo siguiente:

```java
$ git add README
```

Ahora si vuelves a ver el estado del proyecto, verás que el archivo **README** está siendo
rastreado y está preparado para ser confirmado:

```java
$ git status
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)
  new file: README
```

Puedes ver que está siendo rastreado porque aparece luego del encabezado
**“Cambios aser confirmados”** **(“Changes to be committed” en inglés)**. Si confirmas en este punto, se
guardará en el historial la versión del archivo correspondiente al instante en que
ejecutaste **git add**. Anteriormente cuando ejecutaste **git init**, ejecutaste luego
**git add (files)** - lo cual inició el rastreo de archivos en tu directorio. El comando **git add**
puede recibir tanto una ruta de archivo como de un directorio; si es de un directorio,
el comando añade recursivamente los archivos que están dentro de él.

## Preparar Archivos Modificados

Vamos a cambiar un archivo que esté rastreado. Si cambias el archivo rastreado llamado
**“CONTRIBUTING.md”** y luego ejecutas el comando **git status**, verás algo parecido a esto:

```java
$ git status
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)
  new file: README
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)
  modified: CONTRIBUTING.md
```

El archivo **“CONTRIBUTING.md”** aparece en una sección llamada **“Changes not staged for**
**commit” (“Cambios no preparado para confirmar” en inglés)** - lo que significa que existe
un archivo rastreado que ha sido modificado en el directorio de trabajo pero que aún
no está preparado. Para prepararlo, ejecutas el comando **git add**. **git add**es un comando
que cumple varios propósitos - lo usas para empezar a rastrear archivos nuevos,
preparar archivos, y hacer otras cosas como marcar archivos en conflicto por
combinación como resueltos. Es más útil que lo veas como un comando para
**“añadir este contenido a la próxima confirmación”** más que para
**“añadir este archivo al proyecto”**

```java
$ git add CONTRIBUTING.md
$ git status
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)
  new file: README
  modified: CONTRIBUTING.md
```

Ambos archivos están preparados y formarán parte de tu próxima confirmación. En este
momento, supongamos que recuerdas que debes hacer un pequeño cambio en
**CONTRIBUTING.md** antes de confirmarlo. Abres de nuevo el archivo, lo cambias y ahora
estás listos para confirmar. Sin embargo, ejecutemos **git status** una vez más:

```java
$ vim CONTRIBUTING.md
$ git status
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)
  new file: README
  modified: CONTRIBUTING.md
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)
  modified: CONTRIBUTING.md
```

Ahora **CONTRIBUTING**.md aparece como preparado y como no preparado.
¿Cómo es posible? Resulta que Git prepara un archivo de acuerdo al estado que
tenía cuando ejecutas el comando **git add**. Si confirmas ahora, se confirmará la versión
de **CONTRIBUTING.md** que tenías la última vez que ejecutaste **git add** y no la versión que
ves ahora en tu directorio de trabajo al ejecutar **git status**. Si modificas un archivo
luego de ejecutar **git add**, deberás ejecutar **git add** de nuevo para preparar la última
versión del archivo:

```java
$ git add CONTRIBUTING.md
$ git status
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)
  new file: README
  modified: CONTRIBUTING.md
```

## Ignorar Archivos

A veces, tendrás algún tipo de archivo que no quieres que Git añada
automáticamente o más aun, que ni siquiera quieras que aparezca como no rastreado.
Este suele ser el caso de archivos generados automáticamente como trazas o archivos
creados por tu sistema de compilación. En estos casos, puedes crear un archivo llamado
**.gitignore** que liste patrones a considerar. Este es un ejemplo de un archivo .**gitignore**:

```java
$ cat .gitignore
*.[oa]
*~
```

La primera línea le indica a Git que ignore cualquier archivo que termine en **“.o”**o
**“.a”** - archivos de objeto o librerías que pueden ser producto de compilar tu código. La
segunda línea le indica a Git que ignore todos los archivos que terminen con una
**tilde (~)**, la cual es usada por varios editores de texto como Emacs para marcar
archivos temporales. También puedes incluir cosas como trazas, temporales, o pid
directamente; documentación generada automáticamente; etc. Crear un archivo **.gitignore**
antes de comenzar a trabajar es generalmente una buena idea, pues así evitas confirmar
accidentalmente archivos que en realidad no quieres incluir en tu repositorio Git.

Las reglas sobre los patrones que puedes incluir en el archivo .gitignore son las
siguientes:

- Ignorar las líneas en blanco y aquellas que comiencen con #.
- Emplear patrones glob estándar que se aplicarán recursivamente a todo el directorio
  del repositorio local.
- Los patrones pueden comenzar en barra (/) para evitar recursividad.
- Los patrones pueden terminar en barra (/) para especificar un directorio.
- Los patrones pueden negarse si se añade al principio el signo de exclamación (!).

Los patrones glob son una especie de expresión regular simplificada usada por los
terminales.

```java
# ignora los archivos terminados en .a
*.a
# pero no lib.a, aun cuando había ignorado los archivos terminados en .a en la línea
anterior
!lib.a
# ignora unicamente el archivo TODO de la raiz, no subdir/TODO
/TODO
# ignora todos los archivos del directorio build/
build/
# ignora doc/notes.txt, pero no este: doc/server/arch.txt
doc/*.txt
# ignora todos los archivos .txt del directorio doc/
doc/**/*.txt
```

## Confirmar tus Cambios

Ahora que tu área de preparación está como quieres, puedes confirmar tus cambios.
Recuerda que cualquier cosa que no esté preparada - cualquier archivo que hayas
creado o modificado y que no hayas agregado con **git add** desde su edición - no será
confirmado. Se mantendrán como archivos modificados en tu disco. En este caso,
digamos que la última vez que ejecutaste git status verificaste que todo estaba
preparado y que estás listo para confirmar tus cambios. La forma más sencilla de
confirmar es escribiendo **git commit -m ("text")**

```java
$ git commit -m "Story 182: Fix benchmarks for speed"
[master 463dc4f] Story 182: Fix benchmarks for speed
 2 files changed, 2 insertions(+)
 create mode 100644 README
```

¡Has creado tu primera confirmación (o **commit**)! Puedes ver que la confirmación te
devuelve una salida descriptiva: indica cuál rama has confirmado (**master**), que checksum
SHA-1 tiene el **commit** (463dc4f), cuántos archivos han cambiado y estadísticas sobre las
líneas añadidas y eliminadas en el commit.

## Eliminar Archivos

Para eliminar archivos de Git, debes eliminarlos de tus archivos rastreados (o mejor
dicho, eliminarlos del área de preparación) y luego confirmar. Para ello existe el
comando **git rm**, que además elimina el archivo de tu directorio de trabajo de manera
que no aparezca la próxima vez como un archivo no rastreado.
Si simplemente eliminas el archivo de tu directorio de trabajo, aparecerá en la sección
**“Changes not staged for commit”** (esto es, sin preparar) en la salida de git status:

```java
$ rm PROJECTS.md
$ git status
On branch master
Your branch is up-to-date with 'origin/master'.
Changes not staged for commit:
  (use "git add/rm <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)
  deleted: PROJECTS.md
no changes added to commit (use "git add" and/or "git commit -a")
```

Ahora, si ejecutas **git rm**, entonces se prepara la eliminación del archivo:

```java
$ git rm PROJECTS.md
rm 'PROJECTS.md'
$ git status
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)
  deleted: PROJECTS.md
```

Con la próxima confirmación, el archivo habrá desaparecido y no volverá a ser
rastreado. Si modificaste el archivo y ya lo habías añadido al índice, tendrás que forzar
su eliminación con la opción **-f**. Esta propiedad existe por seguridad, para prevenir que
elimines accidentalmente datos que aun no han sido guardados como una instantánea y
que por lo tanto no podrás recuperar luego con Git.

Al comando **git** rm puedes pasarle archivos, directorios y patrones glob. Lo que significa
que puedes hacer cosas como

```java
$ git rm log/\*.log
```

## Ver el Historial de Confirmaciones

Después de haber hecho varias confirmaciones, o si has clonado un repositorio que ya
tenía un histórico de confirmaciones, probablemente quieras mirar atrás para ver qué
modificaciones se han llevado a cabo. La herramienta más básica y potente para hacer
esto es el comando **git log**.

```java
$ git log
commit ca82a6dff817ec66f44342007202690a93763949
Author: Scott Chacon <schacon@gee-mail.com>
Date: Mon Mar 17 21:52:11 2008 -0700
  changed the version number

commit 085bb3bcb608e1e8451d4b2432f8ecbe6306e7e7
Author: Scott Chacon <schacon@gee-mail.com>
Date: Sat Mar 15 16:40:33 2008 -0700
  removed unnecessary test

commit a11bef06a3f659402fe7563abf99ad00de2209e6
Author: Scott Chacon <schacon@gee-mail.com>
Date: Sat Mar 15 10:31:28 2008 -0700

  first commit
```

Por defecto, si no pasas ningún parámetro, **git log** lista las confirmaciones hechas sobre
ese repositorio en orden cronológico inverso. Es decir, las confirmaciones más recientes
se muestran al principio. Como puedes ver, este comando lista cada confirmación con su
suma de comprobación SHA-1, el nombre y dirección de correo del autor, la fecha y el
mensaje de confirmación.

- Revisando el Estado de tus Archivos:

> - El comando principal para verificar el estado de tus archivos es git status.
> - Muestra información sobre archivos no rastreados, modificados y la rama actual.

- Rastrear Archivos Nuevos:

> - Para comenzar a rastrear un archivo nuevo, se utiliza git add.
> - Después de agregar un archivo, aparece en la sección "Cambios a ser confirmados" en git status.

- Preparar Archivos Modificados:

> - Después de realizar cambios en un archivo rastreado, se debe usar git add nuevamente para prepararlo para la confirmación.
> - git add se utiliza para preparar archivos nuevos, modificar archivos existentes y otras acciones relacionadas.

- Ignorar Archivos:

> - Se puede crear un archivo .gitignore para indicar a Git qué archivos ignorar.
> - Las reglas para los patrones en .gitignore incluyen ignorar líneas en blanco, emplear patrones globales estándar y negar patrones si es necesario.

- Confirmar tus Cambios:

> - Después de preparar los archivos, se realiza una confirmación con git commit -m "mensaje".
> - La confirmación incluye información sobre la rama, el identificador de confirmación, los archivos modificados y estadísticas sobre las líneas añadidas y eliminadas.

- Eliminar Archivos:

> - Para eliminar archivos de Git, se usa git rm, que también elimina el archivo del directorio de trabajo.
> - Si se elimina un archivo sin usar git rm, aparecerá como "Cambios no preparados para confirmar" en git status.

- Ver el Historial de Confirmaciones:

> - git log muestra el historial de confirmaciones, incluyendo el identificador de confirmación, autor, fecha y mensaje de confirmación.
> - Por defecto, git log lista las confirmaciones en orden cronológico inverso.

### El dia siguiente se vera :

> - Ver el Historial de confirmaciones -- Extras
> - Limitar la Salida del Historial
> - Deshacer Cosas
> - Deshacer un Archivo Preparado
> - Deshacer un Archivo Modificado
> - Trabajar con Remotos
> - Ver Tus Remotos
