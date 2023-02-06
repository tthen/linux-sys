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

```
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

## Pasando Argumentos a los Scripts de Bash

El siguiente script `contando_lineas.sh` mostrará el número total de líneas que existen en cualquier archivo que el usuario introduzca:

```
#!/user/bin/bash

echo -n "Por favor, introduce la direccion del archivo: "
read direccion_de_archivo
numero_lineas=$(wc -l < $direccion_de_archivo)

echo "Hay $numero_lineas lineas en $direccion_de_archivo"
```

Por ejemplo, el usuario puede introducir el archivo `/etc/passwd` y el script escupirá el número de líneas como resultado:

Este script funciona bien; sin embargo, ¡hay una alternativa mucho mejor!

En lugar de pedir al usuario el nombre del archivo, podemos hacer que el usuario simplemente pase el nombre del archivo como un argumento de la línea de comandos mientras se ejecuta el script de la siguiente manera:

```
./contando_lineas.sh /etc/passwd
```

El primer argumento bash (también conocido como parámetro posicional) puede ser accedido dentro de su script bash usando la variable `$1`.

Así que en el script `contando_lineas.sh`, puedes sustituir la variable filename por `$1` de la siguiente manera:

```
#!/user/bin/bash

numero_lineas=$(wc -l < $1)
echo "Hay $numero_lineas lineas en $1"
```

Fíjate que también me he deshecho del comando `read` y del primer comando `echo` porque ya no son necesarios.

Por último, puedes ejecutar el script y pasar cualquier archivo como argumento:

```
./contando_lineas.sh /etc/group
Hay 62 lineas en /etc/group
```

Puedes pasar más de un argumento a tu script bash. En general, esta es la sintaxis para pasar múltiples argumentos a cualquier script bash:

```
script.sh arg1 arg2 arg3  …
```

El segundo argumento será referenciado por la variable `$2`, el tercer argumento es referenciado por `$3`, .. etc.

La variable `$0` contiene el nombre de tu script bash en caso de que te lo estés preguntando.

Ahora podemos editar nuestro script bash `contando_lineas.sh` para que pueda contar las líneas de más de un archivo:

```
#!/user/bin/bash

n1=$(wc -l < $1)
n2=$(wc -l < $2)
n3=$(wc -l < $3)

echo "Hay $n1 lineas en $1"
echo "Hay $n2 lineas en $2"
echo "Hay $n3 lineas en $3"
```

Algunos de ellos son un poco complicados, ya que pueden tener una larga sintaxis o una larga serie de opciones que puede utilizar.

Afortunadamente, puedes utilizar los argumentos de bash para convertir un comando difícil en una tarea bastante fácil.

Para demostrarlo, echa un vistazo al siguiente script bash `encontrar.sh`:

```
#!/user/bin/bash

find / -iname $1 2> /dev/null
```

Es un script muy sencillo que, sin embargo, puede resultar muy útil. Puede suministrar cualquier nombre de archivo como argumento al script y éste mostrará la ubicación de su archivo:

Verás como ahora es mucho más fácil que teclear todo el comando find! Esta es una prueba de que puedes usar argumentos para convertir cualquier comando largo y complicado en Linux en un simple script de bash.

Si te preguntas sobre el 2> /dev/null, significa que cualquier mensaje de error (como que no se puede acceder al archivo) no se mostrará en la pantalla. Te sugiero que leas sobre la redirección de stderr en Linux para obtener más conocimientos sobre este tema.

Bash tiene un montón de variables especiales incorporadas que son bastante útiles y están a tu disposición.

La siguiente tabla destaca las variables especiales incorporadas más comunes de bash:

```
Variable Especial 	Descripción

$0 	           El nombre del script bash.
$1, $2…$n 	    Los argumentos del script bash.
$$        	    El id del proceso del shell actual.
$#         	   El número total de argumentos pasados al script.
$@            	El valor de todos los argumentos pasados al script.
$?            	El estado de salida del último comando ejecutado.
$!            	El ID del proceso del último comando ejecutado.
```

Para ver estas variables especiales en acción; eche un vistazo al siguiente script bash `variables.sh`:

```
#!/user/bin/bash

