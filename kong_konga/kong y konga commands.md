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


=========================================================================================
## Solución en github
```
https://github.com/Kong/kong/issues/4363

docker run -d --name kong-database --network=kong-net -p 5555:5432 -e "POSTGRES_USER=kong" -e "POSTGRES_DB=kong" -e "POSTGRES_PASSWORD=helloworld" postgres:9.6

docker run --rm --link kong-database:kong-database --network=kong-net -e "KONG_DATABASE=postgres" -e "KONG_PG_HOST=kong-database" -e "KONG_PG_PASSWORD=helloworld" kong:latest kong migrations bootstrap
```


