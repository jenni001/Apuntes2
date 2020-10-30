 # Información git

 Git es un sistema de control de versiones distribuido, gratuito y de código abierto. Diseñado por Linus Torvalds, pensando en la eficiencia y la confiabilidad del mantenimiento de versiones de aplicaciones cuando éstas tienen un gran número de archivos de código fuente. Su objetivo es llevar registro de los cambios en archivos de computadora y coordinar el trabajo que varias personas realizan sobre archivos compartidos, llevando a cabo un seguimiento del progreso de diversos proyectos en el caso de las empresas.
  
 En este *documento MD* redactaré un listado de comandos que deben utilizarse por consola en **comandos git**:

 ## Comandos git:

1. git init: para iniciar el git en la carpeta en la que esta el proyecto.
2. git clone *url*: para clonar un repositorio.
3. git status (-s): para ver el estado de todos los archivos (señala si alguno esta modificado), la versiones.
4. git add (. / un fichero en particular / *.txt): añadir los archivos para el commit.
   * add . : para añadir todos los archivos al commit.
   * add archivo.txt : un archivo en particular.
   * add *.txt : todos los archivos con esa extensión solamente.
   * add --all : todos los archivos excepto los nuevos.
   * add directorio/ : todos los archivos de un directorio determinado.
   * add directorio/*.txt : todos los archivos de un directorio determinado con esa extensión solamente.
5. git commit -m "comentario": para realizar el commit con comentario.
   * git commit --amend -m "nuevo comentario commit": para cambiar el mensaje del último commit.
6. git log --oneline: para mostrar el historial de commits.
   * git log --graph --oneline : para mostrar el historial de commits pero más grafico y especifico.
7. git diff: para observar los cambios que se han realizado.
8. git rebase -i HEAD~cantidad_commit: cuando queremos cambiar mensajes de varios commits anteriores ya ejecutados (ejemplo:git rebase -i HEAD~3). Este comando muestra un editor de texto donde tenemos que cambiar *pick* por *edit* en los mensajes de los commits que deseamos cambiar, guardamos y después ejecutamos los siguientes comandos (para salir :qa!):
   * git commit --amend -m "Nuevo mensaje": anteriormente visto para cambiar el mensaje commit.
   * git rebase --continue : para pasar al siguiente.
   * git push --force : para subir.
   * git rebase --abort: para retroceder si se han cambiado o eliminado los commits al señalar para cambiar erroneamente.

   ![Una imagen de ejemplo de rebase en unificación de ramas](https://wac-cdn.atlassian.com/dam/jcr:e4a40899-636b-4988-9774-eaa8a440575b/02.svg?cdnVersion=1316)

9. git reset : volver a una version anterior de commit, moverse a otra version.
   * git reset --soft: sin modificar el índice de archivos ni el contenido local, genera un reset de HEAD hacia otro commit, haciendo que los archivos agregados o eliminados y los cambios producidos durante los commits reseteados se mantengan en el contenido local  (modifica el head pero no el índice de datos ni el contenido local).
   * git reset --mixed: modifica el HEAD y el índice de archivos pero no el contenido local, haciendo que cualquier archivo insertado o eliminado dentro de los commits reseteados no se agrege en el índice de commits futuros (modifica el head y el índice de datos pero no el contenido local).
   * git reset --hard: modifica el HEAD, el índice de archivos y el contenido local, haciendo que el estado del proyecto sea equivalente al que se encontraba el commit al que se ha reseteado (modifica el head, el índice de datos y el contenido local).
10. git revert: se utiliza para deshacer cambios efectuados en el historial de confirmaciones de un repositorio, tomando una confirmación especificada, sin mover los punteros de referencia a esta confirmación. Este comando invierte los cambios de la confirmación y crea una "confirmación de reversión" nueva, actualizando los punteros de referencia para apuntar a la nueva confirmación de reversión, convirtiendolo en la punta de la rama.
      * git revert -e --edit: abre el editor configurado del sistema para editar el mensaje de confirmación antes de confirmar la reversión.
      * git revert --no-edit: no abre el editor configurado del sistema para editar el mensaje de confirmación antes de confirmar la reversión.
      * git revert -n --no-commit: para impedir que *git revert* cree una nueva confirmación que invierta la confirmación objetivo. De esta forma, en lugar crear la nueva confirmación, se añadirá los cambios inversos al índice del entorno de ensayo y al directorio de trabajo. 
Para entender mejor la diferencia entre git reset y git revert esta la siguiente imagen:

 ![Una imagen de la diferencia entre git reset y git revert](https://wac-cdn.atlassian.com/dam/jcr:a6a50d78-48e3-4765-8492-9e48dec8fd2f/04%20(2).svg?cdnVersion=1318)

11. git reflog: muestra un listado de todos los movimientos que se han hecho, acompañado del hash del commit de cada movimiento (incluido a los que se les ha echo reset).
12. git push:  subir al repositorio.
13. git remote : para sincronizar con otros repositorios remotos.
14. git pull: para importar cambios de otro repositorio remoto la rama en la que estemos trabajando actualmente.
15. git fetch: permite recuperar todos los ficheros de un repositorio remoto y los ubica en una rama oculta de tu repositorio local (hay que utilizar *git merge* para unificarlo en la rama que deseamos).
16. git branch x : para crear ramas nuevas si se le añade un nombra al final, *git branch* a secas, muestra las ramas existentes marcando en cual nos encontramos en ese momento.
17. git checkout x: para movernos por las ramas existentes, especificando a cual deseamos movernos.
      * git checkout -b:  crear una rama y cambiarse a ella de forma simultanea.
18. git merge x: para unificar dos ramas, ejecutando en la rama en la cual queremos unificar, indicandole cual se quiere unificar a la posicionada actual (también se puede hacer mediante rebase).
  ![Una imagen de ejemplo de mergen antes y después de la unificación de ramas](https://wac-cdn.atlassian.com/dam/jcr:91b1bdf5-fda3-4d20-b108-0bb9eea402b2/08.svg?cdnVersion=1316)
19. git tag: es para etiquetar puntos específicos del historial como importantes, especialmente para marcar versiones de lanzamiento (v1.0, por ejemplo). Lista las etiquetas en orden alfabético. 
      * git tag -a : para crear una etiqueta anotada (ejemplo, git tag -a v1.4 -m 'my version 1.4'). Se guardan en la base de datos de Git como objetos enteros. Tienen un *checksum*; contienen el nombre del etiquetador, correo electrónico y fecha; tienen un mensaje asociado; y pueden ser firmadas y verificadas con GNU Privacy Guard (GPG). También puedes etiquetar *commits* mucho tiempo después de haberlos hecho, especificando el *checksum* del commit (o parte de él, que se puede obtener mediante *git log --pretty=oneline*) al final del comando como en el siguiente ejemplo *git tag -a v1.2 9fceb02*.
      * git tag x: para crear una etiqueta ligera (ejemplo, git tag v1.4-lw). Es muy parecido a una rama que no cambia - simplemente es un puntero a un commit específico, es el checksum de un commit guardado en un archivo que no incluye más información. 
      * git tag vx.x.x -m "x": para crear una etiqueta ligera con mensaje.
      * git tag -l 'vx.x.x*': para buscar etiquetas con un patrón, si sólo te interesa ver la serie en concreto especificandolo (ejemplo *git tag -l 'v1.8.5*'*).
      * git show: para ver la información de la etiqueta junto con el commit que está etiquetado (ejemplo, *git show v1.4*).
      * git push origin [etiqueta]: para enviar las etiquetas de forma explícita al servidor tras crearlas.
      * git push origin --tags: para enviar varias etiquetas simultaneamente.

 ## Archivo gitignore:

Un archivo gitignore especifica archivos sin seguimiento intencional que Git debe ignorar. Los patrones que deben ser controlados por versiones y distribuidos a otros repositorios a través de clones (archivos que todos los desarrolladores querrán ignorar) deben ir a un .gitignore archivo.
 

 ## Formateo de código:

Se puede observar, que en cuanto escribimos algo con forma de código, *Visual Studio Code* lo resalta en función de como lo escribimos:

        echo `Hola`

- Similar pasa utilizando 'pre' : <pre>  como se puede ver con este ejemplo </pre>


- hola `hola` --> cuando se trata de un comando, añadiendole ' al principio y al final.

- El mismo es el resultado de esta <code>  forma </code> utilizando 'code'.

</br>

- ```hola``` --> para marcar un idioma de programación, añadiendole  tres ' al principio y al final.

<br>
<br>
<br>   


La siguiente _página web_ contiene información muy útil en cuanto a los comandos para git:

>[gist.github](https://gist.github.com/dasdo/9ff71c5c0efa037441b6)
<br>
>[git-scm](https://git-scm.com/)
<br>
>[github](https://github.com/JJ/aprende-git)
<br>
>[domingogallardo.github](https://domingogallardo.github.io/practicas-mads/01-intro-spring-boot/comandos-git.html)
<br>
>[bitdegree](https://es.bitdegree.org/tutoriales/tutorial-git/)

