## Descargar una imagen

```
docker pull [nombreImagen]
```
ej:
```
docker pull postgres
```


## Correr una imagen

#### Si una imagen no existe en mi maquina, se va a comenzar a descargar.

#### Cuando se corre una imagen, se hace antes implicitamente un docker pull.

```
docker run [nombreImagen]
```
ej:
```
docker run postgres
```

## Tags - versiones de imagenes
#### Podemos especificar la version a descargar/ejecutar añadiendo dos puntos despues del nombre de la imagen y el nombre de la version.
#### Si no especificamos nada, normalmente descarga la ultima version (latest).
#### La etiqueta latest, se usa para descargar la ultima version que se encuentra en docker hub.

ejp:
```
docker pull postgres:lastest
docker run postgres:14.2-alpine3.15
docker pull node:alpine
docker run node:16
```
## Mostrar todas mis imagenes

```
docker images
```
#### En linux para listar imagenes pero solo mostrar una parte
```
docker images | head
```
#### En powershell para listar imagenes pero solo mostrar una parte
```
docker images | select -first 10
```

## Mostrar los contenedores que estan corriendo
```
docker ps
```
## Mostrar los contenedores que estan corriendo y los que estan parados
```
docker ps -a
```

## Iniciar un contenedor existente
#### Con esto puedo recuperar los datos que se encuentran en ese contenedor.
#### Puedo usar el container Id o el nombre de la imagen

```
docker start [containerId]
docker start [name]
```
ejp:
```
docker start f2a09f7a79bc
docker start strange_galileo
```

## Ver logs de un contenedor
```
docker logs [containerId]
```
ejp:
```
docker logs f2a09f7a79bc
docker logs thirsty_williamson
```
