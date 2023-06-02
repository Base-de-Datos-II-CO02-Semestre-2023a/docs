# AgenteP

Este es el sistema que se encarga de procesar los datos, manejar las peticiones del cliente y asegurar la seguridad de
los datos.

Se implementa mediante una API REST, dando así flexibilidad al equipo frontend para trabajar con el stack que más le 
convenga

A continuacion describiremos los endpoints que se implementan, listandolos de la siguiente manera {METODO} {direccion}:

## POST /auth/login
Proporciona informacion necesaria para el manejo de sesiones, cualquier persona puede hacer peticion, no es necesario 
que se incluya autenticacion en esta misma.
### Cuerpo de la petición
```json
{
  "rfc": string,
  "password":string
}
```
### Cuerpo de la respuesta
```json
{
    "rfc":string,
    "jwt_token":string,
    "puesto": string
}
```
Tome en cuenta que el valor del puesto proviene del enum `tipo_puesto` de la base de datos, nunca tomará un valor distinto.

## POST /auth/register
Se encarga de crear un Empleado, este regresa el estado de la operacion (400 si no fue autorizado, 200 si se efectuo con
exito o 500 si se presento algun error a la hora de registrarlo).

En este es necesario mandar un token de autorizacion, este es el generado por el endpoint anterior, esto debido a que solamente
los empleados con puesto `Recursos_Humanos` y `Admin` pueden registrar nuevos empleados.
## Header de la peticion
```json
{
  ...,
  "Authorization": "Bearer {token}"
}
```

## Cuerpo de la peticion
```json
{
  "nombre": string,
  "telefono": number,
  "correo": string,
  "codigoPostal": number,
  "idCiudad": string,
  "calle": string,
  "numeroInterno": number o null,
  "numeroExterno": number o null,
  "nss": number,
  "password": string,
  "rfc": string,
  "fechaDeIngreso": date,
  "fechaDeNacimiento": date,
  "indiceEroductividad": number (1 por default)
}
```
