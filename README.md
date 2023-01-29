# linux-sys
Learn Linux and Beyoind

# Curso de Bash Scripting
<!-- https://itsfoss.com/tag/bash-curso/?ref=its-foss-news
-->
## Primer Script de Bash Shell

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

## variables en scripts de shell bash

Edita tu script hello.sh y utiliza el comando read para obtener la entrada del usuario:

```
#! /bin/bash

echo "¿Cuál es tu nombre?"

read nombre

echo "Hola, $nombre"
```

Ahora si ejecutas tu script hello.sh; te pedirá tu nombre y luego te saludará con el nombre que le proporciones:

```
team@itsfoss:~/scripts$ hola.sh 
¿Cuál es tu nombre?
Marco
Hola, Marco
```

Aquí, utilicé el comando read para transferir el control de la ejecución del script al usuario, para que el usuario pueda ingresar un nombre y luego almacenar lo que el usuario ingresó, en la variable `name`.

Puedes usar el signo igual para crear y establecer el valor de una variable. Por ejemplo, la siguiente línea creará una variable llamada `edad` y establecerá su valor en 27.

``
edad = 21
```

Después de haber creado la variable `edad`, puedes cambiar su valor tanto como quieras.

```
edad = 3
```

El comando anterior cambia el valor de la variable edad de `27` a `3`. 

Las variables pueden contener diferentes tipos de datos; las variables pueden almacenar enteros, cadenas y caracteres.

```
letra = 'c'
color = 'azul'
año = 2021
```

También puedes crear una variable constante, es decir, una variable cuyo valor no cambiará nunca. Esto puede hacerse precediendo el nombre de su variable con el comando readonly:

```
readonly PI=3.14159
```

El comando anterior creará una variable constante `PI` y establecerá su valor de `3.14159`. Ahora, no puedes cambiar el valor de la variable constante, si lo intentas, obtendrás un error:

```
bash: PI: readonly variable
```

Como puedes ver, sólo puedes leer el valor de una variable constante, pero nunca puedes cambiar su valor después de haberla creado.

La capacidad de almacenar la salida de un comando en una variable se llama sustitución de comandos y es, con mucho, una de las características más sorprendentes de bash.

El comando `date` es un ejemplo clásico para demostrar la sustitución de comandos:

```
HOY=$(date)
```

El comando anterior almacenará la salida del comando date en la variable `HOY`. Fíjate en que tienes que encerrar el comando `date` entre un par de paréntesis y un signo de dólar (a la izquierda).

También puede encerrar el comando entre un par de comillas:

```
HOY=`date`
```

El método de la cita posterior es la forma antigua de hacer la sustitución de comandos, por lo que recomiendo encarecidamente que lo evites y te quedes con el enfoque moderno:

```
variable=$(comando)
```

Utiliza el comando `whoami` junto con la sustitución de comandos para saludar a quien ejecute el script:

```
#! /bin/bash           

echo "Hello, $(whoami)"
```

Como puedes ver, ¡sólo has necesitado dos líneas! Ahora ejecute el script:

```
./hola.sh
```







