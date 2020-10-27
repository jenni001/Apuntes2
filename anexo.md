 # Anexo

En este *documento MD* redactaré un listado de las 10 preguntas más interesantes encontradas en la dirección  https://es.stackoverflow.com/questions/tagged/git?tab=Votes:

 ## Preguntas y respuestas:

 1. ¿Cuál es la diferencia entre pull y fetch en git?
 **git pull** baja los cambios  de la rama deseada del repositorio remoto y actualiza en la rama del repositorio local.
 **git fetch** baja los cambios del repositorio remoto, pero los deja en otro *branch* (una rama oculta llamada *origin/master*, que se puede visualizar mediante  **git branch -a**. Para incluir luego en la rama local, se puede pasar a la rama *master* mediante **git merge origin/master**, hasta que se hace el **git merge** para traerlos al *branch* local.

 Para comprender esto de forma visual:
 ![Una imagen de ejemplo visual de como avanzan los pasos](https://i.stack.imgur.com/fUk4f.png)

 Por ello, si se ejecuta directamente **git pull**, se esta combinando lo que hacen **git fetch** y **git merge** juntos, (en el caso anterior **git pull origin master**), por lo cual, es una forma de ahorrarse comandos. 
 
 2. ¿Cuál es la diferencia entre 'git rebase' y 'git merge'?

 Ambos son comandos para incorporar cambios de diversas personas en una misma rama.

 Para entender mejor la diferencia, se explicará con ejemplos. Como vemos en la imagen, partiendo del mismo punto (commit C), dos personas crean diferentes commits (D y E). Esto crea un conflicto que puede resolverse de dos formas, para fusionar los commits:

 ![Estado de una rama con diversos commits](https://i.stack.imgur.com/pK7Zb.png)

- Merge: los dos commits están ahí, obteniendo en el historial una forma de diamante, pero se crea un commit de unión *merge commit* (M), para fusionar ambos (D y E), heredando asi los cambios de ambos.
De esta forma juntas el historial de ambas ramas, y si se hace de forma continuada, se creará una serie de historiales intercalados que puede resultar más lioso.


![Merge](https://i.stack.imgur.com/9Ul5w.png)

- Rebase: se crea un commit de unión *rebase commit* (R), que hará que se herede los cambios de ambos commits (D y E), obteniendo el mismo contenido que con el M. Sin embargo, en este caso se elimina el commit E, volviendo a tomar la forma lineal del historial, como si el commit E nunca hubiera existido.
De esta forma, los cambios se realizan de forma limpia, como si se hubiera cambiado de rama mediante *checkout* de forma limpia y después empezaste a trabajar desde allí. Esto mantendrá limpio y simple a la hora de que otra persona quiera revisar el historial, aún realizando nuevos cambios en la rama.

![Rebase](https://i.stack.imgur.com/9Ul5w.png)

Un ejemplo de una comparacion final en este tipo de conflictos seria el siguiente (izquierda merge y derecha rebase):

![Comparacion](https://i.stack.imgur.com/LF8Ys.png)

3. ¿Cómo ver qué archivos son diferentes entre 2 ramas con Git?

Esta duda tiene tres soluciones posibles:

- Archivo por archivo:

        $ git diff branch1 branch2    (1)
    Muestra los cambios entre branch1 y branch2.

        $ git diff branch1..branch2   (2)
    Muestra lo mismo que en la anterior.

En esta imagen se puede ver el resultado que se mostraria al ejecutar los anteriores comandos: 
![1 y 2](https://i.stack.imgur.com/GTxAw.png)

        $ git diff branch1...branch2  (3)  

    Muestra los cambios realizados en la rama branch2 desde que la branch1 comenzó fuera de esa. En la siguiente imagen se puede observar el resultado de este comando:
![3](https://i.stack.imgur.com/nxpg4.png)

- Por listado:

Para obtener un listado de los archivos, estarian los siguientes comandos:

--stat: Muestra una diferencia a nivel binario.

        $ git diff --stat branch1 branch2

![--stat](https://i.stack.imgur.com/9q4qA.png)

--numstat: Muestra en número base decimal las diferencias en líneas.

        $ git diff --numstat branch1 branch2

![--numstat](https://i.stack.imgur.com/9q4qA.png)

- Herramientas adicionales

Si se le añade el argumento --name-status, se obtiene un listado de los archivos que han cambiado entre 2 ramas:

        $ git diff --name-status branch1..branch2

Para verificar los cambios de un archivo entre 2 ramas:

        $ git diff branch1 branch2 -- archivo.ext

4. 
