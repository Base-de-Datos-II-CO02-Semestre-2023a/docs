# Documentacion Técnica

El proyecto esta dividido en tres partes, el backend, el frontend y la base de datos.

El backend se desarrolla en Java con el framework Spring Boot.

El frontend se desarrolla en JavaScript, haciendo uso de TypeScript, la libreria React y el framework Remix.

La base de datos se desarrolla en PostgreSQL.

## Indice
- [Backend](/backend/index.md)
- [Frontend](/frontend/index.md)

## Vista general del sistema

``` mermaid
flowchart LR
c[Cliente]
s[Servidor]
b[(Base de datos)]
e[(Base de datos de desarrollo)]
u([Usuario])
d([Cliente externo])

c<--->s
s---b & e
d<--->s
u---c
```

Como podemos ver, no solo el cliente desarrollado por nosotros puede acceder al sistema, se deja preparado para que
clientes de terceros desarrollen sus propias soluciones y no tengan que desarrollar el backend.

Este diseño se puede aprovechar al poblar la base de datos, pues, solo se hace la llamada a la API y ya no nos preocupamos
por conecciones con la base de datos.

Decidimos utilizar una base de datos de desarrollo para agilizar el proceso de desarrollo y minimizar los problemas de
conexión, version y disponibilidad de la base de datos, para lograr esto utilizamos una instancia de 
`Azure Database for PostgreSQL flexible server` aprovechando la version gratuita que proporcionan a estudiantes (lo mejor:
no nos piden tarjeta ☺️).