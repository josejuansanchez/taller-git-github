# Taller de introducción a `git` y GitHub

En este taller de introducción a `git` y [GitHub][1] aprenderemos los comandos básicos para empezar a trabajar con repositorios de forma local y remota.

1. `git`  
  1.1 Instalación y configuración de `git`  
  1.2 Estados de un archivo en `git`  
  1.3 Trabajando con un repositorio local  
  1.4 Trabajando con un repositorio remoto  
  1.5 Deshaciendo cambios  
  1.6 El archivo `.gitignore`  
  1.7 Consultar el historial de *commits*  
  1.8 Branches  
  1.9 Problemas Comunes  
2. GitHub  
  2.1 Creación de un nuevo usuario  
  2.2 Configuración de GitHub  
  2.3 Cómo trabajar en equipo con GitHub

# `git`

## Instalación y configuración de `git`

### Instalación de `git`

#### Ubuntu

```
sudo apt-get update
sudo apt-get install git
```

#### Windows

Descargar desde la web oficial: http://git-scm.com/downloads.

### Configuración de `git`

Configuramos el nombre y el email que aparecerán en los *commits* que hagamos sobre los repositorios.

```
git config --global user.name "Nombre"
```

```
git config --global user.email "correo@electronico.com"
```

Para comprobar si se han aplicado los cambios podemos ejecutar el siguiente comando para mostrar cuál es la configuración actual de `git`:

```
git config --list
```

## Secciones principales de un repositorio `git`

En un repositorio `git` podemos diferenciar las siguientes secciones:

* *Workspace*
* *Staging area (Index)*
* *Local repository*
* *Remote repository*

![](images/img-00.png)

