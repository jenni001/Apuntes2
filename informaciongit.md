 # Información git
 
 En este *documento MD* redactaré un listado de comandos que deben utilizarse por consola en **comandos git**:

 ## Comandos git:

1. git init: para iniciar el git en la carpeta en la que esta el proyecto
2. git clone <url>: para clonar un repositorio
3. git status (-s): para ver el estado de todos los archivos (señala si alguno esta modificado), la versiones.
4. git add (. / un fichero en particular / *.txt): añadir los archivos para el commit
   * add . : para añadir todos los archivos al commit
   * add archivo.txt : un archivo en particular
   * add *.txt : todos los archivos con esa extensión solamente
   * add --all : todos los archivos excepto los nuevos
   * add directorio/ : todos los archivos de un directorio determinado 
   * add directorio/*.txt : todos los archivos de un directorio determinado con esa extensión solamente

5. git commit -m "comentario": para realizar el commit con comentario
6. git log --oneline: para mostrar el historial de commits
   * git log --graph --oneline : para mostrar el historial de commits pero más grafico y especifico

7. git commit --amend -m "nuevo comentario commit": para cambiar el mensaje del último commit
8. git rebase -i HEAD~cantidad_commit: cuando queremos cambiar mensajes de varios commits anteriores ya ejecutados (ejemplo:git rebase -i HEAD~3). Este comando muestra un editor de texto donde tenemos que cambiar *pick* por *edit* en los mensajes de los commits que deseamos cambiar, guardamos y después ejecutamos los siguientes comandos (para salir :qa!):
   * git commit --amend -m "Nuevo mensaje": anteriormente visto para cambiar el mensaje commit
   * git rebase --continue : para pasar al siguiente
   * git push --force : para subir 
   * git rebase --abort: para retroceder si se han cambiado o eliminado los commits al señalar para cambiar erroneamente.

9. git reset : volver a una version anterior de commit, moverse a otra version
   * git reset --soft: sin modificar el índice de archivos ni el contenido local, genera un reset de HEAD hacia otro commit, haciendo que los archivos agregados o eliminados y los cambios producidos durante los commits reseteados se mantengan en el contenido local  (modifica el head pero no el índice de datos ni el contenido local)
   * git reset --mixed: modifica el HEAD y el índice de archivos pero no el contenido local, haciendo que cualquier archivo insertado o eliminado dentro de los commits reseteados no se agrege en el índice de commits futuros (modifica el head y el índice de datos pero no el contenido local)
   * git reset --hard: modifica el HEAD, el índice de archivos y el contenido local, haciendo que el estado del proyecto sea equivalente al que se encontraba el commit al que se ha reseteado (modifica el head, el índice de datos y el contenido local)

10. git reflog: muestra un listado de todos los movimientos que se han hecho, acompañado del hash del commit de cada movimiento (incluido a los que se les ha echo reset)
11. git push:  subir al repositorio
12. git remote : para sincronizar con otros repositorios remotos
13. git pull: para importar cambios de otro repositorio remoto
14. git branch x : para crear ramas nuevas si se le añade un nombra al final, *git branch* a secas, muestra las ramas existentes marcando en cual nos encontramos en ese momento.
15. git checkout X: para movernos por las ramas existentes, especificando a cual deseamos movernos.
16. git merge x: para unificar dos ramas, ejecutando en la rama en la cual queremos unificar, indicandole cual se quiere unificar a la posicionada actual.


 

 ## Formateo de código:

Se puede observar, que en cuanto escribimos algo con forma de código, *Visual Studio Code* lo resalta en función de como lo escribimos:

        echo `Hola`


`hola` --> cuando se trata de un comando

</br>

```hola``` --> para marcar un idioma de programación

<br>
<br>
<br>   


La siguiente _página web_ contiene información muy útil en cuanto a los comandos para git:

https://gist.github.com/dasdo/9ff71c5c0efa037441b6
https://git-scm.com/
https://github.com/JJ/aprende-git
https://domingogallardo.github.io/practicas-mads/01-intro-spring-boot/comandos-git.html


