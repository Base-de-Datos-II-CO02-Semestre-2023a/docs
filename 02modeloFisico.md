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
| Tipo de dato | SERIAL | VARCHAR(50) | ENTERO | NUMERICO(10,2) | ENTERO | VARCHAR(50) | ENUM | JSON | NUMERICO(10,2) | NUMERICO(10,2) | NUMERICO(10,2) |
| Restricciones | | | | >=0| | | 00, 01,02,03,04| | >=0| >=0| >=0|
| Datos de ejemplo | 1 | Caja de carton | 10101501 | 100 | 10101500 | KG | 00 | {"color":"rojo","tamaño":"grande"} | 0.16 | 0.16 | 0.16 |

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
|Nombre de columna |id_empleado | tipo | total | fecha |
|------------------|------------|------|-------|-------|
|Tipo de llave|PK, FK|PK | |PK|
| Nula / Unica | Not Null | Not Null| Not Null| Not Null|
| Tipo de dato | SERIAL | ENUM | NUMERICO(10,2) | DATE |
| Restricciones | | nomina, seguro, afore, prima_vacacional | >=0| |
| Datos de ejemplo | 1 | nomina | 1000.00 | 2020-01-01 |

## CONTRATO
|Nombre de columna | id_empleado | fecha_inicio | fecha_fin | puesto | salario | dias_vacaciones |
|------------------|-------------|--------------|-----------|--------|---------|-----------------|
|Tipo de llave|PK, FK| | |PK| | |
| Nula / Unica | Not Null | Not Null| Not Null| Not Null| Not Null| Not Null|
| Tipo de dato | SERIAL | DATE | DATE | VARCHAR(50) | NUMERICO(10,2) | ENTERO |
| Restricciones | | | | | >=0| >=0|
| Datos de ejemplo | 1 | 2020-01-01 | 2021-01-01 | Gerente | 1000.00 | 15 |

## REGISTRO_VACACIONES
|Nombre de columna | id_empleado | fecha_inicio | fecha_fin |
|------------------|-------------|--------------|-----------|
|Tipo de llave|PK, FK|PK| |
| Nula / Unica | Not Null | Not Null| Not Null|
| Tipo de dato | SERIAL | DATE | DATE |
| Restricciones | | | |
| Datos de ejemplo | 1 | 2020-01-01 | 2020-01-15 |

## FALTA
|Nombre de columna | id_empleado |tipo| fecha | descripcion | impacto_productividad|
|------------------|-------------|----|-------|-------------|----------------------|
|Tipo de llave|PK, FK|PK |PK|| |
| Nula / Unica | Not Null | Not Null| Not Null| Not Null| Not Null|
| Tipo de dato | SERIAL | ENUM | DATE | VARCHAR(1000) | NUMERICO(10,2) |
| Restricciones | | falta, tardanza | | | >=0|
| Datos de ejemplo | 1 | falta | 2020-01-01 | No se presento a trabajar | 0.40 |

## OBJETIVO
|Nombre de columna |id| id_empleado | descripcion | porcentaje_avance | impacto_productividad |
|------------------|-------------|-------------|-------------------|----------------------|---|
|Tipo de llave|PK|FK | | |
| Nula / Unica | Not Null | Not Null| Not Null| Not Null| Not Null|
| Tipo de dato | SERIAL | SERIAL | VARCHAR(1000) | NUMERICO(10,2) | NUMERICO(10,2) |
| Restricciones | | | | >=0| >=0|
| Datos de ejemplo | 1 | 1 | Vender 1000 cajas de carton | 0.00 | 0.00 |

## MOVIMIENTO
|Nombre de columna |id_movimiento| canidad_conceptos | id_lugar | fecha | hora |
|------------------|-------------|-----------------|----------|-------|------|
|Tipo de llave|PK| |FK|||
| Nula / Unica | Not Null | Not Null| Not Null| Not Null| Not Null|
| Tipo de dato | SERIAL | ENTERO | SERIAL | DATE | TIME |
| Restricciones | | >=0| | | |
| Datos de ejemplo | 1 | 1 | 1 | 2020-01-01 | 12:00:00 |

