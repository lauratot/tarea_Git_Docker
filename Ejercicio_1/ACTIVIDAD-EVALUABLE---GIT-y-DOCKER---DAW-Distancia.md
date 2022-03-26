---
title: ACTIVIDAD EVALUABLE - GIT y DOCKER - DAW Distancia
author: Laura A. Álvarez Cubillas
tags: [DAW, despliegue, git, docekr, Typora]

---

> ACTIVIDAD EVALUABLE - USO DE GIT + DOCKER - DAW Distancia
>
> Laura A. Álvarez Cubillas
>
> :link:  Video:  





# Resolución Ejercicio 1

## Servidor web

- Arrancar el contenedor `php:7.4-apache`

  - usamos -d para que quede arrancado en background
  - --name para dar nombre al contenedor
  - -p para establecer la conexión entre puertos

  ```bash
  docker run -d --name web -p 8000:80 php:7.4-apache
  ```

  ![image-20220326173859084](ACTIVIDAD-EVALUABLE---GIT-y-DOCKER---DAW-Distancia.assets/image-20220326173859084.png)

Como no tenía la imagen se la ha descargado a la vez que crea el contenedor.

Ahora ya se puede ver la imagen descargada en el equipo con el comando:

```bash
docker images
```



![image-20220326174130740](ACTIVIDAD-EVALUABLE---GIT-y-DOCKER---DAW-Distancia.assets/image-20220326174130740.png)

Comprobamos que el contenedor esta arrancado:

```bash
docker ps -a
```

![image-20220326174605777](ACTIVIDAD-EVALUABLE---GIT-y-DOCKER---DAW-Distancia.assets/image-20220326174605777.png)

Para poder trabajar en el contenedor abrimos una terminal en él con el comando `exec`:

```bash
docker exec -it web bash
```

y ahora estamos dentro del contenedor

![image-20220326175901775](ACTIVIDAD-EVALUABLE---GIT-y-DOCKER---DAW-Distancia.assets/image-20220326175901775.png)

- [x] Creamos el fichero `index.html`, para ello primero actualizo el contenedor e instalo el editor `nano` para editar los archivos que creo con el comando `touch`, la secuencia es:

```bash
apt-get update
apt-get install nano
touch index.html
touch mes.php
nano index.html
```

![image-20220326180900345](ACTIVIDAD-EVALUABLE---GIT-y-DOCKER---DAW-Distancia.assets/image-20220326180900345.png)

![image-20220326182504540_index](ACTIVIDAD-EVALUABLE---GIT-y-DOCKER---DAW-Distancia.assets/image-20220326182504540_index.png)

![image-20220326181103251](ACTIVIDAD-EVALUABLE---GIT-y-DOCKER---DAW-Distancia.assets/image-20220326181103251.png)



- [x] La salida del navegador del archivo `index.html` en el puerto establecido

![image-20220326183245476](ACTIVIDAD-EVALUABLE---GIT-y-DOCKER---DAW-Distancia.assets/image-20220326183245476.png)

- [x] Edición y visualización del archivo `mes.php` , en este caso se escribió la ruta al script en el navegador

![image-20220326182504540](ACTIVIDAD-EVALUABLE---GIT-y-DOCKER---DAW-Distancia.assets/image-20220326182504540.png)

![image-20220326184432663](ACTIVIDAD-EVALUABLE---GIT-y-DOCKER---DAW-Distancia.assets/image-20220326184432663.png)

- [x] La salida del navegador del script mes.php

![image-20220326184512438](ACTIVIDAD-EVALUABLE---GIT-y-DOCKER---DAW-Distancia.assets/image-20220326184512438.png)

- [x] Para ver el tamaño del contenedor después de crear los ficheros usamos el comando siguiente, donde el flag -s nos indica el tamaño de los contenedores que están activos, en este caso lo qu ehemos creado dentro del contenedor son 19.5 MB.

```
docker ps -a -s
```

![image-20220326190601952](ACTIVIDAD-EVALUABLE---GIT-y-DOCKER---DAW-Distancia.assets/image-20220326190601952.png)
