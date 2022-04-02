---
title: Resolucion_Ejercicio3
author: Laura A. Álvarez Cubillas
tags: [DAW, despliegue, git, docker, Typora]

---

> Resolucion_Ejercicio3
>
> Laura A. Álvarez Cubillas
>





# Resolución Ejercicio 3 - REDES

## Creación de una red

Creo una red bridge propia llamada `redbd` y reviso que se crea listando las redes de docker

```bash
docker network create redbd
docker network ls
```

![image-20220402195501162](Resolucion_Ejercicio3.assets/image-20220402195501162.png)

## Creación de contenedores en red

- [x] Creo contenedor de mariaDB en la red creada `redbd` con `--network`, asociado con `-v` a un volumen llamado `redes`y a la carpeta `/var/lib/mysql` según instrucciones de la imagen; con `--name` lo llamo `lauraBD`, con `-e` detallo las variables de entorno (en este caso solo ponemos la clave para el usuario root) y que corra en segundo plano con `-d`

  ```bash
  docker run -d --name lauraBD -v redes:/var/lib/mysql -e MARIADB_ROOT_PASSWORD=laura_pass --network redbd mariadb
  ```

  ![image-20220402195825900](Resolucion_Ejercicio3.assets/image-20220402195825900.png)

- [x] Creo contenedor con Adminer en la misma red `redbd` para que se pueda conectar con el creado de mariaDB, este se llama `lauraAdminer`

  Además de los flag usados al crear el contenedor de mariadb ahora se usa `--link` para asociar las bases de datos `db` a gestionar con Adminar que estarán en el contenedor de MariaDB `lauraBD`, y se accede por el puerto 8080 con `-p`

  ```bash
  docker run -d --name lauraAdminer --network redbd --link lauraBD:db -p 8080:8080 adminer
  ```

  ![image-20220402200222053](Resolucion_Ejercicio3.assets/image-20220402200222053.png)

  > al crear este contenedor no hace pull de la imagen porque hice varias pruebas primero y ya estaba la imagen en local

- [x] Podemos ver los dos contenedores corriendo con:

  ```bash
  docker ps
  ```

  ![image-20220402202101155](Resolucion_Ejercicio3.assets/image-20220402202101155.png)

  ### Comprobaciones

- [x] Compruebo que los dos contenedores están dentro de la misma red, para ello entro en el contenedor `lauraBD` e intento ver a `lauraAdminer`

  ```bash
  docker exec -it lauraBD bash
  ```
  
  ![image-20220402203206333](Resolucion_Ejercicio3.assets/image-20220402203206333.png)

- [x] actualizo e instalo los paquetes necesarios para hacer comprobaciones de red

  ```bash
  apt-get update
  apt-get install net-tools
  apt-get install dnsutils
  apt-get install iputils-ping
  nslookup lauraAdminer
  ping lauraAdminer

![image-20220402203257872](Resolucion_Ejercicio3.assets/image-20220402203257872.png)

![image-20220402203409461](Resolucion_Ejercicio3.assets/image-20220402203409461.png)

![image-20220402203615370](Resolucion_Ejercicio3.assets/image-20220402203615370.png)

![image-20220402203517586](Resolucion_Ejercicio3.assets/image-20220402203517586.png)

![image-20220402204040346](Resolucion_Ejercicio3.assets/image-20220402204040346.png)

![image-20220402204215178](Resolucion_Ejercicio3.assets/image-20220402204215178.png)

## Trabajo con los contenedores

- [x] Accedo a Adminer desde el navegador y  creo una base de datos.

![image-20220402204445760](Resolucion_Ejercicio3.assets/image-20220402204445760.png)

![image-20220402204956450](Resolucion_Ejercicio3.assets/image-20220402204956450.png)

![image-20220402205115513](Resolucion_Ejercicio3.assets/image-20220402205115513.png)

![image-20220402205320030](Resolucion_Ejercicio3.assets/image-20220402205320030.png)

- [x] Comprobación de que se ha creado la base de datos en `lauraBD`, ejecuto una terminal en ese contenedor y entramos en mysql

```bash
docker exec -it lauraBD bash
mysql -uroot -plaura_pass
show databases;
```

![image-20220402205950400](Resolucion_Ejercicio3.assets/image-20220402205950400.png)

## Borrado contenedores, red y volumen

- [x] Primero borro los contenedores, como están corriendo fuerzo el borrado y a continuación lo compruebo

  ```bash
  docker rm -f lauraBD lauraAdminer
  docker ps
  ```
  

![image-20220402212433293](Resolucion_Ejercicio3.assets/image-20220402212433293.png)

- [x] Borro la red y compruebo

  ```
  docker network rm redbd
  docker network ls
  ```

![image-20220402212955068](Resolucion_Ejercicio3.assets/image-20220402212955068.png)

- [x] Borro el volumen usado y compruebo

  ```bash
  docker volume rm redes
  docker network ls
  ```

![image-20220402213440588](Resolucion_Ejercicio3.assets/image-20220402213440588.png)