## TRASLADO
|Nombre de columna |id_movimiento| canidad_conceptos | id_lugar | fecha | hora | id_empleado | destino|
|------------------|-------------|-----------------|----------|-------|------|-------------|--------|
|Tipo de llave|PK| |FK|||FK|FK|
| Nula / Unica | Not Null | Not Null| Not Null| Not Null| Not Null| Not Null| Not Null|
| Tipo de dato | SERIAL | ENTERO | SERIAL | DATE | TIME | SERIAL | SERIAL |
| Restricciones | | >=0| | | |
| Datos de ejemplo | 1 | 1 | 1 | 2020-01-01 | 12:00:00 | 1 | 2 |

## VENTA
|Nombre de columna |id_movimiento| canidad_conceptos | id_lugar | fecha | hora |id_empleado| id_cliente | numero_factura | subtotal | iva | total | metodo_pago |
|------------------|-------------|-----------------|----------|-------|------|------------------|-------------|------------|----------------|----------|-----|-------|
|Tipo de llave|PK| |FK|||FK|FK||||||
| Nula / Unica | Not Null | Not Null| Not Null| Not Null| Not Null| Not Null| Not Null| Not Null | Not Null| Not Null| Not Null| Not Null| Not Null| Not Null|
| Tipo de dato | SERIAL | ENTERO | SERIAL | DATE | TIME | SERIAL | SERIAL | ENTERO | NUMERICO(10,2) | NUMERICO(10,2) | NUMERICO(10,2) | ENUM |
| Restricciones | | >=0| | | | | | | >=0| >=0| >=0| tarjeta, efectivo, transferencia |
| Datos de ejemplo | 1 | 1 | 1 | 2020-01-01 | 12:00:00 | 1 | 1 | 1 | 1000.00 | 160.00 | 1160.00 | tarjeta |

## REABASTECIMIENTO
|Nombre de columna |id_movimiento| canidad_conceptos | id_lugar | fecha | hora |id_provedor|total_compra|fecha|
|------------------|-------------|-----------------|----------|-------|------|------------------|-------------|------------|
|Tipo de llave|PK| |FK|||FK||||
| Nula / Unica | Not Null | Not Null| Not Null| Not Null| Not Null| Not Null| Not Null| Not Null|
| Tipo de dato | SERIAL | ENTERO | SERIAL | DATE | TIME | SERIAL | NUMERICO(10,2) | DATE |
| Restricciones | | >=0| | | | | >=0| | |
| Datos de ejemplo | 1 | 1 | 1 | 2020-01-01 | 12:00:00 | 1 | 1000.00 | 2020-01-01 |

## PERDIDA
|Nombre de columna |id_movimiento| canidad_conceptos | id_lugar | fecha | hora | motivo_perdida| total_perdido|
|------------------|-------------|-----------------|----------|-------|------|------------------|-------------|
|Tipo de llave|PK| |FK|||||
| Nula / Unica | Not Null | Not Null| Not Null| Not Null| Not Null| Not Null| Not Null|
| Tipo de dato | SERIAL | ENTERO | SERIAL | DATE | TIME | ENUM | NUMERICO(10,2) |
| Restricciones | | >=0| | | | robo, caducado| >=0|
| Datos de ejemplo | 1 | 1 | 1 | 2020-01-01 | 12:00:00 | robo | 1000.00 |

## GASTOS_LUGAR
|Nombre de la columna | tipo| monto| fecha | id_lugar | descripcion|
|------------------|-------------|-----------------|----------|-------|------|
|Tipo de llave|PK||PK|FK||
| Nula / Unica | Not Null | Not Null| Not Null| Not Null| Not Null|
| Tipo de dato | ENUM | NUMERICO(10,2) | DATE | SERIAL | VARCHAR(1000) |
| Restricciones |fijo, variable | >=0| | | |
| Datos de ejemplo | luz | 1000.00 | 2020-01-01 | 1 | Pago de luz |

