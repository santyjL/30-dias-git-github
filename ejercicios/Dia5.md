# Ver el Historial de Confirmaciones

El comando git log proporciona gran cantidad de opciones para mostrarte exactamente
lo que buscas. Aquí veremos algunas de las más usadas.

Una de las opciones más útiles es **-p**, que muestra las diferencias introducidas en cada
confirmación. También puedes usar la opción **-2**, que hace que se muestren únicamente
las dos últimas entradas del historial:

```java
$ git log -p -2
commit ca82a6dff817ec66f44342007202690a93763949
Author: Scott Chacon <schacon@gee-mail.com>
Date: Mon Mar 17 21:52:11 2008 -0700
  changed the version number
diff --git a/Rakefile b/Rakefile
index a874b73..8f94139 100644
--- a/Rakefile
+++ b/Rakefile
@@ -5,7 +5,7 @@ require 'rake/gempackagetask'
 spec = Gem::Specification.new do |s|
  s.platform = Gem::Platform::RUBY
  s.name = "simplegit"
- s.version = "0.1.0"
+ s.version = "0.1.1"
  s.author = "Scott Chacon"
  s.email = "schacon@gee-mail.com"
  s.summary = "A simple gem for using Git in Ruby code."
commit 085bb3bcb608e1e8451d4b2432f8ecbe6306e7e7
Author: Scott Chacon <schacon@gee-mail.com>
Date: Sat Mar 15 16:40:33 2008 -0700
  removed unnecessary test
diff --git a/lib/simplegit.rb b/lib/simplegit.rb
index a0a60ae..47c6340 100644
--- a/lib/simplegit.rb
+++ b/lib/simplegit.rb
@@ -18,8 +18,3 @@ class SimpleGit
  end
 end
-
-if $0 == __FILE__
- git = SimpleGit.new
- puts git.show
-end
\ No newline at end of file
```

Esta opción muestra la misma información, pero añadiendo tras cada entrada las
diferencias que le corresponden. Esto resulta muy útil para revisiones de código, o para
visualizar rápidamente lo que ha pasado en las confirmaciones enviadas por un
colaborador.

También puedes usar con **git log** una serie de opciones de resumen. Por
ejemplo, si quieres ver algunas estadísticas de cada confirmación, puedes usar la opción
**--stat**

```java
$ git log --stat
commit ca82a6dff817ec66f44342007202690a93763949
Author: Scott Chacon <schacon@gee-mail.com>
Date: Mon Mar 17 21:52:11 2008 -0700
  changed the version number
 Rakefile | 2 +-
 1 file changed, 1 insertion(+), 1 deletion(-)
commit 085bb3bcb608e1e8451d4b2432f8ecbe6306e7e7
Author: Scott Chacon <schacon@gee-mail.com>
Date: Sat Mar 15 16:40:33 2008 -0700
  removed unnecessary test
 lib/simplegit.rb | 5 -----
 1 file changed, 5 deletions(-)
commit a11bef06a3f659402fe7563abf99ad00de2209e6
Author: Scott Chacon <schacon@gee-mail.com>
Date: Sat Mar 15 10:31:28 2008 -0700
  first commit
 README | 6 ++++++
 Rakefile | 23 +++++++++++++++++++++++
 lib/simplegit.rb | 25 +++++++++++++++++++++++++
 3 files changed, 54 insertions(+)
```

Como puedes ver, la opción --stat imprime tras cada confirmación una lista de archivos
modificados, indicando cuántos han sido modificados y cuántas líneas han sido añadidas
y eliminadas para cada uno de ellos, y un resumen de toda esta información.

Otra opción realmente útil es **--pretty**, que modifica el formato de la salida. Tienes
unos cuantos estilos disponibles. La opción oneline imprime cada confirmación en una
única línea, lo que puede resultar útil si estás analizando gran cantidad de
confirmaciones. Otras opciones son **short**, **full** y **fuller**, que muestran la salida en un
formato parecido, pero añadiendo menos o más información, respectivamente:

```java
$ git log --pretty=oneline
ca82a6dff817ec66f44342007202690a93763949 changed the version number
085bb3bcb608e1e8451d4b2432f8ecbe6306e7e7 removed unnecessary test
a11bef06a3f659402fe7563abf99ad00de2209e6 first commit
```

La opción más interesante es format, que te permite especificar tu propio formato. Esto
resulta especialmente útil si estás generando una salida para que sea analizada por otro
programa:

```java
$ git log --pretty=format:"%h - %an, %ar : %s"
ca82a6d - Scott Chacon, 6 years ago : changed the version number
085bb3b - Scott Chacon, 6 years ago : removed unnecessary test
a11bef0 - Scott Chacon, 6 years ago : first commit
```

lista algunas de las opciones más útiles aceptadas por **format**.
![log--pretty:format](/imagenes/opciones%20de%20log%20--pretty-format%20-%20dia%20cinco.jpg)

