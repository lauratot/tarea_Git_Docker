---
title: ACTIVIDAD EVALUABLE - GIT y DOCKER - DAW Distancia
author: Laura A. Álvarez Cubillas
tags: [DAW, despliegue, git, docker]

---

> Resolución EJERCICIO 2 - ALMACENAMIENTO
>
> Laura A. Álvarez Cubillas
>
> :link:  Video:  





# Resolución Ejercicio 2

## Bind Mount para compartir datos

### Preparación carpetas

Primero preparo el repositorio para trabajar en el Ejercicio 2, cambio de rama en git y creo la carpeta `saludo` y el archivo `index.html` que paso a editar con `nano`

```bash
mkdir saludo
cd saludo
touch index.html
nano index.html
```

![image-20220326201130861](Resolucion%20Ejercicio%202.assets/image-20220326201130861.png)

![image-20220326201226110](Resolucion%20Ejercicio%202.assets/image-20220326201226110.png)

### Creación de contenedores y arranque

- [x] Creo contenedor `c1` con la imagen descargada en el ejercicio 1 y hago bind mount para compartir los datos con la carpeta `saludo` y para escuchar en el puerto 8181 lo que se exponga de ese contenedor.

```bash
docker run --name c1 -p 8181:80 -d -v /home/laura/Documentos/programacion/Despliegue/tarea_Git_Docker/saludo/:/var/www/html php:7.4-apache
```

![image-20220326204754523](Resolucion%20Ejercicio%202.assets/image-20220326204754523.png)

Compruebo que está activo,

```bash
docker ps
```

![image-20220326205122509](Resolucion%20Ejercicio%202.assets/image-20220326205122509.png)

y ejecuto una terminal de `bash` de forma interactiva con `-it` dentro del contenedor `c1` para comprobar que se ha realizado bien el bind mount y listo el contenido de la carpeta. 

Se puede comprobar que el vínculo es correcto porque ya nos aparece el archivo `index.html` que hay dentro de la carpeta `saludo.`

```bash
docker exec -it  c1 bash
```

![image-20220326205631145](Resolucion%20Ejercicio%202.assets/image-20220326205631145.png)



- [x] Creo contenedor `c2` de la misma forma que el anterior pero escuchando en el puerto 8282 y con bind mount a la misma carpeta `saludo`

  ![image-20220326210532428](Resolucion%20Ejercicio%202.assets/image-20220326210532428.png)

Compruebo que están los dos activos, `c1` y `c2`

```bash
docker ps
```

![image-20220326211154594](Resolucion%20Ejercicio%202.assets/image-20220326211154594.png)

Comprobación desde dos ventanas del navegador que se puede acceder al contenido de `index.html` desde `c1` y `c2`

![image-20220326211607025](Resolucion%20Ejercicio%202.assets/image-20220326211607025.png)
