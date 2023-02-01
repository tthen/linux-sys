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