Las opciones **oneline** y **format** son especialmente útiles combinadas con otra opción
llamada **--graph**. Ésta añade un pequeño gráfico **ASCII** mostrando tu historial de
ramificaciones y uniones:

```java
$ git log --pretty=format:"%h %s" --graph
* 2d3acf9 ignore errors from SIGCHLD on trap
* 5e3ee11 Merge branch 'master' of git://github.com/dustin/grit
|\
| * 420eac9 Added a method for getting the current branch.
* | 30e367c timeout code and tests
* | 5a09431 add timeout protection to grit
* | e1193f8 support for heads with slashes in them
|/
* d6016bc require time for xmlschema
* 11d191e Merge branch 'defunkt' into local
```

las opciones vistas hasta ahora, y algunas
otras opciones de formateo que pueden resultarte útiles, así como su efecto sobre la
salida.

![log--pretty:format](/imagenes/opciones%20de%20log%20-%20dia%20cinco.jpg)

## Limitar la Salida del Historial

Además de las opciones de formateo, **git log** acepta una serie de opciones para limitar
su salida —es decir, opciones que te permiten mostrar únicamente parte de las
confirmaciones—. Ya has visto una de ellas, la opción **-2**, que muestra sólo las dos
últimas confirmaciones. De hecho, puedes hacer **-<n>**, siendo **n** cualquier entero, para
mostrar las últimas **n** confirmaciones.

Sin embargo, las opciones temporales como **--since** (desde) y **--until** (hasta) sí que
resultan muy útiles. Por ejemplo, este comando lista todas las confirmaciones hechas
durante las dos últimas semanas:

```java
$ git log --since=2.weeks
```

Este comando acepta muchos formatos. Puedes indicar una fecha concreta ("2008-01-15"),
o relativa, como "2 years 1 day 3 minutes ago"

También puedes filtrar la lista para que muestre sólo aquellas confirmaciones que
cumplen ciertos criterios. La opción **--author** te permite filtrar por autor, y **--grep** te
permite buscar palabras clave entre los mensajes de confirmación. (Ten en cuenta que si
quieres aplicar ambas opciones simultáneamente, tienes que añadir **--all-match**, o el
comando mostrará las confirmaciones que cumplan cualquiera de las dos, no
necesariamente las dos a la vez.)

![Limitar la salida del historial](/imagenes/opciones%20para%20limitar%20salida%20con%20log%20-%20dia%20cinco.jpg)

Por ejemplo, si quieres ver cuáles de las confirmaciones hechas sobre archivos de
prueba del código fuente de Git fueron enviadas por Junio Hamano, y no fueron
uniones, en el mes de octubre de 2008, ejecutarías algo así:

```java
$ git log --pretty="%h - %s" --author=gitster --since="2008-10-01" \
  --before="2008-11-01" --no-merges -- t/
5610e3b - Fix testcase failure when extended attributes are in use
acd3b9e - Enhance hold_lock_file_for_{update,append}() API
f563754 - demonstrate breakage of detached checkout with symbolic link HEAD
d1a43f2 - reset --hard/read-tree --reset -u: remove unmerged new paths
51a94af - Fix "checkout --track -b newbranch" on detached HEAD
b0ad11e - pull: allow "git pull origin $something:$current_branch" into an unborn
branch
```

## Deshacer Cosas

En cualquier momento puede que quieras deshacer algo. Aquí repasaremos algunas
herramientas básicas usadas para deshacer cambios que hayas hecho. Ten cuidado, a
veces no es posible recuperar algo luego que lo has deshecho. Esta es una de las pocas
áreas en las que Git puede perder parte de tu trabajo si cometes un error.

Uno de las acciones más comunes a deshacer es cuando confirmas un cambio antes de
tiempo y olvidas agregar algún archivo, o te equivocas en el mensaje de confirmación.
Si quieres rehacer la confirmación, puedes reconfirmar con la opción --amend:

```java
$ git commit --amend
```

Este comando utiliza tu área de preparación para la confirmación. Si no has hecho
cambios desde tu última confirmación , entonces la instantánea lucirá exactamente igual y lo único
que cambiarás será el mensaje de confirmación.

Por ejemplo, si confirmas y luego te das cuenta que olvidaste preparar los cambios de
un archivo que querías incluir en esta confirmación, puedes hacer lo siguiente:

```java
$ git commit -m 'initial commit'
$ git add forgotten_file
$ git commit --amend
```

Al final terminarás con una sola confirmación - la segunda confirmación reemplaza el
resultado de la primera.

### Deshacer un Archivo Preparado

el comando que usas para determinar el estado de esas dos áreas también te recuerda cómo deshacer los cambios
en ellas. Por ejemplo, supongamos que has cambiado dos archivos y que quieres
confirmarlos como dos cambios separados, pero accidentalmente has escrito **git add .** y
has preparado ambos. ¿Cómo puedes sacar del área de preparación uno de ellos? El
comando **git status** te recuerda cómo:

