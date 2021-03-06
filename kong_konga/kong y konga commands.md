## Listar las redes en docker
```
docker network ls
```
## Remover si aparece una red llamada 'kong-net'
```
docker network rm kong-net
```

## Crear una red llamada 'kong-net'
```
docker network create kong-net
```

## Correr PostgreSQL
```
docker run -d --name kong-database --network=kong-net -p 5432:5432 -e "POSTGRES_USER=kong" -e "POSTGRES_DB=kong" -e "POSTGRES_PASSWORD=MyPostgreSQLPassword" postgres:9.6
```

## Descargar Kong y ejecutar migracion en base de datos
```
docker run --rm --link kong-database:kong-database --network=kong-net -e "KONG_DATABASE=postgres" -e "KONG_PG_HOST=kong-database" -e "KONG_PG_PASSWORD=MyPostgreSQLPassword" kong:latest kong migrations bootstrap
```
## Iniciar un contenedor Kong, que se conectará a su contenedor de base de datos:

docker run -d --name kong 
--network=kong-net 
-e "KONG_DATABASE=postgres" 
-e "KONG_PG_HOST=kong-database" 
-e "POSTGRES_USER=kong" 
-e "KONG_PG_PASSWORD=MyPostgreSQLPassword" 
-e "KONG_PROXY_ACCESS_LOG=/dev/stdout" 
-e "KONG_ADMIN_ACCESS_LOG=/dev/stdout"
-e "KONG_PROXY_ERROR_LOG=/dev/stderr" 
-e "KONG_ADMIN_ERROR_LOG=/dev/stderr" 
-e "KONG_ADMIN_LISTEN=0.0.0.0:8001, 0.0.0.0:8444 ssl" 
-p 8000:8000 
-p 8443:8443 
-p 8001:8001 
-p 8444:8444 
kong:latest

```
docker run -d --name kong --network=kong-net -e "KONG_DATABASE=postgres" -e "KONG_PG_HOST=kong-database" -e "POSTGRES_USER=kong" -e "KONG_PG_PASSWORD=MyPostgreSQLPassword" -e "KONG_PROXY_ACCESS_LOG=/dev/stdout" -e "KONG_ADMIN_ACCESS_LOG=/dev/stdout" -e "KONG_PROXY_ERROR_LOG=/dev/stderr" -e "KONG_ADMIN_ERROR_LOG=/dev/stderr" -e "KONG_ADMIN_LISTEN=0.0.0.0:8001, 0.0.0.0:8444 ssl" -p 8000:8000 -p 8443:8443 -p 8001:8001 -p 8444:8444 kong:latest
```

## Preparar la base de datos de Konga iniciando un contenedor corto:

docker run --rm 
--network=kong-net 
pantsel/konga -c prepare -a postgres -u postgresql://kong@kong-database:5432/konga_db

```
docker run -d -p 1337:1337 --network=kong-net --name konga -v /var/data/kongadata:/app/kongadata -e "NODE_ENV=development" pantsel/konga

```

=========================================================================================
## Solución en github
```
https://github.com/Kong/kong/issues/4363

docker run -d --name kong-database --network=kong-net -p 5555:5432 -e "POSTGRES_USER=kong" -e "POSTGRES_DB=kong" -e "POSTGRES_PASSWORD=helloworld" postgres:9.6

docker run --rm --link kong-database:kong-database --network=kong-net -e "KONG_DATABASE=postgres" -e "KONG_PG_HOST=kong-database" -e "KONG_PG_PASSWORD=helloworld" kong:latest kong migrations bootstrap
```


