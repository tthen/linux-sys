# linux-sys
Learn Linux and Beyoind

## Curso de Bash Scripting
<!-- https://itsfoss.com/tag/bash-curso/?ref=its-foss-news
-->

Este curso le enseñará todo lo que necesita para empezar a usar bash scripting. Cada concepto de bash se explica con ejemplos fáciles de entender. Aprenderás a: - Crear y ejecutar un script bash - Utilizar variables y pasar argumentos al script - Utilizar declaraciones de decisión (if-else, switch) - Realizar operaciones aritméticas y de cadena - Utilizar matrices, bucles y funciones en bash - Automatizar tareas repetidas con scripts bash 


```
cat > hola.sh
```

Inserta la siguiente línea dentro del documento escribiéndola en el terminal:

```
echo "¡Hola, mundo!"
```

Pulsa Ctrl+D para guardar el texto en el archivo y salir del comando cat.

La línea `#!/bin/bash` se conoce como la línea shebang y en alguna literatura, se conoce como la línea hashbang y eso es porque comienza con los dos caracteres hash ‘#’ y bang ‘!’.

```
#!/usr/bin/bash

echo "¡Hola, mundo!"
```

Cuando incluyes la línea `#!/bin/bash` en la parte superior de tu script, el sistema sabe que quieres usar bash como intérprete para tu script. Por lo tanto, ahora puedes ejecutar el script `hello.sh` directamente sin precederlo con bash.

Ahora para lograr que el archivo `hello.sh` sea ejecutable, utilizaremos el comando chmod de la siguiente manera:

```
chmod u+x hola.sh
```
Cuando incluyes la línea `#!/bin/bash` en la parte superior de tu script, el sistema sabe que quieres usar bash como intérprete para tu script. Por lo tanto, ahora puedes ejecutar el script `hello.sh` directamente sin precederlo con bash.

```
./hello.sh
```

Habrás notado que he utilizado `./hello.sh` para ejecutar el script; obtendrás un error si omites el `./` inicial

```
team@itsfoss:~/scripts$ hello.sh
hello.sh: command not found
```

Bash pensó que estabas tratando de ejecutar un comando llamado `hello.sh`. Cuando ejecutas cualquier comando en tu terminal; el shell busca ese comando en un conjunto de directorios que se almacenan en la variable `PATH`.

Puedes usar echo para ver el contenido de esa variable `PATH`:

```
echo $PATH
/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/snap/bin
```

El carácter de dos puntos (`:`) separa la ruta de cada uno de los directorios que su shell explora cada vez que ejecuta un comando.

Los comandos de Linux como `echo`, `cat`, etc. pueden ejecutarse desde cualquier lugar porque sus archivos ejecutables se almacenan en los directorios `bin`. Los directorios `bin` se incluyen en el `PATH`. Cuando se ejecuta un comando, el sistema comprueba el `PATH` para todos los posibles lugares que debe buscar para encontrar el ejecutable para ese comando.

Si quieres ejecutar tu script bash desde cualquier lugar, como si fuera un comando normal de Linux, añade la ubicación de tu script de shell a la variable` PATH`.

Primero, obten la ubicación del directorio de tu script (asumiendo que está en el mismo directorio), usa el comando `PWD`:

```
pwd
```

Utiliza el comando export para añadir tu directorio de scripts a la variable `PATH`.

```
export PATH=$PATH:/home/user/scripts
```

El momento de la verdad está aquí; ejecuta `hello.sh`:

```
team@itsfoss:~/scripts$ hello.sh
Hello, World!
```