Figura 1: Imagen de [Oliver Steele](http://osteele.com).

## Estados de un archivo en `git`

Un archivo puede estar en alguno de los siguientes estados:

* Sin seguimiento (*untracked*)
* Preparado (*staged*)
* Modificado (*modified*)
* Confirmado (*commited*)

El siguiente diagrama muestra en qué sección se puede encontrar cada archivo en función de su estado.

```
+-------------+  +-------------+  +-------------+
|  Workspace  |  |   Staging   |  |    Local    |
|             |  |     Area    |  |  Repository |
+------+------+  +------+------+  +------+------+
       |                |                |
       |                |                |
   Untracked            |                |
       |                |                |
   Modified          Staged          Commited
       |                |                |
       |                |                |
       |                |                |
       +                +                +

```

Para consultar el estado de los archivos usamos el comando:

```
git status
```

**Este comando es muy usado** ya que es fundamental conocer el estado de los archivos de nuestro repositorio.

## Cómo trabajar con un repositorio local

### Creación de un repositorio local

Un repositorio Git es un directorio oculto llamado `.git` que se guarda en el directorio raíz de nuestro proyecto. El directorio `.git` almacena el historial de todos los cambios que se han realizado.

El comando para crear un repositorio `git` es el siguiente:

```
git init
```

Por ejemplo, para crear nuestro primer repositorio podríamos hacer lo siguiente:

```
mkdir taller-git
cd taller-git
git init
```

Si examinamos el contenido del directorio `.git` veremos el siguiente árbol de contenidos:

```
.
└── .git
    ├── HEAD
    ├── config
    ├── description
    ├── hooks
    │   ├── applypatch-msg.sample
    │   ├── commit-msg.sample
    │   ├── post-update.sample
    │   ├── pre-applypatch.sample
    │   ├── pre-commit.sample
    │   ├── pre-push.sample
    │   ├── pre-rebase.sample
    │   ├── pre-receive.sample
    │   ├── prepare-commit-msg.sample
    │   └── update.sample
    ├── info
    │   └── exclude
    ├── objects
    │   ├── info
    │   └── pack
    └── refs
        ├── heads
        └── tags
```

### Comandos básicos para trabajar con un repositorio local

**Paso 1**

En primer lugar comprobaremos en qué estado se encuentran los archivos del repositorio:

```
git status
```

**Paso 2**

Si tenemos archivos en estado ***untracked*** o ***modified*** los añadimos a la ***staging area*** con el siguiente comando:

```
git add <nombre_archivo>
```

El comando anterior nos permite seleccionar cuáles son los archivos que queremos mover a la ***staging area***. Si tenemos varios archivos que queremos mover a la ***staging area*** no es necesario hacerlo uno a uno, podemos usar el siguiente comando para moverlos todos a la vez:

```
git add -A
```

**Paso 3**

Una vez que tenemos los archivos en la ***staging area*** tenemos que hacer un ***commit*** para moverlos al repositorio:

```
git commit -m "Breve comentario con los cambios realizados"
```

## Cómo deshacer cambios

### Modificar el texto del último *commit*

```
git commit --amend
```

### Añadir archivos al último *commit*

```
git commit --amend
```

**Ejemplo:**

Suponemos que acabamos de hacer un *commit* en el repositorio pero nos hemos olvidado de añadir un archivo que queremos incluir en ese *commit*. En estos casos podemos utilizar el comando `git commit --amend` para añadir nuevos archivos al último *commit* realizado sobre el repositorio.

A continuación se muestra una posible secuencia de comandos simlando la situación que acabamos de describir.

```
git add archivo.txt
git commit -m "Añadimos el archivo.txt"
git add archivo_olvidado.txt
git commit --amend
```

### Mover un archivo del *staging area* al *workspace*

```
git reset HEAD <archivo>
```

**Ejemplo:**

Suponemos que hemos añadido un archivo llamado `archivo.txt` al *staging area* pero queremos volver a llevarlo al *workspace* para realizar una nueva modificación antes de hacer un *commit* en el repositorio.

El escenario descrito sería el siguiente:

```
+-------------+  +-------------+  +-------------+
|  Workspace  |  |   Staging   |  |    Local    |
|             |  |     Area    |  |  Repository |
+------+------+  +------+------+  +------+------+
       |                |                |
       |                |                |
       |                |                |
       |                |                |
       |            archivo.txt          |
       |                |                |
       |                |                |
       |                |                |
       +                +                +
```

Para mover el archivo `archivo.txt` al *workspace* ejecutamos:

```
git reset HEAD archivo.txt
```

Después del comando anterior el repositorio quedaría así:

```
+-------------+  +-------------+  +-------------+
|  Workspace  |  |   Staging   |  |    Local    |
|             |  |     Area    |  |  Repository |
+------+------+  +------+------+  +------+------+
       |                |                |
       |                |                |
       |                |                |
       |                |                |
   archivo.txt          |                |
   (Modified)           |                |
       |                |                |
       |                |                |
       +                +                +
```

### Deshacer cambios en el *workspace*

```
git ckeckout -- <archivo>
```

**Ejemplo:**

Suponemos que hemos realizado algunos cambios sobre un  archivo llamado `archivo.txt` pero queremos deshacerlos y que el archivo vuelva a tener el contenido con el que se guardó en el útimo *commit* en el repositorio.

El escenario descrito sería el siguiente:

```
+-------------+  +-------------+  +-------------+
|  Workspace  |  |   Staging   |  |    Local    |
|             |  |     Area    |  |  Repository |
+------+------+  +------+------+  +------+------+
       |                |                |
       |                |                |
       |                |                |
       |                |                |
   archivo.txt          |                |
   (Modified)           |                |
       |                |                |
       |                |                |
       +                +                +
```

Para deshacer los cambios realizados en `archivo.txt` y volver a su estado anterior sería necesario ejecutar:

```
git ckeckout -- archivo.txt
```

## Borrando y moviendo archivos

```
git rm <archivo>
```

```
git mv <archivo>
```

## Cómo trabajar con un repositorio remoto

Existen dos opciones para empezar a trabajar con un repositorio remoto. 

* Cuando ya tenemos creado un repositorio local y queremos **añadir** un repositorio remoto para sincronizarnos.
* Cuando no partimos de ningún repositorio local y lo que queremos hacer es **clonar** el repositorio remoto en nuestra máquina.

### Añadir un repositorio remoto a un repositorio ya existente

```
git remote add <alias> <url_del_repositorio_remoto>
```

**Ejemplo:**

Suponemos que ya tenemos creado un repositorio local y queremos añadir el repositorio remoto del taller de git. En este caso hemos usado `taller-git` como alias. Este sería el comando que tendríamos que ejecutar:

```
git remote add taller-git https://github.com/josejuansanchez/taller-git-github.git
```

Para comprobar si el repositorio remoto se ha añadido correctamente ejecutamos:

```
git remote -v
```

El comando anterior nos devolverá estas dos líneas:

```
taller-git	https://github.com/josejuansanchez/taller-git-github.git (fetch)
taller-git	https://github.com/josejuansanchez/taller-git-github.git (push)
```

La primera línea acabada con la palabra *(fectch)* indica que esa es la url del repositorio remoto desde el que podemos recibir cambios.

La segunda línea acabada con la palabra *(push)* indica que esa es la url del repositorio remoto donde podemos enviar nuestros cambios.

(TODO: Explicar cómo hacer fetch y push de un repositorio remoto.)

### Clonar un repositorio remoto

```
git clone <url_del_repositorio_remoto>
```

**Ejemplo:**

```
git clone https://github.com/josejuansanchez/taller-git-github.git
```

Al clonar este repositorio se nos creará un direcorio en nuestra máquina con el nombre `taller-git-github` con el contenido del repositorio remoto.

### Comandos básicos para trabajar con un repositorio remoto

Utilizaremos los mismos comandos que usamos para trabajar con un repositorio local y los siguientes:

```
git push
```

```
git pull
```

```
+-------------+  +-------------+  +-------------+  +-------------+
|  Workspace  |  |   Staging   |  |    Local    |  |    Remote   |
|             |  |     Area    |  |  Repository |  |  Repository |
+------+------+  +------+------+  +------+------+  +------+------+
       |                |                |                |
       |                |                |                |
       |                |                |                |
       |                |                |                |
       |                |                |                |
       |                |                |                |
       |                |                |                |
       |                |                |                |
       +                +                +                +

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

# GitHub

[Revisar el capítulo 6 del libro Git Book](https://git-scm.com/book/es/v2/GitHub-Creaci%C3%B3n-y-configuraci%C3%B3n-de-la-cuenta).


## Crear un nuevo usuario

(TODO)

## Configuración de GitHub

(TODO)

## Cómo trabajar en equipo con GitHub

(TODO)

## *Pull Requests* en GitHub

(TODO)

## *Issues* en GitHub

(TODO)

## Tips

* [Recordar la contraseña](https://gist.github.com/ankurk91/f0b26f1c30d0d6d3ca4e).

## Referencias

* https://git-scm.com/book/es/v2
* https://github.com/oslugr/curso-git
* https://guides.github.com

# Créditos

* La *Figura 1* es una imagen diseñada por [Oliver Steele](http://osteele.com).

## Licencia

<a rel="license" href="http://creativecommons.org/licenses/by-sa/4.0/"><img alt="Licencia de Creative Commons" style="border-width:0" src="https://i.creativecommons.org/l/by-sa/4.0/88x31.png" /></a><br />Esta obra está bajo una <a rel="license" href="http://creativecommons.org/licenses/by-sa/4.0/">licencia de Creative Commons Reconocimiento-CompartirIgual 4.0 Internacional</a>.

[1]: https://github.com