```java
$ git add .
$ git status
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)
  renamed: README.md -> README
  modified: CONTRIBUTING.md
```

Justo debajo del texto “Changes to be committed” (“Cambios a ser confirmados”, en
Español), verás que dice que uses **git reset HEAD <file>**... para deshacer la preparación.
Por lo tanto, usemos el consejo para deshacer la preparación del archivo CONTRIBUTING.md:

```java
$ git reset HEAD CONTRIBUTING.md
Unstaged changes after reset:
M CONTRIBUTING.md
$ git status
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)
  renamed: README.md -> README
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)
  modified: CONTRIBUTING.md
```

git reset puede ser un comando peligroso, especialmente si lo llamas con
la opción --hard.

### Deshacer un Archivo Modificado

¿Qué tal si te das cuenta que no quieres mantener los cambios del archivo
CONTRIBUTING.md? ¿Cómo puedes restaurarlo fácilmente - volver al estado en el que estaba
en la última confirmación ? Afortunadamente, git status también te dice cómo
hacerlo.

```java
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)
  modified: CONTRIBUTING.md

```

Allí se te indica explícitamente como descartar los cambios que has hecho. Hagamos lo
que nos dice:

```java
$ git checkout -- CONTRIBUTING.md
$ git status
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)
  renamed: README.md -> README
```

Es importante entender que **git checkout -- [archivo]** es un
comando **peligroso**. Cualquier cambio que le hayas hecho a ese
archivo desaparecerá - acabas de sobreescribirlo con otro archivo.
Nunca utilices este comando a menos que estés absolutamente
seguro de que ya no quieres el archivo.

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

## Ver Tus Remotos

Para ver los remotos que tienes configurados, debes ejecutar el comando git remote.
Mostrará los nombres de cada uno de los remotos que tienes especificados. Si has
clonado tu repositorio, deberías ver al menos origin (origen, en español) - este es el
nombre que por defecto Git le da al servidor del que has clonado:

```java
$ git clone https://github.com/schacon/ticgit
Cloning into 'ticgit'...
remote: Reusing existing pack: 1857, done.
remote: Total 1857 (delta 0), reused 0 (delta 0)
Receiving objects: 100% (1857/1857), 374.35 KiB | 268.00 KiB/s, done.
Resolving deltas: 100% (772/772), done.
Checking connectivity... done.
$ cd ticgit
$ git remote
origin
```

También puedes pasar la opción **-v**, la cual muestra las URLs que Git ha asociado
al nombre y que serán usadas al leer y escribir en ese remoto:

Si tienes más de un remoto, el comando los listará todos. Por ejemplo, un repositorio
con múltiples remotos para trabajar con distintos colaboradores podría verse de la
siguiente manera.

```java
$ cd grit
$ git remote -v
bakkdoor https://github.com/bakkdoor/grit (fetch)
bakkdoor https://github.com/bakkdoor/grit (push)
cho45 https://github.com/cho45/grit (fetch)
cho45 https://github.com/cho45/grit (push)
defunkt https://github.com/defunkt/grit (fetch)
defunkt https://github.com/defunkt/grit (push)
koke git://github.com/koke/grit.git (fetch)
koke git://github.com/koke/grit.git (push)
origin git@github.com:mojombo/grit.git (fetch)
origin git@github.com:mojombo/grit.git (push)
```

## Resumen :

- Comando git log:

> - Proporciona varias opciones para visualizar el historial de confirmaciones.
>   -Las opciones más útiles incluyen -p para mostrar diferencias introducidas, y -2 para ver las dos últimas entradas del historial.
> - --stat muestra estadísticas de cada confirmación, como archivos modificados, líneas añadidas y eliminadas.
> - --pretty modifica el formato de salida, con opciones como oneline y format.
> - --graph muestra un pequeño gráfico ASCII del historial de ramificaciones y uniones.

- Limitar la salida del historial:

> - Se pueden limitar las confirmaciones mostradas usando opciones temporales como --since y --until.
> - --author y --grep permiten filtrar por autor y buscar palabras clave en los mensajes de confirmación.

- Deshacer cosas:

> - Se pueden deshacer cambios usando git commit --amend para reconfirmar con cambios adicionales.
> - git reset HEAD <file> se usa para sacar archivos del área de preparación.
> - git checkout -- <file> se usa para descartar cambios en archivos modificados.

- Trabajar con remotos:

> - git remote muestra los remotos configurados.
> - git remote -v muestra las URLs asociadas a cada remoto.

### El dia siguiente se vera :

> - Añadir Repositorios Remotos
> - Traer y Combinar Remotos
> - Enviar a Tus Remotos
> - Inspeccionar un Remoto
> - Eliminar y Renombrar Remotos
