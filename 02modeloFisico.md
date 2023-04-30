<!-- Vamos a crear el modelo logico de las entidades que aparecen en ./01analisisEntidades.md, donde cada columna son sus atributos -->

# Modelo logico y fisico
## Tabla ciudad
### Modelo logico
|Nombre de la columna | id_ciudad | entidad | pais | nombre |
|---------------------|-----------|---------|------|--------|
|Tipo de llave        |PK         |         |      |        |
| Nula / Unica        | Not Null, Unica  | Not Null| Not Null| Not Null|
| Tipo de dato        | VARCHAR(5) | VARCHAR(1000) | VARCHAR(1000) | VARCHAR(1000) |
| Restricciones       | | | | |
| Datos de ejemplo    | tol | Estado de México | México | Toluca |
### Modelo fisico
```sql
CREATE TABLE ciudad(
    id_ciudad VARCHAR(5) PRIMARY KEY,
    entidad VARCHAR(1000) NOT NULL,
    pais VARCHAR(1000) NOT NULL,
    nombre VARCHAR(1000) NOT NULL
);
```
## Tabla sujeto
### Modelo logico
|Nombre de la columna | id | nombre | telefono | correo | codigo_postal | id_ciudad | calle | numero_interno | numero_externo |
|---------------------|----|--------|----------|--------|---------------|-----------|-------|----------------|----------------|
|Tipo de llave        |PK  |        |          |        |               |FK         |       |                |                |
| Nula / Unica        | Not Null, Unica  | Not Null| Not Null, Unica| Not Null, Unica| Not Null| Not Null| Not Null|||
| Tipo de dato        | SERIAL | VARCHAR(100) | INT | VARCHAR(256) | INT | VARCHAR(5) | VARCHAR(100) | INT | INT |
|Restricciones        | | | | LIKE '%_@%.%' | | | | | |
| Datos de ejemplo    | 1 | Juan Perez | 7221234567 | juanperez@ejemplo.com | 50000 | tol | Morelos | 1 | 2 |

### Modelo fisico
```sql
CREATE TABLE sujeto(
    id SERIAL PRIMARY KEY,
    nombre VARCHAR(100) NOT NULL,
    telefono INT NOT NULL UNIQUE,
    correo VARCHAR(256) check (correo LIKE '%_@%.%')NOT NULL UNIQUE,
    codigo_postal INT NOT NULL,
    id_ciudad VARCHAR CONSTRAINT sujeto_id_ciudad_fk REFERENCES ciudad(id_ciudad) NOT NULL,
    calle VARCHAR(100) NOT NULL,
    numero_interno INT,
    numero_externo INT
);

```

## Tabla externo
> Esta tabla hereda de sujeto
### Modelo logico
| Nombre de la columna | id | nombre | telefono | correo | codigo_postal | id_ciudad | calle | numero_interno | numero_externo | rfc | regimen_fiscal | tipo |
|----------------------|----|--------|----------|--------|---------------|-----------|-------|----------------|----------------|-----|----------------|------|
| Tipo de llave        | PK |        |          |        |               | FK        |       |                |                |     |                |      |
| Nula / Unica         | Not Null, Unica | Not Null | Not Null, Unica | Not Null, Unica | Not Null | Not Null | Not Null | | |Not Null, Unica | Not Null | Not Null |
| Tipo de dato         | SERIAL | VARCHAR(100) | INT | VARCHAR(256) | INT | VARCHAR(5) | VARCHAR(100) | INT | INT | VARCHAR(13) | tipo_regimen | tipo_cliente |
| Restricciones        | | | | LIKE '%_@%.%' | | | | | | | | |
| Datos de ejemplo     | 1 | Juan Perez | 7221234567 | juanperez@ejemplo.com | 50000 | tol | Morelos | 1 | 2 | PERJ000101000 | 601 | Cliente |

### Modelo fisico

```sql
CREATE TYPE tipo_regimen AS ENUM ('601', '602', '603', '604', '605', '606', '607', '608', '609', '610', '611', '612', '613', '614', '615', '616', '617', '618', '619', '620', '621', '622', '623', '624', '625', '626');

CREATE TYPE tipo_cliente AS ENUM ('Cliente','Provedor');

CREATE TABLE externo(
    id SERIAL PRIMARY KEY,
    rfc VARCHAR(13) NOT NULL UNIQUE,
    regimen_fiscal TIPO_REGIMEN NOT NULL,
    tipo TIPO_CLIENTE NOT NULL
) inherits (sujeto);
```

