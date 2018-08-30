COMANDOS GIT
============

Básicos
-------
	git help											Ayuda
	git config --global user.name "nombre"				Agregar nombre de usuario en las configuraciones globales
	git config --global user.email email@domain.com 	Agregar correo de usuario en las configuraciones globales
	git config --global color.ui true					Activar colores en la consola de comandos
	git config --global push.default simple				Configuracion para cuando se realice un "git push" solo se suban los cambios de la rama actual

	git init											Inicializa la carpeta donde este el promtuario como un repositorio git
	git clone <url>										Clonar repositorio remoto en local
	git status											Verifica los cambios sin consignar al escenario


Enlace con repositorios remotos
-------------------------------
	git remote add origin <ruta>						Agrega repositorio remoto principal 
	git remote add upstream <ruta>						Agrega reporitorio remoto paralelo	
	git remote set-url origin <newurl> <oldurl>			Cambiar la url del repositorio
	git remote set-url origin <ssh_url> <https_url>		Cambiar la url del repositorio remoto por la ruta para conexion con ssh
	

Key SSH para conexión al repositorio
------------------------------------

Proceso de creacion (http://git-scm.com/book/es/Git-en-un-servidor-Generando-tu-clave-p%C3%BAblica-SSH)		

	cd ~/.ssh	moverse a la carpeta personal para keys ssh
	ssh-keygen	Generar nueva key


Agregar archivos al escenario
-----------------------------
	git add <listado de archivos>		Adicionar uno o varios archivos nuevos o editados al escenario
	git add --all						Adicionar todos los archivos nuevos o editados al escenario
	git add *.txt						Adicionar todos los archivos nuevos o editados al escenario con extension txt
	git add docs/*.txt 					Adicionar todos los archivos nuevos o editados al escenario con extension txt dentro de la carpeta docs
	git add docs/ 						Adicionar todos los archivos nuevos o editados al escenario dentro de la carpeta docs
	git add "*.txt"						Adicionar todos los archivos nuevos o editados al escenario con extension txt en todo el proyecto


Consignaciones al repositorio local (commit)
--------------------------------------------
	git commit -m "Mensaje descriptivo" 			Consignar los cambios. Crea una instantánea del escenario y la adiciona a la línea de trabajo.
													El mensaje debe estar en presente
	git commit -a -m "Mensaje descriptivo"			"-a" adiciona todos los archivos con cambios. No adiciona archivos que estén fuera del escenario
	git commit -am "Mensaje descriptivo"			"-a" adiciona todos los archivos con cambios. No adiciona archivos que estén fuera del escenario
	git commit --amend -m "Mensaje descriptivo"		"amend" es para que git sepa que es una modificación  o arreglo de la última consignación, 
													se puede especificar un nuevo mensaje en la consignación, Cualquier cosa que esté en el escenario 
													será adicionada a la consignación anterior.
													
	git revert <idCommit>					 Revertiendo un commit
	git reset --soft <idCommit> 				Deshaciendo  commits deja cambios en stage
	git reset --mixed <idCommit> 				Deshaciendo  commits deja cambios  en directorios
	git reset --hard <idCommit> 				Deshaciendo  commits deja cambios  en directorios
	cat .git/refs/heads/master				ver commit actual

Subir y bajar consignaciones del repositorio central
----------------------------------------------------
	git push -u origin master	Subir cambios consignados al repositorio remoto. "origin" se refiere al nombre de la conexion con el 
								repositorio central y "master" es el nombre del branch
	git pull					Bajar los cambios desde el repositorio remoto
	git fetch					Bajar los cambios desde el repositorio remoto sin mezclar los archivos


Conexiones con repositorios remotos
-----------------------------------
	git remote 				Verificar todos los remotos registrados, Se pueden tener muchos remotos, generalmente el de pruebas, producción y el de seguridad
	git remote -v				Verificar todos los remotos registrados, lista direccion de recepcion fetch
	git remote add origin <repositorioRemoto>	Agregar repositorio remoto
	git remote rm <nombre>		Eliminar un remoto
	git remote r <nombre>		Eliminar un remoto
	git remote show origin		Muestra:
									Ramas remotas
									Ramas locales y con cuales remotas mapean o fusionan
									Ramas locales que referencian a las remotas para push
	

Revertir cambios en las consignaciones locales
----------------------------------------------
	git checkout <archivo>		Deshacer cambios en el escenario
	git checkout --<archivo>	Devolver la última consignación
	git reset HEAD <archivo>	Remover cambios de escenario: vuelve al estado anterior
	git reset --soft HEAD^		Devolver al escenario solo un paso
	git reset --hard HEAD^		Deshace completamente todos los cambios y la última consignación
	git reset --hard HEAD^^		Las últimas dos consignaciones


Branch (Ramas)
--------------
	git branch 											Muestra las ramas creadas y resalta en la que se esta trabajando actualmente
	git branch <nombre>									Crear una nueva rama
	git checkout -t origin/<rama>						Agregar al repositorio local una rama remota
	git checkout -b <nuevonombre> origin/<ramaremota>	Agregar al repositorio local una rama remota con un nombre distinto
	git branch -r										Puede ver todas las ramas remotas
	git push origin :<rama>								Elimina rama del repositorio remoto
	git push origin --delete <idBranch>						Elimina rama del repositorio remoto
	git branch -d <rama>								Elimina rama del repositorio local
	git branch -D <rama>								Forzar eliminacion de rama local
	
	git checkout <rama>									Cambiar a escenario de otra rama
	git merge <nombrerama>								Mezcla la rama que se indica en <nombrerama> a la rama donde se esta trabajando
	git merge --abort								Aborta cambios de la mezcla
	git checkout -b <nombrerama>						Crea y se cambia a la nueva rama
	
	git remote prune origin								Eliminar referencia remota de las ramas eliminadas
	git diff <master>..<idBranch>							Muestra diferencias de ramas
	git push -u origin <idRama>				Creando un branch remoto (Cargar al repositorio una rama local)

	
	

Tags (Etiquetas)
----------------
	git tag								Muestra las etiquetas creadas
	git tag -a <nombre> -m "<mensaje>"	Crear una etiqueta
	git push --tags						Subir etiquetas a remoto
	git checkout <nombretag>			Volver a como estaba el código cuando se liberó con una etiqueta especifica
	git clone -b <tag> <link_git>		Clonar un tag especifico
	git tag -d <tag>					Eliminar una etiqueta local
	git push origin :refs/tags/<tag>	Eliminar una etiqueta remota

Comparaciones (diff)
--------------------
	git diff							Muestra cambios de la copia de trabajo
	git diff HEAD						Muestra cambios de la última consignación
	git diff -w HEAD						Muestra cambios de la última consignación sin nuevos espacios
	git diff HEAD^						Muestra cambios del padre de la última consignación
	git diff HEAD^^						Muestra cambios del abuelo de la última consignación
	git diff HEAD~5						Muestra cambios de 5 consignaciones atras
	git diff 4fb063f..f5a6ff9			Mostrar diferencias usando los identificadores SHA de dos consignaciones
	git diff --stat --summary 4fb063f..HEAD			Mostrar diferencias puntuales
	git diff master <rama>				Compara dos ramas
	git blame <archivo> --date short	Para conocer las historia de un cambio que no se entiende


Eliminar archivos
-----------------
	git rm <archivo>			Eliminar archivo del escenario y sistema de archivos
	git rm --cache <archivo>	Eliminar archivo del escenario pero no del sistema de archivo

 
Consultar registro (Historial de consignaciones)
------------------------------------------------
	git log												Mostrar lista de consignaciones
	git log --since=1.minute.go							Muestra consignaciones de hace 1 minuto
	git log --since=1.day.ago							Muestra consignaciones de hace 1 dia
	git log --since=1.hour.ago							Muestra consignaciones de hace 1 hora
	git log --since=1.month.ago --until=2.weeks.ago		Muestra consignaciones de hace 1 mes hasta hace 2 semanas
	git log --since=2000-01-01 --until=2012-12-21		Muestra consignaciones entre dos fechas
	git log --graph						Mostrar lista de consignaciones con grafica
	git log --oneline --graph --all --decorate		Mostrar lista de consignaciones con grafica decorado en una linea
	git log show <idCommit>					Examinando el contenido de cada commit

Alias
-----
	git config --global alias.co checkout				Crea alias co para checkout
	git config --global alias.br branch					Crea alias br para branch
	git config --global alias.ci commit					Crea alias ci para commit	
	git config --global alias.st status					Crea alias st para status
	git config --global alias.aa 'add --all'			Crea alias aa para add --all (agregar todo)
	
Listado de contenido
-----
	git ls-tree master					Lista contenido de la Rama
	git ls-tree master^					Lista contenido de la Rama vercion anterior
	git ls-tree master^^					Lista contenido de la Rama vercion anterior a la anterior
	git ls-tree master~2					Lista contenido de la Rama vercion anterior a la anterior

	
cambios almacenados temporalmente
-----
	git stash list								lista de stash
	git stash show <isStash>						Estadisticas del cambio
	git stash show -p <isStash>						Estadisticas del cambio similar a git diff
	git stash save "nameComit"						Almacenando cambios temporalmente
	git stash save "nameComit"						Almacenando cambios temporalmente
	git stash pop	<isStash>						aplica cambios y elimina de temporales
	git stash apply	<isStash>						aplica cambios y no elimina de temporales
	git stash clear	<isStash>						Elimina de temporales








	


	

