# Taller de introducción a `git` y GitHub

En este taller de introducción a `git' y GitHub aprenderemos los comandos básicos para empezar a trabajar con repositorios de forma local y remota.

## Instalación y configuración

### Instalación de `git`

#### Ubuntu

```
sudo apt-get update
sudo apt-get install git
```

#### Windows

Descargar desde la web oficial: http://git-scm.com/downloads.

### Configuración de Git

Configuramos el nombre y el email que aparecerán en los *commits* que hagamos sobre los repositorios.

```git
git config --global user.name "Nombre"
```

```git
git config --global user.email "correo@electronico.com"
```

## ¿Cómo funciona `git`?

![](https://upload.wikimedia.org/wikipedia/commons/thumb/4/44/Git_data_flow_simplified.svg/360px-Git_data_flow_simplified.svg.png)

## Trabajando con un repositorio local

### Creación de un repositorio local

Un repositorio Git es un directorio oculto llamado `.git` que se guarda en el directorio raíz de nuestro proyecto. El directorio `.git` almacena el historial de todos los cambios que se han realizado.

```git
git init
```

Por ejemplo, para crear nuestro primer repositorio podríamos hacer lo siguiente:

```
mkdir taller-git
cd taller-git
git init
```

### Comandos básicos para trabajar con un repositorio local

```
git status
```

```
git add <archivo>
```

```
git add -A
```

```
git commit -m "Breve comentario con los cambios realizados"
```

```
git commit --amend
```

```
git diff
```

## Trabajando con un repositorio remoto

### Clonar un repositorio remoto

```
git clone https://github.com/josejuansanchez/taller-git-github.git
```

### Comandos básicos para trabajar con un repositorio remoto

Utilizaremos los mismos comandos que usamos para trabajar con un repositorio local y los siguientes:

```
git push
```

```
git pull
```

## Deshaciendo cambios

```
git reset HEAD <archivo>
```

```
git ckeckout -- <archivo>
```

## El archivo `.gitignore`

Dentro del directorio raíz de nuestro proyecto podemos tener un archivo especial llamado `.gitignore` donde indicamos los archivos o tipos de archivos que queremos que sean ignorados por `git`. 

Por ejemplo, si en nuestro repositorio no queremos guardar archivos `*.class` y `*.log` tendríamos el siguiente contenido en el archivo `.gitignore`:

```
*.class
*.log
```

## Consultar el historial de *commits*

```
git log
```

```
git log --oneline
```

```
git log --graph
```

## Branches

(TODO)

## Problemas comunes

(TODO)

## Referencias

* https://git-scm.com/book/es/v2
* https://guides.github.com

# Créditos

* Imagen de [Cmglee](https://commons.wikimedia.org/wiki/User:Cmglee), [CC BY-SA 3.0](https://creativecommons.org/licenses/by-sa/3.0) or [GFDL](http://www.gnu.org/copyleft/fdl.html), via Wikimedia Commons.

## Licencia

<a rel="license" href="http://creativecommons.org/licenses/by-sa/4.0/"><img alt="Licencia de Creative Commons" style="border-width:0" src="https://i.creativecommons.org/l/by-sa/4.0/88x31.png" /></a><br />Esta obra está bajo una <a rel="license" href="http://creativecommons.org/licenses/by-sa/4.0/">licencia de Creative Commons Reconocimiento-CompartirIgual 4.0 Internacional</a>.