## Tabla lugar
> Esta tabla hereda de sujeto
### Modelo logico
| Nombre de la columna | id | nombre | telefono | correo | codigo_postal | id_ciudad | calle | numero_interno | numero_externo | tipo | id_responsable | cap_almacenamiento_max |
|----------------------|----|--------|----------|--------|---------------|-----------|-------|----------------|----------------|------|----------------|------------------------|
| Tipo de llave        | PK |        |          |        |               | FK        |       |                |                |      | FK             |                        |
| Nula / Unica         | Not Null, Unica | Not Null | Not Null, Unica | Not Null, Unica | Not Null | Not Null | Not Null || | Not Null | Not Null | Not Null |
| Tipo de dato         | SERIAL | VARCHAR(100) | INT | VARCHAR(256) | INT | VARCHAR(5) | VARCHAR(100) | INT | INT | TIPO_LUGAR | INT | NUMERIC(10,2) |
| Restricciones        | | | | LIKE '%_@%.%' | | | | | | | | |
| Datos de ejemplo     | 1 | Tienda 2 | 7221234567 | tienda2@ejemplo.com | 50000 | tol | Morelos | 1 | 2 | sucursal | 1 | 1000 |

### Modelo fisico

```sql
CREATE TYPE tipo_lugar AS ENUM('sucursal','almacen','oficina');

CREATE TABLE lugar(
    id SERIAL PRIMARY KEY,
    tipo tipo_lugar NOT NULL,
    id_responsable INTEGER NOT NULL,
    cap_almacenamiento_max NUMERIC(10,2) NOT NULL
) INHERITS (sujeto);
```

## Tabla registro_contratos
### Modelo logico
| Nombre de la columna | id | id_empleado | fecha_inicio | fecha_fin | puesto | salario | dias_vacaciones |
|----------------------|----|-------------|--------------|-----------|--------|---------|-----------------|
| Tipo de llave        | PK |FK           |             |           |        |         |                 |
| Nula / Unica         | Not Null, Unica | Not Null | Not Null | Not Null | Not Null | Not Null | Not Null |
| Tipo de dato         | SERIAL | INT | DATE | DATE | TIPO_PUESTO | NUMERIC(10,2) | INT |
| Restricciones        | | | | | | salario >= 0 | dias_vacaciones >= 0 |
| Datos de ejemplo     | 1 | 1 | 2020-01-01 | 2020-12-31 | Mostrador | 5000 | 10 |

### Modelo fisico
```sql
CREATE TYPE tipo_puesto AS ENUM('Mostrador','Recursos_Humanos','Finanzas','Almacen','Admin');

CREATE TABLE registro_contratos(
    id SERIAL PRIMARY KEY,
    id_empleado INTEGER NOT NULL,
    fecha_inicio DATE NOT NULL,
    fecha_fin DATE NOT NULL,
    puesto TIPO_PUESTO NOT NULL,
    salario NUMERIC (10,2) check ( salario >= 0) NOT NULL,
    dias_vacaciones INT check (dias_vacaciones >= 0)NOT NULL
);
```
## Tabla modificacion

### Modelo logico
| Nombre de la columna | id_contrato | changed_on | modificaciones |
|----------------------|-------------|------------|----------------|
| Tipo de llave        | PK, FK      | PK         |                |
| Nula / Unica         | Not Null    | Not Null   | Not Null       |
| Tipo de dato         | INT         | TIMESTAMP  | JSON           |
| Restricciones        |             |            |                |
| Datos de ejemplo     | 1           | 2023-04-29 15:56:27.464955 | {'salario':5200,'dias_vacaciones':11}         |

### Modelo fisico
```sql

CREATE TABLE modificacion(
    id_contrato INT CONSTRAINT id_contrato_fk REFERENCES registro_contratos(id) NOT NULL,
    changed_on TIMESTAMP(6) NOT NULL,
    modificaciones JSON NOT NULL,
    PRIMARY KEY (id_contrato, changed_on)
);

```

