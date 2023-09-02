Documentación
https://git-scm.com/doc

git --version  (-- significa que sigue un nombre completo, a un sólo guión le sigue abreviaturas)
git help (doc general)
ejemplo
git help commit  (los dos puntos al final significa que hay mas contenido y con las fleas puedes ver, tecla q para salir)
git config --global user.name "Alfredo Aquino"
git config --global user.email "alfaquino@gmail.com"

git config --global -e (para comprobar, muestra la rama por defecto) para salir :q! enter
y para salir esc + :wq!  (w sólo si queremos grabar)

En windows se aconseja trabajar con Power Shell o Git Bash

git init  (Inicializa el repositorio) con la rama principal master que en el futuro podría ser main

git config --global init.defaultBranch nuevo_nombre  (para que en adelante siempre cree con cierto nombre la rama principal)

git status (da información de la rama en la que nos encontremos)

git add nombre_archivo (es el paso inicial para poder hacerles commit, y se puede hacer por archivo, es indicar que haremos seguimiento
	 los archivos ya están en el stage )

git add .  (añade todo)
git reset nombre_archivo (si queremos removerlo del stage)

git commit -m "Primer commit"

git checkout -- .  (le dice a git reconstruye el proyecto a como estaba en el último commit)
git branch   (muestra todas las ramas, y pone un asterisco y de otro color la rama en la que estoy trabajando)

cambiar nombre de la rama de master a main
git branch -m master main

para no hacer un add luego commit se puede hacer esto en una sóla línea para archivos que ya hayan sido agregados al menos
una vez o sea que no sean UNTRACKED

git commit -am "Readme actualizado"

git log (para ver los commits historial)

para ver la  vista Source Control en VSC se debe instalar el activitus bar

para usar git add con ciertos filtros pero los busca en la ruta actual