## DEPARTAMENTO
|Nombre de la columna | id_departamento | id_lugar|nombre|gerente|
|------------------|-------------|-----------------|--|------|
|Tipo de llave|PK|FK| |FK |
| Nula / Unica | Not Null | Not Null| Not Null| Not Null|
| Tipo de dato | SERIAL | SERIAL | VARCHAR(1000) |SERIAL|

## PAIS
|Nombre de la columna | id_pais | nombre|
|------------------|-------------|-----------------|
|Tipo de llave|PK| |
| Nula / Unica | Not Null | Not Null|
| Tipo de dato | VARCHAR(2) | VARCHAR(1000) |
| Restricciones | | |
| Datos de ejemplo | MX | Mexico |

## ENTIDAD_FEDERATIVA
|Nombre de la columna | id_entidad | id_pais|nombre|
|------------------|-------------|-----------------|--|
|Tipo de llave|PK|FK| |
| Nula / Unica | Not Null | Not Null| Not Null|
| Tipo de dato | VARCHAR(3) | VARCHAR(2) | VARCHAR(1000) |
| Restricciones | | | |
| Datos de ejemplo | MEX | MX | Estado de Mexico |

## CIUDAD
|Nombre de la columna | id_ciudad | id_entidad|nombre|
|------------------|-------------|-----------------|--|
|Tipo de llave|PK|FK| |
| Nula / Unica | Not Null | Not Null| Not Null|
| Tipo de dato | VARCHAR(5) | VARCHAR(3) | VARCHAR(1000) |
| Restricciones | | | |
| Datos de ejemplo | MEX | MEX | Toluca |

## CONCEPTO
|Nombre de la columna | cantidad | id_articulo | id_movimiento| precio_unitario| monto|tipo|
|------------------|-------------|-----------------|--|--|-|-|
|Tipo de llave||FK PK|FK PK| | | |
| Nula / Unica | Not Null | Not Null| Not Null| Not Null| Not Null| Not Null|
| Tipo de dato | ENTERO | SERIAL | SERIAL | NUMERICO(10,2) | NUMERICO(10,2) | ENUM |
| Restricciones | | | | | | venta, reabastecimiento, perdida |
| Datos de ejemplo | 1 | 1 | 1 | 1000.00 | 1000.00 | venta |

## INVENTARIO
|Nombre de la columna | id_articulo | id_lugar|cantidad|
|------------------|-------------|-----------------|--|
|Tipo de llave|PK FK|PK FK| |
| Nula / Unica | Not Null | Not Null| Not Null|
| Tipo de dato | SERIAL | SERIAL | ENTERO |
| Restricciones | | | |
| Datos de ejemplo | 1 | 1 | 1 |

---

