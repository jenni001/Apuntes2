 # Anexo

En este *documento MD* redactaré un listado de las 10 preguntas más interesantes encontradas en la siguiente [ubicación]( https://es.stackoverflow.com/questions/tagged/git?tab=Votes):

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

        git diff branch1 branch2    (1)

Muestra los cambios entre branch1 y branch2.

        git diff branch1..branch2   (2)

Muestra lo mismo que en la anterior.

En esta imagen se puede ver el resultado que se mostraria al ejecutar los anteriores comandos: 
![1 y 2](https://i.stack.imgur.com/GTxAw.png)

        git diff branch1...branch2  (3)  
Muestra los cambios realizados en la rama branch2 desde que la branch1 comenzó fuera de esa. En la siguiente imagen se puede observar el resultado de este comando:
![3](https://i.stack.imgur.com/nxpg4.png)

- Por listado:

Para obtener un listado de los archivos, estarian los siguientes comandos:

--stat: Muestra una diferencia a nivel binario.

        git diff --stat branch1 branch2

![--stat](https://i.stack.imgur.com/9q4qA.png)

--numstat: Muestra en número base decimal las diferencias en líneas.

        git diff --numstat branch1 branch2

![--numstat](https://i.stack.imgur.com/9q4qA.png)

- Herramientas adicionales

Si se le añade el argumento --name-status, se obtiene un listado de los archivos que han cambiado entre 2 ramas:

        git diff --name-status branch1..branch2

Para verificar los cambios de un archivo entre 2 ramas:

        git diff branch1 branch2 -- archivo.ext

4.  ¿Como cambiar la fecha de un commit antes de hacer 'git push'?

Lo que hay que hacer, es cambiarle la fecha del commit (local) antes de realizar el push, utilizando *git commit --amend --date=" "*, como en el siguiente ejemplo:

        git commit --amend --date="Wed Feb 16 14:00 2011 +0100"

Con el ejemplo anterior se cambia la fecha al dia que queramos. En caso de que simplemente queramos cambiarla al momento (día, fecha, hora...) del momento presente, con la siguiente linea bastaria (modifica el último commit):

        git commit --amend --reset-author --no-edit

En caso de querer modificar un commit más antiguo, hay que utilizar un rebase interactivo, cambiando a *edit* el commit que se desea modificar. Para ello hay que utilizar:
        
        git rebase -i <ref>

Tras seleccionar el commit deseado, solo hay que utilizar el comando anterior para cambiar la fecha a la actual (*git commit --amend --reset-author --no-edit*).

Una vez hecho el cambio, para pushear solo algunos commits, se utiliza la siguiente sintaxis:

        git push <remoto> <SHA del commit>:<branch>

5. Quitar archivos añadidos antes de un commit

Para quitarlos del index solamente hay que utilizar el siguiente comando:

        git reset <paths>

De esta forma se restable las entradas del index para los paths (archivo) que indiquemos a su correspondiente estado, como seria el "working tree" (el directorio de trabajo). Con *git reset* se elimina el/los archivos del "index", quedando únicamente el original en el working tree. Es decir, haciendo con *git reset <paths>*  lo opuesto a *git add <paths>*.

6. ¿Para qué es el branch “gh-pages” que aparece en muchos repos de GitHub?

Github da la posibilidad de generar un sitio web a partir de una organización o proyecto, útil para portafolios, blogs y todo tipo de páginas del lado del front-end (totalmente gratis).Esto se hace mediante la rama *gh-pages*.  Es de manera gratuita y con repositorios ilimitados, pero no se puede usar código del lado del servidor (Python, Ruby, PHP, etc.).   
Sin embargo, si sólo se quiere mostrar un proyecto (Front-end), GitHub Pages es una buena opción, sin necesidad de comprar y/o usar un dominio.
Una buena página para documentarse sobre esto es la de [platzi](https://platzi.com/blog/github-pages/).

La creacion de esta rama se lleva a cabo de la siguiente forma:

- Posicionados dentro de la carpeta del proyecto:

        git branch gh-pages

- De esta forma se crea la rama(branch) gh-pages en el proyecto. Después únicamente hay que subirlo al repositorio remoto(Github) haciendo un push:

        git push origin gh-pages


7. ¿Cómo averiguar la procedencia de una rama determinada?

Con hacer un checkout a la rama en cuestión y luego ejecutando el siguiente comando, se podra identificar:

        git log --oneline --decorate --all --graph

Un ejemplo seria el siguiente:

![Ejemplo resultado](https://i.stack.imgur.com/P2482.png)

8. Pull a un branch remoto que no existe en mi local

Primero hay que hacer un fetch:

        git fetch <remoto> <rama>

Fetch trae la rama remota y la almacena dentro de *<"remoto"> /<"rama">*.

Pull es una combinación de fetch+merge, por ello, cuando se haga el fetch hay que hacer checkout a esa rama dentro del remoto sin mezclarla con alguna local y luego, hacer merge. Otra opción sería crear una rama localmente, hacer checkout a esa rama y luego hacer pull de la rama remota.

El problema con pull es que hace tanto el fetch como un merge automático de esa rama a la rama donde está situado actualmente.

Como ejemplo para resolver esta duda estaria el siguiente: 

        git fetch feature validateEmail

Posteriormente, para entrar a esa rama remota:

        git checkout feature/validateEmail

Luego únicamnete quedaria realizar los cambios que se necesiten y hacer merge con master o con cualquier otra rama.

9. ¿Cómo puedo deshacer el último commit en Git?

Si se quiere mantener los cambios en el working tree para que puedan ser modificados luego:

        git reset [--mixed] HEAD~1

No modifica ni el working tree ni el index. Además de mantener los cambios, no se desea eliminar el commit, sólo mover el head al anterior:

        git reset --soft HEAD~1

Si no se quiere mantener los cambios, solo volver al estado del commit anterior revirtiendo el index y el working tree y destruyendo el último commit completamente como si nunca hubiera existido:

        git reset --hard HEAD~1

10. Git me pide contraseña cada vez que envío a Github

Hay que ejecutar la siguiente linea:

        git config --global credential.helper wincred

Esto hará que se solicite las credenciales una vez, quedando cacheadas para futuras operaciones.

11. ¿Para qué se usan los tags en Git?

Cada vez que se realiza un *commit*, se crea un identificador único (ejemplo, 0dc20efa9ec36cefd67dcb832d9b01b7531c3a33), y a pesar de que se ponga un comentario al commit, no resulta fácil consultarlo, por lo cual se puede crear una etiqueta que en el futuro facilite el acceso a él de forma rápida. Sirven para dejar un registro, una marca de una versión en concreto, creandose cuando publicas una versión (v0.1, v1.0, v2.2, etc.) de modo que se pueda volver a dicha versión. Si se crea una etiqueta, se puede obtener el código con un *git checkout* (ejemplo, etiqueta v1.0.0, *git checkout* v1.0.0).  
Moverse por un tag es similar a moverse por una rama, pero en modo *detached*, es decir, no se puede modificar el código y hacer un commit salvo creando una rama, pues lo que se tiene es un snapshot, una instantánea del código en un momento dado.