git add index.html main.html
git add *.html
git add js/*.js

cuando tenemos una carpeta vacía Git no lo toma en cuenta pero si queremos que la tome en cuenta dentro creamos un archivo:
.gitkeep

git add css/  (agrega todo lo que está en la carpeta y subcarpetas)

git status --short  (+ resumdo)

Alias (como git s me devuelve desconocido entonces puedo usarlo)
git config --global alias.s "status --short"

para modificar alias
git config --global -e (tecla A para hacer la modificación) -----------------------------------------------------------
:wq!  (para salir grabando)

git log --oneline (resumido)
git log --oneline --decorate --all --graph  (más banderas)
documentacion:  https://git-scm.com/

abreviaturas:
https://gist.github.com/Klerith/0acf18bbece7923bcac55edb71b03c2b

--alias personalizado para git log => git lg
git config --global alias.lg "log --graph --abbrev-commit --decorate --format=format:'%C(bold blue)%h%C(reset) - %C(bold green)(%ar)%C(reset) %C(white)%s%C(reset) %C(dim white)- %an%C(reset)%C(bold yellow)%d%C(reset)' --all"

git diff (para ver las diferencias, puedo especificar qué archivos también)

git diff --staged (para cuando no muestra nada porque lo compara con los cambios que no estén en el stage) pero es mejor ver el diff en el mismo VSCode

git commit -am "instalaciones actualiz"  (para agregar al stage y commit)
para modificar el mensaje del commit
git commit --amend -m "Instalaciones actualizadas"  (es para el último commit) (si no le pones el -m se abre en modo edición, tecla A para insertar)

ahora si quiero que mis últimas modificaciones sean partes del commit anterior

git reset --soft HEAD^  (--soft --hard  hard:sí elimina los cambios, el HEAD apunta al último commit
			 HEAD^2 HEAD^3 HEAD^4 si quiero commits anteriores)
			en lugar del HEAD podemos poner el hash del commit
git reset --soft HEAD^  (muéveme al commit antes de el HEAD y ya no aparece el último commit) 

si aparece warning de LF will be replaced by CRLF
git config core.autocrlf true

para agregar toda una carpeta:
git add nombre_archivo/

para cambiar en modo editor sólo digitamos
git commit --amend

en lugar de poner el HEAD^ podemos poner el penúltimo hash que es al que realmente apunta el HEAD^
git reset --soft 123123 

mixed tampoco es destructivo pero saca todo del stage y los cambios quedan listos para añadirlos
git reset --mixed  (si no le colocamos es el mixed por defecto)

log de la referencia de todo lo que ha sucedido en orden cronológico, se puede usar como info para recuperar cambios que ya no se ven
git reflog

mover archivo de una localización a otra si es dentro de la misma carpeta o sea es renombrarlo
git mv nombre_archivo nuevo_nombre  (este cambio se va al stage)

para remover un archivo normalmente se hace fisicamente pero también está el comando:

git rm nombre_archivo (este cambio se va al stage)

git reset --hard  es casi lo mismo que git checkout -- .

cuando cambiamos de nombre fisicamente para git es un nuevo archivo al cual no le da seguimiento pero al darle git add .
git se da cuenta que se trata del mismo archivo y le pasa la historio de uno al otro

R archivo_original -> archivo_renombrado

crear rama
git branch rama-villanos

en qué rama estoy?
git branch (ver el asterisco)

para moverme a otra rama

git checkout nombre_rama
git checkout -b nombre_rama  (para crear la rama y moverme allí)

(HEAD -> rama-villanos, master) (me indica que el HEAD rama-villanos y el master están apuntando a lo mismo)
o sea que las dos ramas están paradas en el mismo punto del  tiempo

para hacer un merge de a la rama principal, primero me muevo a la rama principal

para hacer el merge 
git merge rama_que_se_va_integrar_a_master
si en el mensaje sale Fast-forward significa que no hubo ningún conflicto

para eliminar una rama porque ya no la necesitamos
git branch -d nombre_rama (si hubiera cambios pendientes en la rama GIT te pregunta si lo deseas borrar igual)
y para asegurarnos de que lo borre de manera forzada le ponemos un -f (git branch -d nombre_rama -f)

 
both modified:   misiones.md
se unió todo lo que no tiene conflicto pero sólo falta resolver los mismos
se tiene que resolver el conflicto luego de un merge, se resuelve el conflicto y hacer commit y listo! (git commit -am "mensaje")

para crear etiquetas como versiones por ejemplo
git tag nombre_version (y se va a quedar en la historia del último commit)
git tag  (ver todos los tags)
git tag -d nombre_tag (borrar tag)
git tag -a v1.0.0 -m "Versión 1.0.0 lista" (-a: annotated, -m: mensaje)
git tag -a v0.1.0 XXxxXxX -m "Versión Alpha de nuestra app"  (XXxxXxX hash de commit)
git show v0.1.0 (ver información del tag)


07 DEMO STASH

git stash (y nos sale un msg que dice todo el directorio ha sido salvado WIP: trabajo en progreso)
git stash list (muestra la lista de stashes, se recomienda sólo un stash)
git stash pop (esto toma el último stash y va a traer todo lo del stash y va a mantener los cambios posteriores)

y si hay varios stashes todos van a correr, el que era 0 ahora será 1
para borrar el stash  ya que al hacer pop cuando hay conflicto no lo elimina

git stash clear (borra todos los stashes)

cuando tengo varios stashes
git stash apply "stash@{2}" (para obtener los cambios de cierto stash y no borra el stash) 

git stash drop "stash@{0}"  (para borrar cierto stash) y es lo mismo que:  git stash drop (ya que para el primero 
no es necesario colocar el hash)

para revisar un stash: 
git stash show "stash@{1}"

git stash save "Agregamos a loki en villanos"  (para guardar un stash con un nombre)

git stash list --stat (mas info)
git stash pop (toma el último stash o sea el cero y lo ellimina, también trae todos los cambios del stash y los regresa a mi rama)
como se puede apreciar aparece en rojo el archivo modificado, entonces con un git commit am "xxxx" recién surge efecto el stash

08 - REBASE
git rebase  master (estando parados en una rama diferente a master hacemos rebase para que los commits del
			master se coloquen en la rama antes de los commits de la rama)

git checkout master (luego del rebase nos pasamos al master)
git merge rama-misiones-completadas  (hacemos el merge que es un fastforward)

git branch -d rama-misiones-completadas (eliminamos la rama)
el rebase no se acostumbra hacer lo que se acostumbra es el merge y resolver conflictos

ctrl + l para limpiar la consola

git rebase -i HEAD~4 (puedes cambiar los últimos 4 commits en modo edición, y muestra comandos)

con squash uno dos elementos
reword para cambiar de nombres a los commits
edit para editar el commit luego hacemos reset y desagrupamos el commit en dos y al final
git rebase --continue
git rebase -i HEAD~3

5440fe5
/()=?=)/^~
git remote add origin https://github.com/xxxxxxxxxxxx
git remote -v    (esto es para revisar todos las fuentes remotas que tenemos)
git push -u origin master (master es la rama que nosotros deseamos enviar al repositorio origin, -u es para la prox vez que hagamos
un push no necesitemos especificar la rama)


git push --tags (para subir todos mis tags)
en el repositorio entrando a los tags, puedo descargar el proyecto como estaba en ese momento pero no descargo el repositorio en
sí o sea no descargo el archivo .git