## Tabla empleado
> Esta tabla hereda de sujeto
### Modelo logico
| Nombre de la columna | id | nombre | telefono | correo | codigo_postal | id_ciudad | calle | numero_interno | numero_externo | nss | password | rfc | fecha_de_nacimiento | fecha_de_ingreso | contrato | indice_productividad |
|----------------------|----|--------|----------|--------|---------------|-----------|-------|----------------|----------------|-----|----------|-----|---------------------|------------------|----------|----------------------|
| Tipo de llave        | PK |        |          |        |               | FK        |       |                |                |     |          |     |                     |                  | FK       |                      |
| Nula / Unica         | Not Null, Unica | Not Null | Not Null, Unica | Not Null, Unica | Not Null | Not Null | Not Null || | Not Null, Unica | Not Null | Not Null, Unica | Not Null | Not Null | Not Null |Not Null|
| Tipo de dato         | SERIAL | VARCHAR(100) | INT | VARCHAR(256) | INT | VARCHAR(5) | VARCHAR(100) | INT | INT | INT | CHAR(64) | VARCHAR(13) | DATE | DATE | INT | NUMERIC(10,2) |
| Restricciones        | | | | LIKE '%_@%.%' | ||||||||| | |BETWEEN 0 AND 1 |
| Datos de ejemplo     | 1 | Juan Perez | 7221234567 | ejemplo@empresa.com | 50000 | tol | Morelos | 1 | 2 | 1234567890 |bd4526534df7b33772c2f1ee26d97c39ff11379c8848e4e19d74ad849ef66423| 1234567890123 | 1999-01-01 | 2020-01-01 | 1 | 0.5 |

### Modelo fisico

```sql
CREATE TABLE empleado(
    id SERIAL PRIMARY KEY,
    nss INT NOT NULL UNIQUE,
    password CHAR(64) NOT NULL,
    rfc VARCHAR(13) NOT NULL UNIQUE,
    fecha_de_nacimiento DATE NOT NULL,
    fecha_de_ingreso DATE NOT NULL,
    contrato INTEGER CONSTRAINT contrato_fk REFERENCES registro_contratos(id)NOT NULL,
    indice_productividad NUMERIC(10,2) check (indice_productividad BETWEEN 0 AND 1) NOT NULL
) INHERITS (sujeto);
```

#### Llaves foraneas

```sql
alter table lugar 
  add constraint lugar_responsable_fk 
  foreign key (id_responsable)
  REFERENCES empleado(id);

alter table registro_contratos 
  add constraint registro_contrato_id_empleado_fk 
  foreign key (id_empleado) 
  REFERENCES empleado(id);
```
## Tabla prestaciones

### Modelo logico
| Nombre de la columna | id_empleado | concepto | descripcion | total | fecha |
|----------------------|-------------|----------|-------------|-------|-------|
| Tipo de llave        | PK, FK      |          |             |       | PK    |
| Nula / Unica         | Not Null    | Not Null |             | Not Null | Not Null |
| Tipo de dato         | INT         | ENUM     | VARCHAR(1000) | NUMERIC(10,2) | DATE |
| Restricciones        |             |          |             | total >= 0 | |
| Datos de ejemplo     | 1 | Nomina | Pago de nomina | 5000 | 2020-01-01 |

### Modelo fisico
```sql
CREATE TYPE tipo_gasto_empleado AS ENUM('Nomina','Seguro','Afore','Prima_Vacacional');

CREATE TABLE prestaciones(
    id_empleado INTEGER CONSTRAINT lugar_ REFERENCES empleado(id) NOT NULL,
    concepto tipo_gasto_empleado NOT NULL,
    descripcion VARCHAR(1000),
    total NUMERIC (10,2) CHECK (total >= 0 )NOT NULL,
    fecha DATE NOT NULL,
    PRIMARY KEY(id_empleado, fecha)
);
```

## Tabla registro_vacaciones

### Modelo logico
| Nombre de la columna | id_empleado | fecha_inicio | fecha_fin |
|----------------------|-------------|--------------|-----------|
| Tipo de llave        | PK, FK      | PK           |           |
| Nula / Unica         | Not Null    | Not Null     | Not Null  |
| Tipo de dato         | INT         | DATE         | DATE      |
| Restricciones        |             |              |           |
| Datos de ejemplo     | 1           | 2020-01-01   | 2020-01-15|

### Modelo fisico
```sql
CREATE TABLE registro_vacaciones(
    id_empleado INTEGER CONSTRAINT registro_vacaciones_id_empleado_fk REFERENCES empleado(id) NOT NULL,
    fecha_inicio DATE NOT NULL,
    fecha_fin DATE NOT NULL,
    PRIMARY KEY(id_empleado, fecha_inicio)
);
```
## Tabla gasto_lugar
### Modelo logico
| Nombre de la columna | id_lugar | descripcion | monto | tipo | fecha |
|----------------------|----------|-------------|-------|------|-------|
| Tipo de llave        | PK, FK   |             |       |      | PK    |
| Nula / Unica         | Not Null | Not Null    | Not Null | Not Null | Not Null |
| Tipo de dato         | INT      | VARCHAR(1000) | NUMERIC(10,2) | tipo_gasto_lugar | DATE |
| Restricciones        |          |              | CHECK (monto >= 0) || |
| Datos de ejemplo     | 1        | Luz      | 50000 | fijo | 2020-01-01 |