echo "Nombre del script: $0"
echo "Número total de argumentos: $#"
echo "Valor de todos los argumentos: $@"
```

Ahora puedes pasar los argumentos que quieras y ejecutar el script:

## Add user
<!-- https://www.digitalocean.com/community/tutorials/how-to-add-and-delete-users-on-a-centos-7-server 
-->

When you first start using a fresh Linux server, adding and removing users is often one of the first things you’ll need to do. In this guide, you will learn how to create user accounts, assign sudo privileges, and delete users on a CentOS 7 server.

To complete this tutorial, you will need:

A CentOS 7 server with a non-root sudo-enabled user. If you are logged in as root instead, you can drop the sudo portion of all the following commands. For guidance, please see our tutorial [Initial Server Setup with CentOS 7](https://www.digitalocean.com/community/tutorials/initial-server-setup-with-centos-7).

Throughout this tutorial we will be working with the user sammy. Please substitute with the username of your choice.

You can add a new user by typing:

```
sudo adduser sammy
```

Next, you’ll need to give your user a password so that they can log in. To do so, use the passwd command:

```
sudo passwd sammy
```

Si el comando anterior falla

```
su -
adduser sammy
passwd sammy
```

You will be prompted to type in the password twice to confirm it. Now your new user is set up and ready for use! You can now log in as that user, using the password that you set up.

Note: if your SSH server disallows password-based authentication, you will not yet be able to connect with your new username. Details on setting up key-based SSH authentication for the new user can be found in step 4 of [Initial Server Setup with CentOS 7](https://www.digitalocean.com/community/tutorials/initial-server-setup-with-centos-7#step-four-%E2%80%94-add-public-key-authentication-recommended).

If your new user should have the ability to execute commands with `root` (administrative) privileges, you will need to give the new user access to sudo.

We can do this by adding the user to the `wheel` group (which gives sudo access to all of its members by default).

To do this, use the usermod command:

```
sudo usermod -aG wheel sammy
```

Now your new user is able to execute commands with administrative privileges. To do so, simply type sudo ahead of the command that you want to execute as an administrator:

```
sudo some_command
```

You will be prompted to enter the password of your user account (not the root password). Once the correct password has been submitted, the command you entered will be executed with root privileges.

To see which users are part of the `wheel` group (and thus have `sudo`), you can use the lid function. `lid` is normally used to show which groups a user belongs to, but with the `-g` flag, you can reverse it and show which users belong in a group:

```
sudo lid -g wheel

Output
 sammy(uid=1001)
```

The output will show you the usernames and UIDs that are associated with the group. This is a good way of confirming that your previous commands were successful, and that the user has the privileges that they need.

If you have a user account that you no longer need, it’s best to delete the old account.

If you want to delete the user without deleting any of their files, type:

```
sudo userdel sammy
```

If you want to delete the user’s home directory along with the user account itself, type:

```
sudo userdel -r sammy
```

With either command, the user will automatically be removed from any groups that they were added to, including the wheel group if they were given sudo privileges. If you later add another user with the same name, they will have to be added to the wheel group again to gain sudo access.


Agregar los otros comandos: `useradd`, `userdel`, `usermod`. Revisar el uso de los comandos con `man usermod`.
Cuando se crear el usuario este se crea sin password, asi que no se puede utilizar la cuenta por que el password esta en blanco. `useradd` no tiene la opcion de agregar el password. Por lo tanto se debe utilizar el comando `passwd`

```
sudo passwd janes
Output:
Changing password for user janes
New Password:
```

Al usuario se debe notificar el cambio del password por el que el desee. Una forma de obligarlo es otorgando un plazo corto para hacerlo en la fecha de expiracion. Pero para esto contamos con el comando `chage` (change user password spiry information), para forzar el cambio del password. Para ver como esta configurada la cuenta utilizar el siguiente comando.

```
sudo chage -l janes
```

Esto muestra las opciones default de la cuenta. Cada distribucion linux tiene su propio manejo. 

En CentOS se pueden ver los defaults con el comando.

```
sudo useradd -D

Output:

GROUP=100
HOME=/home
INACTIVE=-l
EXPIRE=
SHELL=/bin/bash
SKEL=/etc/skel
CREATE_MAIL_SPOOL=yes
```
Es decir, los archivos que se van a encontrar en el directorio del usuario, son los mismos que aparecen en el directorio `/etc/skel`.

Si quiero cambiar el comportamiento default del editor `vim` por ejemplo, que muestre la nuemracion de las lineas de codigo, lo puedo hacer en este diectorio con el siguiente comando.

```
sudo vim ./.vimrc
```

Al interior agregar `set number`, grabar y salir.

Asi de esta manera se ha agregado el archivo `.vimrc` a los nuevos archivos default. Asi cuando se crea un nuevo usuario, este archivo aparecera en los default y podra utilizar esta configutacion del editor vim.

Pero tambien hay otros sitios de donde provienen los defaults, es `login definitions`. Define los sitios donde se almacenan los emails. Aparece el password ages, crea el directorio de usuario, entre otras cosas,

```
sudo less /etc/login.defs
```

Hay otros sitios, como el directorio `/etc/default`. Revisar el contenido del archivo useradd

```
# useradd default file
GROUP=100
HOME=/home
INACTIVE=-1
EXPIRE=
SHELL=/bin/bash
SKEL=/etc/skel
CREATE_MAIL_SPOOL=yes
```

Archivo donde se almacenan todos los usuarios registrados en el sistema: `/etc/passwd`. 
Al final del archivo se encuentran los usuarios con todos los valores, nombre de usuario, bash, directorio, shell, password como una `x`, pero no se puede ver realmente el password.

Con `usermod` se puede modificar el shell que el usuario emplea por default, con el comando `chsh`. Asi cambia el comando shell

En las distribuciones modernas de Linux no se almacena el password en el archivo `/etc/passwd`. Lo hace en un archivo oculto, es decir, en `/etc/shadow`. El contenido es similar al archivo `/etc/passwd`, pero encambio de la `x` tenemos los passwords en formato sha 256 hash.

La informacion de los grupos se encuentra en el archivo `/etc/group`

**Manejando grupos**

Utilizar el comando `groupadd`

```
groupadd Sales
```

Para observar los grupos creados consultar el archivo `/etc/group`

Borrar un grupo existente `groupdel`

Cambiar el nombre de un grupo con el comando `groupmod`

```
sudo groupmod -n Marketing marketing

