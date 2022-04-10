 - https://youtu.be/OHcU0d-0YmU
 - https://youtu.be/u5rCiyZyHo8
 
 - https://hub.docker.com/publishers/microsoftowner

 - https://hub.docker.com/_/microsoft-mssql-server

Descargar imagen de Sql Server desde Docker Hub:
```
docker pull mcr.microsoft.com/mssql/server
```

Descargar y correr SQL Server en Docker:
```
docker run --name sqlserver -p 1433:1433 -e "ACCEPT_EULA=Y" -e "SA_PASSWORD=Password1!" -d mcr.microsoft.com/mssql/server:2019-latest
```
Ingresar al contenedor de manera interactiva
```
docker exec -it sqlserver /opt/mssql-tools/bin/sqlcmd -S localhost -U sa -P Password1!
```
Crear base de datos:

```
1> CREATE DATABASE MyDockerDatabase;
2> GO
```

Usar la base de datos creada:
```
1> USE MyDockerDatabase;
2> GO
Changed database context to 'MyDockerDatabase'.
```

Crear base de datos de prueba
```
1> CREATE TABLE Customers(Id int , Name varchar(200), DateOfBirth date);
2> GO
```

Setear lenguaje a ingles para no tener problemas con las fechas:
```
1> SET LANGUAGE ENGLISH;
2> GO
Changed language setting to us_english.
```

Insertar datos de prueba en la tabla
```
1> INSERT INTO Customers VALUES(1, 'Benjamin', '1985-12-20'), (2, 'Miriam', '1994-04-20');
2> GO

(2 rows affected)
```