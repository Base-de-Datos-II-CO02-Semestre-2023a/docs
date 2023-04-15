<!-- Vamos a crear el modelo logico de las entidades que aparecen en ./01analisisEntidades.md, donde cada columna son sus atributos -->

# Modelo Lógico

## SUJETO
Nombre de columna | id | nombre | telefono | correo | codigo_postal | id_ciudad | calle | numero_interno | numero_externo |
|-----------------|----|--------|----------|--------|---------------|----------|-------|---------------|---------------|
|Tipo de llave|PK|||||FK|||
| Nula / Unica | Not Null Unica | Not Null| Not Null| Not Null| Not Null| Not Null| Not Null|Null|Null|
| Tipo de dato | SERIAL | VARCHAR(100) | ENTERO | VARCHAR(256) | ENTERO | VARCHAR | VARCHAR(100) | ENTERO | ENTERO |
| Restricciones | | | | LIKE(* @ * . *) || | | | |
| Datos de ejemplo |1526 | Juan Perez | 5555555555 | juanperez@ejemplo.com | 12345 | CDMX | Calle 1 | 1 | 1 |

## LUGAR
Nombre de columna | id | nombre | telefono | correo | codigo_postal | id_ciudad | calle | numero_interno | numero_externo | tipo | id_responsable | cap_max |
|-----------------|----|--------|----------|--------|---------------|----------|-------|---------------|---------------|-----|---------------|--------|
|Tipo de llave|PK|||||FK|||
| Nula / Unica | Not Null Unica | Not Null| Not Null| Not Null| Not Null| Not Null| Not Null|Null|Null| Not Null| Not Null| Not Null|
| Tipo de dato | SERIAL | VARCHAR(100) | ENTERO | VARCHAR(256) | ENTERO | VARCHAR | VARCHAR(100) | ENTERO | ENTERO | ENUM | SERIAL | ENTERO |
| Restricciones | | | | LIKE(* @ * . *) || | | | |sucursal, almacen, oficina| | |  |
| Datos de ejemplo |1526 | Tienda 1 | 5555555555 | tienda1@empresa.com | 12345 | CDMX | Calle 1 | 1 | 1 | sucursal | 1 | 100 |

## EMPLEADO
|Nombre de columna | id | nombre | telefono | correo | codigo_postal | id_ciudad | calle | numero_interno | numero_externo | nss | rfc | fecha_nacimiento | fecha_ingreso | contrato_activo_id_empleado | contrato_activo_fecha  |  id_lugar | departamento_id | departamento_lugar | indice_productividad |
|-----------------|----|--------|----------|--------|---------------|----------|-------|---------------|---------------|-----|---------------|--------|--------|--------|--------|--------|--------|--------|-------|
|Tipo de llave|PK|||||FK||||||||FK|FK|FK|FK|FK||
| Nula / Unica | Not Null Unica | Not Null| Not Null| Not Null| Not Null| Not Null| Not Null|Null|Null| Not Null| Not Null| Not Null| Not Null| Not Null| Not Null| Null|Null| Null| Not Null|
| Tipo de dato | SERIAL | VARCHAR(100) | ENTERO | VARCHAR(256) | ENTERO | VARCHAR | VARCHAR(100) | ENTERO | ENTERO | ENTERO | VARCHAR(13) | DATE | DATE | SERIAL | DATE | SERIAL | SERIAL | SERIAL | NUMERICO(10,2) |
| Restricciones | | | | LIKE(* @ * . *) |||||||||||||||0 < indiceProbabilidad < 1|
| Datos de ejemplo |1526 | Juan Perez | 5555555555 | juanperez@ejemplo.com | 12345 | CDMX | Calle 1 | 1 | 1 | 123456789 | 123456789 | 1990-01-01 | 2010-01-01 | 1 | 2010-01-01 | 1 | 1 | 1 | 0.5 |
##  CLIENTE
Nombre de columna | id | nombre | telefono | correo | codigo_postal | id_ciudad | calle | numero_interno | numero_externo | rfc | regimen_fiscal |
|-----------------|----|--------|----------|--------|---------------|----------|-------|---------------|---------------|----------|---------------|
|Tipo de llave|PK|||||FK|||||
| Nula / Unica | Not Null Unica | Not Null| Not Null| Not Null| Not Null| Not Null| Not Null|Null|Null|Not Null|Not Null|
| Tipo de dato | SERIAL | VARCHAR(100) | ENTERO | VARCHAR(256) | ENTERO | VARCHAR | VARCHAR(100) | ENTERO | ENTERO | VARCHAR(13) | ENUM |
| Restricciones | | | | LIKE(* @ * . *) || | | | || 601, 603, 605, 606, 607, 608, 610, 611, 612, 614, 615, 616, 620, 621, 622, 623, 624, 625, 626|
| Datos de ejemplo |1526 | Juan Perez | 5555555555 | juanperez@ejemplo.com | 12345 | CDMX | Calle 1 | 1 | 1 | 123456789 | 603 |

