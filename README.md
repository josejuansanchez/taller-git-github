# Taller de introducción a `git` y GitHub

En este taller de introducción a `git` y GitHub aprenderemos los comandos básicos para empezar a trabajar con repositorios de forma local y remota.

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

* *Working directory*
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
+-----------+  +-------+  +----------------+
| Workspace |  | Index |  |Local repository|
+-----+-----+  +---+---+  +-------+--------+
      |            |              |
      |            |              |
  Untracked        |              |
      |            |              |
  Modified      Staged        Commited
      |            |              |
      |            |              |
      |            |              |
      +            +              +
```

Para consultar el estado de los archivos usamos el comando:

```
git status
```

**Este comando es muy usado** ya que es fundamental conocer el estado de los archivos de nuestro repositorio.

## Trabajando con un repositorio local

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

En primer lugar comprobaremos en qué estado se encuentran los archivos del repositorio:

```
git status
```

Si tenemos archivos en estado ***untracked*** o ***modified*** los añadimos a la ***staging area*** con el siguiente comando:

```
git add <nombre_archivo>
```

El comando anterior nos permite seleccionar cuáles son los archivos que queremos mover a la ***staging area***. Si tenemos varios archivos que queremos mover a la ***staging area*** no es necesario hacerlo uno a uno, podemos usar el siguiente comando para moverlos todos a la vez:

```
git add -A
```

Una vez que tenemos los archivos en la ***staging area*** tenemos que hacer un ***commit*** para moverlos al repositorio:

```
git commit -m "Breve comentario con los cambios realizados"
```


```
git commit --amend
```

### Borrando y moviendo archivos

```
git rm <archivo>
```

```
git mv <archivo>
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

# GitHub

## Crear un nuevo usuario

(TODO)

## Configuración de GitHub

(TODO)

## Cómo trabajar en equipo con GitHub

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