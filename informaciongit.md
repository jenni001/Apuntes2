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
6. git log --oneline: para mostrar la historia de commits
7. git resert --hard: volver a una version anterior de commit, moverse a otra version
8. git push:  subir al repositorio
9. git remote : para sincronizar con otros repositorios remotos
10. git pull: para importar cambios de otro repositorio remoto

 ## Formateo de código:

Se puede observar, que en cuanto escribimos algo con forma de código, *Visual Studio Code* lo resalta en función de como lo escribimos:

        echo `Hola`


`hola` --> cuando se trata de un comando

</br>

```hola``` --> para marcar un idioma de programación

<br>
<br>
<brS>   


La siguiente _página web_ contiene información muy útil en cuanto a los comandos para git:

https://gist.github.com/dasdo/9ff71c5c0efa037441b6

https://github.com/JJ/aprende-git