### Modelo fisico
```sql
CREATE TYPE tipo_gasto_lugar AS ENUM('fijo','variable');

CREATE TABLE gastos_lugar(
    id_lugar INTEGER CONSTRAINT gastos_lugar_id_fk REFERENCES lugar(id) NOT NULL,
    descripcion VARCHAR(1000) NOT NULL,
    monto NUMERIC(10,2) check(monto >= 0)NOT NULL,
    tipo tipo_gasto_lugar NOT NULL,
    fecha DATE NOT NULL,
    PRIMARY KEY (tipo, fecha)
);
```


## Tabla falta

### Modelo logico
| Nombre de la columna | id_empleado | tipo | fecha | descripcion | impacto_productividad |
|----------------------|-------------|------|-------|-------------|-----------------------|
| Tipo de llave        | PK, FK      |PK      | PK    |             |                       |
| Nula / Unica         | Not Null    | Not Null | Not Null | Not Null | Not Null |
| Tipo de dato         | INT         | tipo_falta | DATE | VARCHAR(1000) | NUMERIC(10,2) |
| Restricciones        |             |          |       |             | impacto_productividad >= 0 |

### Modelo fisico
```sql
CREATE TYPE tipo_falta AS ENUM('falta','retardo');

CREATE TABLE falta(
    id_empleado INTEGER CONSTRAINT falta_id_empleado_fk REFERENCES empleado(id) NOT NULL,
    tipo tipo_falta NOT NULL,
    fecha DATE NOT NULL,
    descripcion VARCHAR(1000) NOT NULL,
    impacto_prodcuitividad NUMERIC(10,2) check(impacto_prodcuitividad >= 0) NOT NULL,
    PRIMARY KEY (id_empleado, tipo, fecha)
);
```

## Tabla objetivo

### Modelo logico
| Nombre de la columna | id | id_empleado | descripcion | porcentaje_avance | impacto_productividad |
|----------------------|----|-------------|-------------|-------------------|-----------------------|
| Tipo de llave        | PK | FK          |             |                   |                       |
| Nula / Unica         | Not Null, UNIQUE | Not Null    | Not Null    | Not Null | Not Null |
| Tipo de dato         | INT | INT         | VARCHAR(1000) | NUMERIC(10,2) | NUMERIC(10,2) |
| Restricciones        |    |             |             | porcentaje_avance BETWEEN 0 AND 1| impacto_productividad BETWEEN 0 AND 1 |
| Datos de ejemplo     | 1  | 1           | Aumentar ventas en 10% | 0.7 | .5 |
```sql

CREATE TABLE objetivo(
    id SERIAL PRIMARY KEY,
    id_empleado INTEGER CONSTRAINT objetivo_id_empleado_fk REFERENCES empleado(id) NOT NULL,
    descripcion VARCHAR(1000) NOT NULL,
    porcentaje_avance NUMERIC(10,2) CHECK (porcentaje_avance BETWEEN 0 AND 1) NOT NULL,
    impacto_productividad NUMERIC(10,2) CHECK (impacto_productividad >= 0) NOT NULL
);

```

### Tabla control_asistencia

```sql
CREATE TYPE tipo_asistencia AS ENUM('entrada','salida');

CREATE TABLE control_asistencia(
    id_empleado INTEGER CONSTRAINT objetivo_id_empleado_fk REFERENCES empleado(id) NOT NULL,
    fecha DATE NOT NULL,
    hora TIME NOT NULL,
    tipo TIPO_ASISTENCIA NOT NULL
);
```
### Tabla cat_prod_ser
```sql
CREATE TABLE cat_prod_ser(
    clave INT PRIMARY KEY,
    descripción VARCHAR(1000) NOT NULL
);
```

### Tabla articulo

```sql
CREATE TYPE impuesto AS ENUM('00','01','02','03','04');
CREATE TYPE tipo_unidad AS ENUM('kilogramos','kilos','litros','mililitros','metros','centimetros');
CREATE TABLE articulo(
    id INT PRIMARY KEY,
    nombre VARCHAR(50) NOT NULL,
    descripcion INT CONSTRAINT articulo_descripcion_prod_ser_fk REFERENCES cat_prod_ser(clave) NOT NULL,
    unidad TIPO_UNIDAD NOT NULL,
    volumen NUMERIC(10,2),
    obj_imp impuesto NOT NULL,
    caracteristicas JSON NOT NULL,
    precio_base NUMERIC(10,2) NOT NULL,
    porcentaje_iva NUMERIC(10,2) check(porcentaje_iva >= 0) NOT NULL,
    porcentaje_ieps NUMERIC(10,2) check(porcentaje_ieps >= 0) NOT NULL,
    porcentaje_ganancia NUMERIC(10,2) check(porcentaje_ganancia BETWEEN 0 AND 1) NOT NULL
);
```