## PROVEEDOR
Nombre de columna | id | nombre | telefono | correo | codigo_postal | id_ciudad | calle | numero_interno | numero_externo | rfc | regimen_fiscal | pagina_web |
|-----------------|----|--------|----------|--------|---------------|----------|-------|---------------|---------------|----------|---------------|---------------|
|Tipo de llave|PK|||||FK|||||
| Nula / Unica | Not Null Unica | Not Null| Not Null| Not Null| Not Null| Not Null| Not Null|Null|Null|Not Null|Not Null|Null|
| Tipo de dato | SERIAL | VARCHAR(100) | ENTERO | VARCHAR(256) | ENTERO | VARCHAR | VARCHAR(100) | ENTERO | ENTERO | VARCHAR(13) | ENUM | VARCHAR(256) |
| Restricciones | | | | LIKE(* @ * . *) || | | | || 601, 603, 605, 606, 607, 608, 610, 611, 612, 614, 615, 616, 620, 621, 622, 623, 624, 625, 626| |
| Datos de ejemplo |1526 | Juan Perez | 5555555555 | juanperez@gmail.net| 12345 | CDMX | Calle 1 | 1 | 1 | 123456789 | 603 | www.ejemplo.com |

## ARTICULO
|Nombre de columna |id_articulo |nombre| descripcion |precio_base | categoria | unidad | obj_imp| caracteristicas | porcentaje_iva | porcentaje_ieps | porcentaje_ganancia |
|------------------|---|------|-------------|------------|-----------|--------|--------|----------------|---------------|----------------|--------------------|
|Tipo de llave|PK||FK||FK|FK|||||
| Nula / Unica | Not Null | Not Null| Not Null| Not Null| Not Null| Not Null| Not Null| Not Null| Not Null| Not Null| Not Null|
| Tipo de dato | SERIAL | VARCHAR(50) | ENTERO | DECIMAL(10,2) | VARCHAR(50) | VARCHAR(50) | VARCHAR(50) | VARCHAR(50) | DECIMAL(10,2) | DECIMAL(10,2) | DECIMAL(10,2) |
| Restricciones | | | | >=0| | | | | >=0| >=0| >=0|

## CAT_PROD_SER
|Nombre de columna |clave | descripcion |
|------------------|------|-------------|
|Tipo de llave|PK||
| Nula / Unica | Not Null | Not Null|
| Tipo de dato | ENTERO | VARCHAR(1000) |
| Restricciones | | |
| Datos de ejemplo | 10101500 |Animales vivos de granja|

## CAT_UNIDAD
|Nombre de columna |clave | descripcion |
|------------------|------|-------------|
|Tipo de llave|PK||
| Nula / Unica | Not Null | Not Null|
| Tipo de dato | VARCHAR(30) | VARCHAR(1000) |
| Restricciones | | |
| Datos de ejemplo | KG | Kilogramo |

## GASTOS_EMPLEADO
|Nombre de columna |id_empleado | tipo | 