tail /etc/group
```
El ultimo comando me permite ver los cambios o modificaciones realizadas.

En linux existen dos tipos de grupos, el primario y el secundario. Cada vez que se crea un usuario se crea de igual manera el grupo con el nombre del usuario. 

Con el siguiente comando se pueden observar el id del nombre. id del grupo primario y id del grupo secundario

```
sudo id htorres
```

Asi como hay password para usuario, tambien hay password para grupos, este es `gpasswd`. Aunque usualmente no se asignan podria hacerlo, pero tambien nos permite agregar otros usuarios al grupo que deseemos. Veamos como agregamos `jdoe` al grupo `Sales`.

```
sudo gpasswd -a jdoe Sales
sudo gpasswd -a jsmith Marketing
```

Para eliminar un usuario de un grupo se utiliza e mismo comando, pero con la opcion `-d`, de la siguiente manera.

```
sudo gpasswd -d jsmith Marketing
```
Si se desea volver un usuario administrador del grupo, se puede hacer a un usuario que ya pertenezca al grupo utilizando el mismo comando, pero con la `A` mayuscula, de la siguiente manera,

```
sudo gpasswd -A jdoe Sales
```

Ahora `jdoe` esta autorizado para agregar y eliminar usuarios en su grupo.

El comando `newgrp` permite el cambio momentaneo de usuario a un grupo secundario. A continuacion cambiando al grupo `Marketing`

```
newgrp Marketing
```
De esta manera podemos crear archivos para diferentes grupos, con este simple comando. Al realizar el listado con `ls -la` podemos ver que el usuario es el mismo, pero los grupos son diferentes.

Podemos cambiar el nombre del grupo al archivo con el siguiente comando

```
chown htorres:Marketing file1.txt
```

Despues de hacer los cambios se regresa al grupo primario, que es el nombre de usuario, con el siguiente comando,

```
newgrp htorres
```

Para conocer el nombre de los grupos existentes en el sistema utilizar `groups`, o para conocer los grupos a los que pertenece un usuarios, asumiendo que tenga permiso para verlos `groups htorres`

Para identificar los usuarios inscritos en los grupos existentes utilizamos el comando

```
tail /etc/group
```

El comando `getent` se utiliza para ver el contenido de los archivos `/etc/passwd`, `/etc/group` y ubicar rapidamente un usuario y su configuracion. Una forma de utilizar el comando es la siguiente.

```
getent passwd htorres
getent group Marketing
sudo getent shadow htorres
```

El anterior comando permite visualizar informacion rapidamente, aunque tambien se puede utilizar `grep` sobre cada uno de los archivos `etc`, veamos,

```
cat /etc/passwd | grep htorres

# equivalente a 
getent passwd htorres

```




<!--
-->
## Which do you use: ip or ifconfig?

Like a lot of users, I learned `ifconfig`, although I don't recall whether it's because the `ip` command didn't exist at the time or whether it just hadn't gained traction. It took a while to get used to `ip`, but when I understood how much `ip` encompassed, I switched over to it as soon as I could find a good cheat sheet for it. I think of `ip` as a suite.`

If you're using `ifconfig` as just a query for an IP address, then `ip addr show` may seem superfluous. But when you're setting network routes and adding interfaces and IP addresses, the `ip` command suite brings your tasks together into a unified interface. For instance, instead of using `ifconfig` and `route`, each with different syntax, you can just use `ip`.

For instance, here's `ifconfig`:

```
$ sudo ifconfig eth0 add 192.168.12.20
$ sudo route add default gw 192.168.12.0 eth0
```

Those are valid commands, but they're not very consistent from the user's perspective. The device definition is front-loaded with `ifconfig` and trailing with `route`.

Here's the same process using `ip`:

```
$ sudo ip addr add 192.168.12.20 dev eth0
$ sudo ip route add 192.168.12.0/24 dev eth0 proto static
```

From a user interface perspective, the `ip` commands have a kind of symmetry. They're practically identical, so once you train yourself to understand the syntax of one `ip` subcommand, you know it for all `ip` subcommands.

And there's a lot you can do with `ip`. Each subcommand has its own manual entry, so you can focus on parsing each command's options without sorting through options that don't apply.

```
$ man ip-route
$ man ip-address
$ man ip-link
```
There's nothing wrong with `ifconfig`, and if it's the command you know and it's the command that's working for you, then keep on using it. But if you're just now learning networking basics on Linux, focus on material that uses the `ip` command, and I believe you'll have an easier time comprehending the different components. Just as importantly, you'll find it easier to remember how to view and modify your network settings with one simple two-letter command: ip.

<!--
-->