### Tabla inventario

```sql
CREATE TABLE inventario(
    cantidad INT NOT NULL,
    descuento NUMERIC(10,2),
    id_lugar INTEGER CONSTRAINT inventario_lugar_id_fk REFERENCES lugar(id) NOT NULL,
    id_articulo INTEGER CONSTRAINT inventario_id_articulo_fk REFERENCES articulo(id) NOT NULL,
    caducidad DATE,
    PRIMARY KEY(id_lugar, id_articulo, caducidad)
);
```
### Tabla movimiento
```sql

CREATE TABLE movimiento(
    id SERIAL PRIMARY KEY,
    cantidad_conceptos INT CHECK (cantidad_conceptos >= 0) NOT NULL,
    id_lugar INTEGER CONSTRAINT movimiento_id_lugar_fk REFERENCES lugar(id) NOT NULL,
    fecha DATE NOT NULL,
    hora TIME NOT NULL
);
```
### Tabla traslado

```sql

CREATE TABLE traslado(
    id INTEGER PRIMARY KEY,
    id_lugar INTEGER CONSTRAINT movimiento_id_lugar_fk REFERENCES lugar(id) NOT NULL,
    id_empleado INTEGER CONSTRAINT traslado_id_empleado_fk REFERENCES empleado(id) NOT NULL,
    destino INTEGER CONSTRAINT destino_destino_fk REFERENCES lugar(id) NOT NULL
) INHERITS (movimiento);
```
### Tabla perdidas
```sql

CREATE TYPE tipo_perdida AS ENUM('robo','caducado');

CREATE TABLE perdida(
    id INTEGER PRIMARY KEY,
    id_lugar INTEGER CONSTRAINT movimiento_id_lugar_fk REFERENCES lugar(id) NOT NULL,
    movimiento_perdida tipo_perdida NOT NULL,
    total_perdida NUMERIC(10,2) CHECK (total_perdida >= 0) NOT NULL
) INHERITS (movimiento);
```
  
### Tabla reabastecimiento 

```sql
CREATE TABLE reabastecimiento(
    id INTEGER PRIMARY KEY,
    id_lugar INTEGER CONSTRAINT movimiento_id_lugar_fk REFERENCES lugar(id) NOT NULL,
    id_provedor INTEGER CONSTRAINT reabastecimiento_id_provedor_fk REFERENCES externo(id) NOT NULL,
    total_compra NUMERIC(10,2) CHECK (total_compra >= 0) NOT NULL,
    fecha DATE NOT NULL
) INHERITS (movimiento);
```

### Tabla ventas

```sql
CREATE TYPE tipo_pago AS ENUM('efectivo','tarjeta','transferencia');

CREATE TABLE venta(
    id INTEGER PRIMARY KEY,
    id_lugar INTEGER CONSTRAINT movimiento_id_lugar_fk REFERENCES lugar(id) NOT NULL,
    id_empleado INTEGER CONSTRAINT venta_id_empleador_fk REFERENCES empleado(id) NOT NULL,
    id_cliente INTEGER CONSTRAINT venta_id_cliente_fk REFERENCES externo(id) NOT NULL,
    numero_factura INT NOT NULL,
    subtotal NUMERIC(10,2) CHECK (subtotal >= 0) NOT NULL,
    iva NUMERIC(10,2) CHECK (iva >= 0) NOT NULL,
    total NUMERIC(10,2) CHECK (total >= 0) NOT NULL,
    metodo_pago tipo_pago NOT NULL
) INHERITS (movimiento);
```
### Tabla concepto
```sql
CREATE TYPE tipo_movimiento AS ENUM('Venta','Translado','Reabastecimiento','Perdida');

CREATE TABLE concepto(
    cantidad INT NOT NULL,
    id_articulo INT CONSTRAINT concepto_id_articulo_fk REFERENCES articulo(id),
    id_movimiento INT NOT NULL ,
    caducidad DATE,
    precio_unitario NUMERIC(8,2) NOT NULL,
    tipo tipo_movimiento NOT NULL,
    monto NUMERIC(10,2) NOT NULL,
    PRIMARY KEY (id_articulo, id_movimiento),
    CONSTRAINT concepto_movimiento_fk FOREIGN KEY (id_movimiento) references movimiento(id)
);
```
