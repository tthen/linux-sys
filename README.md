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