## Modelo Fisico Codigo SQL
``` sql
### Tabla país

CREATE TABLE pais(
	id_pais VARCHAR(2) PRIMARY KEY,
	nombre 	VARCHAR(1000) NOT NULL 
);

### Tabla entidad_federativa

CREATE TABLE entidad_federativa(
	id_entidad	VARCHAR(3) PRIMARY KEY,
	id_pais		  VARCHAR(2) CONSTRAINT entidad_id_pais_fk REFERENCES pais(id_pais) NOT NULL,
	nombre		  VARCHAR(1000) NOT NULL
);

### Tabla ciudad

CREATE TABLE ciudad(
	id_ciudad	VARCHAR(5) PRIMARY KEY,
	id_entidad	VARCHAR(3) CONSTRAINT ciudad_id_entidad_fk REFERENCES entidad_federativa(id_entidad) NOT NULL,
	nombre		VARCHAR(1000) NOT NULL 
	
);

### Tabla sujeto

CREATE TABLE sujeto(
	id 		    SERIAL PRIMARY KEY,
	nombre		VARCHAR(100) NOT NULL,
	telefono	INT NOT NULL,	
	correo		VARCHAR(256) check (correo LIKE '%_@__%.__%')NOT NULL,
	codigo_postal	INT NOT NULL,
	id_ciudad	VARCHAR CONSTRAINT sujeto_id_ciudad_fk REFERENCES ciudad(id_ciudad) NOT NULL,
	calle		  VARCHAR(100) NOT NULL,
	numero_interno	INT,
	numero_externo	INT,
);

### Tabla provedor

CREATE TYPE tipo_regimen
AS ENUM ('601', '602', '603', '604', '605', '606', '607', '608', '609', '610', '611', '612', '613', '614', '615',
	'616', '617', '618', '619', '620', '621', '622', '623', '624', '625', '626');


CREATE TABLE provedor(
	id 		  SERIAL PRIMARY KEY,
	rfc			VARCHAR(13) NOT NULL,
	regimen_fiscal		TIPO_REGIMEN NOT NULL,
	pagina_web		    VARCHAR(256),
	FOREIGN KEY (id) REFERENCES sujeto(id))
	INHERITS (sujeto);

### Tabla cliente

CREATE TABLE cliente(
	id 		SERIAL PRIMARY KEY,
	rfc	  VARCHAR(13) NOT NULL,
	regimen_fiscal	TIPO_REGIMEN NOT NULL,
	FOREIGN KEY (id) REFERENCES sujeto(id))
	INHERITS (sujeto);

### Tabla lugar

CREATE TYPE tipo_lugar AS 
ENUM('sucursal','almacen','oficina');

CREATE TABLE lugar(
	id 		SERIAL PRIMARY KEY,
	tipo	tipo_lugar NOT NULL,
	id_responsable	INTEGER NOT NULL,
	cap_max	INT NOT NULL,
	FOREIGN KEY (id) REFERENCES sujeto(id))
	INHERITS (sujeto);

### Tabla departamento

CREATE TABLE departamento(
  id_departamento SERIAL,
  id_lugar INTEGER CONSTRAINT departamento_id_lugar_fk REFERENCES lugar(id) NOT NULL,
  nombre VARCHAR(1000),
  id_gerente INTEGER NOT NULL,
  PRIMARY KEY(id_departamento, id_lugar)
);

### Tabla contrato

CREATE TABLE contrato(
	id_empleado		INTEGER NOT NULL,
	fecha_inicio		DATE NOT NULL,
	fecha_termino		DATE NOT NULL,
	puesto			VARCHAR (50),
	salario			NUMERIC (10,2) check ( salario >= 0) NOT NULL,
	dias_vacaciones	INT     check (dias_vacaciones >= 0),
	PRIMARY KEY(id_empleado, fecha_inicio)
);

### Tabla empleado

CREATE TABLE empleado(
  id  SERIAL PRIMARY KEY,
  nss INT NOT NULL,
  rfc VARCHAR(13) NOT NULL,
  fecha_de_nacimiento DATE NOT NULL,
  fecha_de_ingreso DATE NOT NULL,
  contrato_activo_id_empleado INTEGER NOT NULL, 
  contrato_activo_fecha DATE NOT NULL,
  id_lugar INTEGER CONSTRAINT empleado_id_lugar_fk REFERENCES lugar(id),
  id_departamento_id INTEGER,
  id_departamento_lugar INTEGER,
  indice_productividad NUMERIC(10,2) check (indice_productividad BETWEEN 0 AND 1) NOT NULL,
  FOREIGN KEY (id) REFERENCES sujeto(id),
  FOREIGN KEY (id_departamento_id, id_departamento_lugar) REFERENCES departamento(id_departamento, id_lugar),
  FOREIGN KEY (contrato_activo_id_empleado, contrato_activo_fecha) REFERENCES contrato(id_empleado, fecha_inicio))
INHERITS (sujeto);

### Llaves foraneas

alter table lugar add constraint lugar_responsable_fk foreign key (id_responsable) REFERENCES empleado(id);
alter table departamento add constraint departamento_gerente_fk foreign key (id_gerente) REFERENCES empleado(id);
alter table contrato add constraint contrato_id_empleado_fk foreign key (id_empleado) REFERENCES empleado(id);

### Tabla gasto_empleado

CREATE TABLE gastos_empleado(
  id_empleado INTEGER CONSTRAINT lugar_ REFERENCES empleado(id) NOT NULL,
  tipo tipo_gasto_empleado NOT NULL,
  total NUMERIC (10,2) CHECK (total >= 0 )NOT NULL,
  fecha DATE NOT NULL,
  PRIMARY KEY(id_empleado, tipo, fecha)
);

### Tabla registro_vacaciones

CREATE TABLE registro_vacaciones(
  id_empleado INTEGER CONSTRAINT registro_vacaciones_id_empleado_fk REFERENCES empleado(id) NOT NULL,
  fecha_inicio DATE NOT NULL,
  fecha_fin DATE NOT NULL,
  PRIMARY KEY(id_empleado, fecha_inicio)
);

### Tabla gasto_lugar

CREATE TYPE tipo_gasto_lugar AS 
ENUM('fijo','variable');

CREATE TABLE gastos_lugar(
  id_lugar INTEGER CONSTRAINT gastos_lugar_id_fk REFERENCES lugar(id) NOT NULL,
  descripcion VARCHAR(1000) NOT NULL,
  monto NUMERIC(10,2) check(monto >= 0)NOT NULL,
  tipo tipo_gasto_lugar NOT NULL,
  fecha DATE NOT NULL,
  PRIMARY KEY (tipo, fecha)
);

### Tabla falta

CREATE TYPE tipo_falta AS 
ENUM('falta','retardo');

CREATE TABLE falta(
  id_empleado INTEGER CONSTRAINT falta_id_empleado_fk REFERENCES empleado(id) NOT NULL,
  tipo tipo_falta NOT NULL,
  fecha DATE NOT NULL,
  descripcion VARCHAR(1000) NOT NULL,
  impacto_prodcuitividad NUMERIC(10,2) check(impacto_prodcuitividad >= 0) NOT NULL,
  PRIMARY KEY (id_empleado, tipo, fecha) 
);

### Tabla objetivo

CREATE TABLE objetivo(
  id   SERIAL PRIMARY KEY,
  id_empleado                INTEGER CONSTRAINT objetivo_id_empleado_fk REFERENCES empleado(id) NOT NULL,
  descripcion                VARCHAR(1000) NOT NULL,
  porcentaje_avance          NUMERIC(10,2) CHECK (porcentaje_avance >= 0) NOT NULL,
  impacto_productividad      NUMERIC(10,2) CHECK (porcentaje_avance >= 0) NOT NULL
);

### Tabla cat_unidad

CREATE TABLE cat_unidad(
	clave	        VARCHAR(30) PRIMARY KEY,
	descripción     VARCHAR(1000) NOT NULL
);

### Tabla cat_prod_ser

CREATE TABLE cat_prod_ser(
	clave	        INT PRIMARY KEY,
	descripción     VARCHAR(1000) NOT NULL
);

### Tabla articulo

CREATE TYPE impuesto AS 
ENUM('00','01','02','03','04');

CREATE TABLE articulo(
  id_articulo INT PRIMARY KEY,
  nombre VARCHAR(50) NOT NULL,
  descripcion INT CONSTRAINT articulo_descripcion_prod_ser_fk REFERENCES cat_prod_ser(clave) NOT NULL,
  unidad VARCHAR(50) CONSTRAINT articulo_unidad_clave_fk REFERENCES cat_unidad(clave) NOT NULL,
  categoria INT CONSTRAINT articula_categoria_clave_fk REFERENCES cat_prod_ser(clave) NOT NULL,
  obj_imp impuesto NOT NULL,
  caracteristicas JSON NOT NULL,
  precio_base NUMERIC(10,2) NOT NULL,
  porcentaje_iva NUMERIC(10,2) check(porcentaje_iva >= 0) NOT NULL,
  porcentaje_ieps NUMERIC(10,2) check(porcentaje_ieps >= 0) NOT NULL,
  porcentaje_ganancia NUMERIC(10,2) check(porcentaje_ganancia BETWEEN 0 AND 1)  NOT NULL
);

### Tabla inventario

CREATE TABLE inventario(
  cantidad INT NOT NULL,
  id_lugar INTEGER CONSTRAINT inventario_lugar_id_fk REFERENCES lugar(id) NOT NULL,
  id_articulo INTEGER CONSTRAINT inventario_id_articulo_fk REFERENCES articulo(id_articulo) NOT NULL,
  PRIMARY KEY(id_lugar, id_articulo)
);

### Tabla movimiento

CREATE TABLE movimiento(
  id_movimiento          SERIAL PRIMARY KEY,
  cantidad_conceptos     INT CHECK (cantidad_conceptos >= 0) NOT NULL,
  id_lugar               INTEGER CONSTRAINT movimiento_id_lugar_fk REFERENCES lugar(id) NOT NULL,
  fecha               DATE NOT NULL,
  hora               TIME NOT NULL
);

### Tabla traslado

CREATE TABLE traslado(
  id_movimiento          SERIAL PRIMARY KEY,
  id_empleado    INTEGER CONSTRAINT traslado_id_empleado_fk REFERENCES empleado(id) NOT NULL,
  destino        INTEGER CONSTRAINT destino_destino_fk REFERENCES lugar(id) NOT NULL,
  FOREIGN KEY (id_movimiento) REFERENCES movimiento(id_movimiento))
  INHERITS (movimiento);
  
### Tabla perdidas

CREATE TYPE tipo_perdida AS 
ENUM('robo','caducado');

CREATE TABLE perdida(
	id_movimiento          SERIAL PRIMARY KEY,
	movimiento_perdida    tipo_perdida NOT NULL,
	total_perdida	      NUMERIC(10,2) CHECK (total_perdida >= 0) NOT NULL,
	FOREIGN KEY (id_movimiento) REFERENCES movimiento(id_movimiento))
	INHERITS (movimiento);
  
### Tabla reabastecimiento 

CREATE TABLE reabastecimiento(
  id_movimiento          SERIAL PRIMARY KEY,
  id_provedor       INTEGER CONSTRAINT reabastecimiento_id_provedor_fk REFERENCES provedor(id) NOT NULL,
  total_compra      NUMERIC(10,2) CHECK (total_compra >= 0) NOT NULL ,
  fecha          DATE NOT NULL,
  FOREIGN KEY (id_movimiento) REFERENCES movimiento(id_movimiento))
  INHERITS (movimiento);

### Tabla ventas

CREATE TYPE tipo_pago AS 
ENUM('efectivo','targeta','transferencia');

CREATE TABLE venta(
  id_movimiento          SERIAL PRIMARY KEY,
  id_empleado        INTEGER CONSTRAINT venta_id_empleador_fk REFERENCES empleado(id) NOT NULL,
  id_cliente         INTEGER CONSTRAINT venta_id_cliente_fk REFERENCES cliente(id) NOT NULL,
  numero_factura     INT NOT NULL,
  subtotal           NUMERIC(10,2) CHECK (subtotal >= 0) NOT NULL,
  iva                NUMERIC(10,2) CHECK (iva >= 0) NOT NULL,
  total              NUMERIC(10,2) CHECK (total >= 0) NOT NULL,
  metodo_pago        tipo_pago NOT NULL,
  FOREIGN KEY (id_movimiento) REFERENCES movimiento(id_movimiento))
  INHERITS (movimiento);
  
### Tabla concepto

CREATE TYPE tipo_movimiento AS 
ENUM('Venta','Translado','Reabastecimiento','Perdida');

CREATE TABLE concepto(
  cantidad INT NOT NULL,
  id_articulo INT CONSTRAINT concepto_id_articulo_fk REFERENCES articulo(id_articulo),
  id_movimiento INT CONSTRAINT concepto_id_movimiento_fk REFERENCES movimiento(id_movimiento),
  precio_unitario NUMERIC(8,2) NOT NULL,
  tipo tipo_movimiento,
  PRIMARY KEY (id_articulo, id_movimiento)
);

```
  
