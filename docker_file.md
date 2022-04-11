# Docker File
### Tiene que llamarse si o si 'Dockerfile', sin ninguna extension

## FROM

Indicamos la imagen padre que vamos a usar, y vamos a basar nuestar aplicación.
Puede ser una imagen nuestra custom, o otra imagen que creo otra persona, pero lo mas comun es que sea una imagen extraida de docker hub.
### Siempre tratar de buscar una imagen Alpine (es una distribucion muy ligera de linux (como 6MB) especialmente para containers)
### Puede que haya algunas diferencias entre alpine y ubuntu, asi que si hay problemas con alpine, usar ubuntu
```
FROM [nombreImagen]:[tag]
```
Ejp:
```
FROM node:12.22.1-alpine93.11
```
## WORKDIR
Declaramos donde vamos a poner todo nuestro trabajo.
Si no existe se crea el directorio, y todos los comandos a partir de alli, van a correr en ese directorio.
```
WORKDIR [directorio]
```
Ejp:
```
WORKDIR /app
```

## COPY
Copia todos los archivos que tenga en el directorio donde esta el DockerFile dentro del directorio de trabajo del contenedor.
```
COPY [DockerfileDirectorio] [ContenedorDirectorio]
```
Ejp:
```
COPY . .
COPY . /app
```

## RUN
Va a correr y compilar (build), todo lo que tengamos en nuestro código
```
RUN [comandoDeCompilacion] 
```
Ejp:
```
RUN yarn install --production
```

## CMD
Al final necesitamos expecificar el comando que va a correr.
```
CMD [comando] [argumentos] 
```
Ejp:
```
CMD ["node", "/app/src/index.js"]
```

## ENTRYPOINT
Es similar al CMD solo que deja abierto los argumentos, para cuando hagamos un 'docker run imagen [argumentos]', si o si tengamos que pasar los argumentos.
De esta manera lo hace mas generico.

```
ENTRYPOINT [ejecutable] [parametro1] [parametro2] 
```
Ejp:
```
ENTRYPOINT ["/bin/echo", "Hello World"]
```