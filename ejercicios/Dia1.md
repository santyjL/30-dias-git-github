# ¿Qué es un control de versiones, y por qué debería importarte?

Un control de versioneses un sistema que registra los cambios realizados en un
archivo o conjunto de archivos a lo largo del tiempo, de modo que puedas recuperar
versiones específicas más adelante

## control de verciones locales

![vcs & rcs](/30-dias-git-github/imagenes/vcs%20local%20-%20dia%20uno.jpg)

Una de las herramientas de control de versiones más popular fue un sistema llamado
RCS, que todavía podemos encontrar en muchas de las computadoras actuales. Incluso el
famoso sistema operativo Mac OS X incluye el comando rcs cuando instalas las
herramientas de desarrollo. Esta herramienta funciona guardando conjuntos de parches
(es decir, las diferencias entre archivos) en un formato especial en disco, y es capaz de
recrear cómo era un archivo en cualquier momento a partir de dichos parches

## Sistemas de Control de Versiones Centralizados

![cvcs](/30-dias-git-github/imagenes/cvcs%20centralizados%20-%20dia%20uno.jpg)

El siguiente gran problema con el que se encuentran las personas es que necesitan
colaborar con desarrolladores en otros sistemas. Los sistemas de Control de Versiones
Centralizados (CVCS por sus siglas en inglés) fueron desarrollados para solucionar este
problema. Estos sistemas, como CVS, Subversion y Perforce, tienen un único servidor que
contiene todos los archivos versionados y varios clientes que descargan los archivos
desde ese lugar central. Este ha sido el estándar para el control de versiones por
muchos años.

ofrece muchas ventajas, especialmente frente a VCS locales. Por
ejemplo, todas las personas saben hasta cierto punto en qué están trabajando los otros
colaboradores del proyecto. Los administradores tienen control detallado sobre qué puede
hacer cada usuario, y es mucho más fácil administrar un CVCS que tener que lidiar con
bases de datos locales en cada cliente.

Sin embargo, esta configuración también tiene serias desventajas. La más obvia es el
punto único de fallo que representa el servidor centralizado. Si ese servidor se cae
durante una hora, entonces durante esa hora nadie podrá colaborar o guardar cambios
en archivos en los que hayan estado trabajando.

## Sistemas de Control de Versiones Distribuidos

![vcs & rcs](/30-dias-git-github/imagenes/dvcs%20distribuidas%20-%20dia%20uno.jpg)

Los sistemas de Control de Versiones Distribuidos (DVCS por sus siglas en inglés) ofrecen
soluciones para los problemas que han sido mencionados. En un DVCS (como Git,
Mercurial, Bazaar o Darcs), los clientes no solo descargan la última copia instantánea de
los archivos, sino que se replica completamente el repositorio. De esta manera, si un
servidor deja de funcionar y estos sistemas estaban colaborando a través de él,
cualquiera de los repositorios disponibles en los clientes puede ser copiado al servidor
con el fin de restaurarlo. Cada clon es realmente una copia completa de todos los
datos.

## En resumen :

- Control de Versiones:
  > - Sistema para registrar y gestionar cambios en archivos a lo largo del tiempo.
- Control de Versiones Locales:
  > - Utiliza herramientas como RCS para almacenar conjuntos de parches.
  > - Permite reconstruir archivos a partir de cambios registrados en disco.
- Sistemas de Control de Versiones Centralizados (CVCS):
  > - CVS, Subversion y Perforce son ejemplos.
  > - Un servidor central almacena archivos versionados.
  > - Los clientes descargan archivos del servidor central.
  > - Ventajas: visibilidad del trabajo de otros, control de permisos.
  > - Desventajas: riesgo de fallo único del servidor central.
- Sistemas de Control de Versiones Distribuidos (DVCS):
  > - Git, Mercurial, Bazaar, Darcs son ejemplos.
  > - Cada cliente tiene una copia completa del repositorio.
  > - Mayor independencia y flexibilidad en el desarrollo.
  > - Elimina el riesgo de fallo único del servidor central.
