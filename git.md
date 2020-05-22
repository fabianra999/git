# GIT

## Configuración inicial
	* git config --global user.name "nombre"				Agregar nombre de usuario en las configuraciones globales
	* git config --global user.email email@domain.com 		Agregar correo de usuario en las configuraciones globales
	* git config --global color.ui true						Activar colores en la consola de comandos
	* git config --global push.default simple				Configuracion para cuando se realice un "git push" solo se suban los cambios de la rama actual
	* git config --global core.autocrlf false				Desactivar control de salto de linea LF(unix) a CRLF(windows)

	* git config --global core.preloadindex true
	* git config --global core.fscache true
	* git config --global gc.auto 256


## Clonar un repositorio
	* git clone //192.168.90.100/htdocs/git_repository/test_git.git 	Descarga el repositorio en la carpeta donde este ubicado
	* git pull															Descarga estructura adicional del repositorio (ramas, tags)

## Consignar cambios
	* git add . 									Prepara todos los archivos para ser consignados
	* git commit -m "Descripción de los cambios"	Se realiza la consignacióngi clo de los cambios realizados en el repositorio local
	* git log										Ver listado de consignaciones

## Subir commits a repositorio remoto
	* git pull origin master								Descargar primero posibles cambios cargados por otros
	* git status											Ver estado de los cambios
	* Resolver conflictos									Si exiten conflictos deben resolverse manualmente
	* git commit -m "Mensaje de solución de conflictos"		Se consignan los cambios realizados para solucionar los conflictos
	* git push origin master								Se sube al repositorio remoto

## Ramas
	* git branch <nombre-rama>					Crea una rama
	* git checkout <nombre-rama>				Apunta el directorio de trabajo a la rama
	* git add . 								Prepara todos los archivos para ser consignados en la rama
	* git commit -m "Descripción"				Se realiza la consignación de los cambios realizados en la rama del repositorio local
	* git push origin <nombre-rama>				Sube al repositorio remoto las consignaciones de la rama. Si la rama no existe en el repositorio centra se crea automaticamente

## Descargar cambios de la rama principal (master) a la rama de trabajo
	* git checkout master									Moverse a la rama principal
	* git pull origin master								Descargar los posibles cambios
	* git checkout <nombre-rama>							Moverse a la rama en la que se esta trabajando
	* git merge master										Mezclar la rama principal a la rama en la que se esta trabajando
	* Solucionar posibles conflictos						Si exiten conflictos deben resolverse manualmente
	* git commit -m "Mensaje de solución de conflictos"		Se consignan los cambios realizados para solucionar los conflictos

## Subir cambios de la rama de trabajo a la rama principal (master)
	* git checkout master									Moverse a la rama principal
	* git merge <nombre-rama>								Mezclar la rama de trabajo a master
	* git push origin master								Subir al repositorio remoto

## Descargar rama del repositorio remoto que no existe en mi repositorio local
	* git checkout master						Asegurarse de estar en la rama master
	* git branch -r								Ver referencias a ramas en el repositorio remoto
	* git pull									Actualizar rama principal y descargar referencias de las ramas que estan en el repositorio remoto
	* git checkout -t origin/<nombre-rama>		Moverse a la rama descargada

## Congelar cambios
	*git stash        				 Congelar cambios	
	*git stash pop          		 Descongelar cambios
## Eliminar Cambios locales
	*git reset --hard       				 Eliminar todos los cambios locales	
