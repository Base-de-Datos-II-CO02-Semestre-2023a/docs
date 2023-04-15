# Analisis de las entidades.

Esta fase del analisis tiene identificar los atributos de las entidades, así como nombrar las relaciones entre ellas, con el fin de obtener el diagrama ER.
Procederemos a analizar cada entidad y sus relaciones.

El analisis de entidad debe seguir el siguiente formato
## Nombre entidad
Descripcion entidad
### Atributos
---
#### nombre atributo
Descripcion atributo

## SUJETO
Por `SUJETO` se refiere a cualquier entidad que tenga un nombre, un lugar, un telefono, un correo y una dirección. En este caso tenemos a `EMPLEADO`, `CLIENTE`, `LUGAR` y `PROVEEDOR`.
### Atributos
---
#### id
Dato serial con el objetivo de identificar los distintos sujetos.
#### telefono
Número de teléfono del sujeto. Este es un dato numérico de 10 dígitos.
#### correo
Correo electrónico del sujeto. Este es un dato alfanumérico.

Una dirección de correo electrónico válida debe cumplir las siguientes condiciones:

- Contener "@"
- La longitud de la parte local (antes del símbolo "@") debe estar comprendida entre 1 y 64 caracteres.
- La longitud de la parte de dominio (después del símbolo "@") debe estar comprendida entre 4 y 255 caracteres.
- La longitud total debe ser menor o igual a 256 caracteres.
- La parte local y la parte de dominio deben comenzar por una letra o dígito y no deben contener dos símbolos "." consecutivos
- La parte local y la parte de dominio pueden contener letras, números y los caracteres ".", "_" y "-".
- La parte del dominio debe terminar con un símbolo "." y entre dos y cuatro caracteres alfabéticos.

#### nombre
Nombre del sujeto. Este es un dato alfanumérico, el cual puede contener espacios, acentos y caracteres especiales, su longitud máxima es de 100 caracteres.
#### codigo postal
Código postal del sujeto. Este es un dato numérico de 5 dígitos.
#### ciudad
Ciudad del sujeto. Hace referencia a la tabla `CIUDAD`.
#### calle
Calle del sujeto. Es una cadena de texto de 100 caracteres acorde.
#### numero_interno
Número interno del sujeto. Es un dato numérico.
#### numero_externo
Número externo del sujeto. Es un dato numérico.


## LUGAR 
Por `LUGAR` se refiere a la sucursal y/o almacen (si se da el caso) en que se encuentran almacenados productos.
Por lugares hacemos referencia a las sucursales, almacenes y/u oficinas que posee la empresa, los dos primeros poseeran una capacidad máxima, en los dos primeros casos de productos y en el ultimo de personal.

Hereda de `SUJETO`.
### Atributos
---
##### tipo
Tipo de lugar, puede ser `sucursal`, `almacen` u `oficina`.
##### id_responsable
Responsable del lugar, es una llave foránea que hace referencia a la tabla `EMPLEADO`.
##### cap_max
Capacidad máxima del lugar, es un dato numérico.

## EMPLEADO
Por `EMPLEADO` se refiere a los trabajadores de la empresa, cada empleado puede pertenecer o a un departamento o a un lugar, pero no a ambos, puesto que pertenecer a un departamento implicaría que pertenece al lugar dónde se encuentra dicho departamento.

Hereda de `SUJETO`.

### Atributos
---
##### nss
Número de seguridad social del empleado. Este es un dato numérico de 11 dígitos.

##### rfc
Registro federal de contribuyentes del empleado. Este es un dato alfanumérico de 13 caracteres.

##### fecha_nacimiento
Fecha de nacimiento del empleado. Este es un dato de tipo `DATE`.

##### fecha_ingreso
Fecha de ingreso del empleado. Este es un dato de tipo `DATE`.

##### contrato_activo
Contrato activo del empleado. Hace referencia al ultimo contrato que se le ha hecho al empleado, es una llave foránea que hace referencia a la tabla `CONTRATO`.

##### id_departamento
Departamento al que pertenece el empleado. Hace referencia al departamento al que pertenece el empleado, es una llave foránea que hace referencia a la tabla `DEPARTAMENTO` y es opcional.

##### id_lugar
Lugar al que pertenece el empleado. Hace referencia al lugar al que pertenece el empleado, es una llave foránea que hace referencia a la tabla `LUGAR` y es opcional.


##### indice_productividad
Indice de productividad del empleado. Este es un dato se encuentra entre el 0 y el 1.


## CLIENTE
Por `CLIENTE` se refiere a los clientes que realizan la compra de los productos de la empresa.

### Atributos
---
#### rfc
Registro federal de contribuyentes del cliente. Este es un dato alfanumérico de 13 caracteres.
#### regimen_fiscal
Regimen fiscal del cliente. Este es un dato alfanumérico de 3 caracteres acorde al SAT.
Los posibles valores son:
			
| c_RegimenFiscal | Descripción | Física | Moral |
| --- | --- | --- | --- |
| 601 | General de Ley Personas Morales | No | Sí |
| 603 | Personas Morales con Fines no Lucrativos | No | Sí |
| 605 | Sueldos y Salarios e Ingresos Asimilados a Salarios | Sí | No |
| 606 | Arrendamiento | Sí | No |
| 607 | Régimen de Enajenación o Adquisición de Bienes | Sí | No |
| 608 | Demás ingresos | Sí | No |
| 610 | Residentes en el Extranjero sin Establecimiento Permanente en México | Sí | Sí |
| 611 | Ingresos por Dividendos (socios y accionistas) | Sí | No |
| 612 | Personas Físicas con Actividades Empresariales y Profesionales | Sí | No |
| 614 | Ingresos por intereses | Sí | No |
| 615 | Régimen de los ingresos por obtención de premios | Sí | No |
| 616 | Sin obligaciones fiscales | Sí | No |
| 620 | Sociedades Cooperativas de Producción que optan por diferir sus ingresos | No | Sí |
| 621 | Incorporación Fiscal | Sí | No |
| 622 | Actividades Agrícolas, Ganaderas, Silvícolas y Pesqueras | No | Sí |
| 623 | Opcional para Grupos de Sociedades | No | Sí |
| 624 | Coordinados | No | Sí |
| 625 | Régimen de las Actividades Empresariales con ingresos a través de Plataformas Tecnológicas | Sí | No |
| 626 | Régimen Simplificado de Confianza | Sí | Sí |





## PROVEEDOR
Por `PROVEEDOR` se refiere a los proveedores de la empresa.
### Atributos
---
#### rfc
Registro federal de contribuyentes del proveedor. Este es un dato alfanumérico de 13 caracteres.
#### regimen_fiscal
Regimen fiscal del proveedor. Este es un dato alfanumérico de 3 caracteres acorde al SAT.
Los posibles valores son:
| c_RegimenFiscal | Descripción | Física | Moral |
| --- | --- | --- | --- |
| 601 | General de Ley Personas Morales | No | Sí |
| 603 | Personas Morales con Fines no Lucrativos | No | Sí |
| 605 | Sueldos y Salarios e Ingresos Asimilados a Salarios | Sí | No |
| 606 | Arrendamiento | Sí | No |
| 607 | Régimen de Enajenación o Adquisición de Bienes | Sí | No |
| 608 | Demás ingresos | Sí | No |
| 610 | Residentes en el Extranjero sin Establecimiento Permanente en México | Sí | Sí |
| 611 | Ingresos por Dividendos (socios y accionistas) | Sí | No |
| 612 | Personas Físicas con Actividades Empresariales y Profesionales | Sí | No |
| 614 | Ingresos por intereses | Sí | No |
| 615 | Régimen de los ingresos por obtención de premios | Sí | No |
| 616 | Sin obligaciones fiscales | Sí | No |
| 620 | Sociedades Cooperativas de Producción que optan por diferir sus ingresos | No | Sí |
| 621 | Incorporación Fiscal | Sí | No |
| 622 | Actividades Agrícolas, Ganaderas, Silvícolas y Pesqueras | No | Sí |
| 623 | Opcional para Grupos de Sociedades | No | Sí |
| 624 | Coordinados | No | Sí |
| 625 | Régimen de las Actividades Empresariales con ingresos a través de Plataformas Tecnológicas | Sí | No |
| 626 | Régimen Simplificado de Confianza | Sí | Sí |

#### pagina_web
Pagina web del proveedor. Este es un dato alfanumérico de 100 caracteres.

## ARTICULO

 Nos interesa identificarlo, conocer su nombre, descripción, precio en que se compra, precio a la venta, categoria a la que pertenece, en qué tiendas/almacenes se encuentra y la cantidad que hay en cada uno, un registro de cuando se reabastece y un registro de cada venta de dicho producto.

 Dado que el  departamento de facturacióntambien usará el sistema, el SAT (Secretaria de Administración Tributaria) requiere dentro de una factura algunos datos del articulo, entre ellos se encuentran
 - Clave de producto o servicio
 - Numero de identificación
 - Clave de unidad
 - Unidad
 - Descripción
 - Valor unitario
 - Si es objeto de impuestos o no

Se procede a analizar atributo por atributo para definir y normalizar cada uno.

### Atributos
---

#### id
Este atributo tiene el fin de identificar a cada articulo, este es el mismo que el Numero de Identificacion requerido por el SAT, hay distintas formas de conformar el identificador, citando lo descrito por la *Secretaria de Administración Tributaria*
> En este campo se puede registrar el número de parte, identificador del producto o del servicio, la clave de producto o servicio, SKU (número de referencia) o equivalente, propia de la operación del contribuyente emisor del comprobante fiscal descrito en el presente concepto.
>- Opcionalmente se pueden utilizar claves del estándar GTIN (número global de artículo comercial).
>- Puede conformarse desde uno hasta 100 caracteres alfanuméricos.
> Ejemplo: NoIdentificacion= UT421510<sup>4</sup>

Considerando que estamos empleando la gestion del inventario mediante codigo de barras, y estas se obtienen utilzando el GTIN, este sera nuestro identificador, el cual varia de 8 a 14 digitos númericos.

#### nombre
Este atributo tiene cómo finalidad que el usuario final sepa a que articulo se está haciendo referencia, este será un dato de tipo alfanumerico de longitud de 70 caracteres.

#### descripción
Este atributo permite al usuario identificar la naturaleza del articulo, para fines de este proyecto tomaremos que es la descripcion mostrada por el SAT en su catalogo de productos y servicios, para lo que simplemente se hace referencia a la clave de producto o servicio, para una optima implementacion, se creará la entidad `CAT_PROD_SER`, la cual será poblada con la informacion proporcionada por el SAT.

La entidad `CAT_PROD_SER` se analizará más.

#### precio_base
Este atributo es una pieza clave en nuestra base de datos, este lo podemos considerar en dos partes, el precio a la compra, y el precio a la venta, dado que el precio a la compra no es propio del articulo, más bien, es propio del movimiento de reabastecimiento, este se ignorará de momento en esta entidad, mientras que el precio a la venta sí lo es, este sera referenciado solamente cómo precio_base, el cual es el valor unitario solicitado por el SAT, a este precio se le agregarán lo correspondiente a el iva, ieps y ganancias para obtener el precio final a la venta.

#### categoria
Este atributo tiene un fin similar a la descripcion, con la unica diferencia de que su uso es agrupar a este producto con otros similares, para esto igualmente utilizaremos los datos proporcionados en el catalogo de productos y servicios, a diferencia que esta vez, el interes es unicamente la clave de la clase.

#### unidad
Este atributo es el que se utiliza para identificar la unidad de medida del articulo, para esto se hace referencia a la clave de unidad, la cual es proporcionada por el SAT, para una optima implementacion, se creará la entidad `CAT_UNIDAD`, la cual será poblada con la informacion proporcionada por el SAT.

#### obj_imp
Se utiliza simplemente para identificar si el articulo es objeto de impuesto o no, utilizado posteriormente en el analizis y calculo de impuestos, los posibles valores son:
|obj_imp|Definicion|
|--|--|
|01|No objeto de impuesto|
|02|Sí objeto de impuesto|
|03|Si objeto de impuesto y no obligado al desglose|
|04|Sí objeto del impuesto y no causa impuesto|

#### caracteristicas
Con el fin de analizar el comportamiento de los usuarios, y hacer un analizis más completo de las ventas, estos se guardaran en objetos javascript.


El resto de datos no son propios de un articulo, pues recaen en otras entidades, cómo lo es el precio de reabastecimiento, la cantidad que hay del articulo, o el lugar en el que se almacena, entre otros.

#### porcentaje_iva
Este atributo es el que se utiliza para identificar el porcentaje de iva que se le aplica a este articulo, este es un dato de tipo numerico, con dos decimales, y un rango de 0 a 1.
#### porcentaje_ieps
Este atributo es el que se utiliza para identificar el porcentaje de ieps que se le aplica a este articulo, este es un dato de tipo numerico, con dos decimales, y un rango de 0 a 1.
#### porcentaje_ganancia
Este atributo es el que se utiliza para identificar el porcentaje de ganancia que se le aplica a este articulo, este es un dato de tipo numerico, con dos decimales, y un rango de 0 a 1.

## CAT_PROD_SER
Esta entidad es la encargada de almacenar la informacion proporcionada por el SAT, en su catalogo de productos y servicios, esta entidad es de solo lectura, y no se podra modificar, solo se podra agregar nuevos datos, para esto se creara un script que se encargara de poblar esta entidad con la informacion proporcionada por el SAT.

### Atributos
---
#### clave
Este atributo es de tipo numerico, y es el identificador unico de cada producto o servicio, este es el mismo que el Clave de producto o servicio requerido por el SAT, este es un dato de tipo numerico, con 8 digitos.

#### descripcion
Este atributo es de tipo alfanumerico, y es la descripcion del producto o servicio, este es el mismo que el Descripción requerido por el SAT, este es un dato de tipo alfanumerico, con 1000 caracteres.

## CAT_UNIDAD
Esta entidad es la encargada de almacenar la informacion proporcionada por el SAT, en su catalogo de unidades, esta entidad es de solo lectura, y no se podra modificar, solo se podra agregar nuevos datos, para esto se creara un script que se encargara de poblar esta entidad con la informacion proporcionada por el SAT.

### Atributos
---
#### clave
Este atributo es de tipo alfanumerico, y es el identificador unico de cada unidad, este es el mismo que el Clave de unidad requerido por el SAT, este es un dato de tipo alfanumerico, con 3 caracteres.

#### descripcion
Este atributo es de tipo alfanumerico, y es la descripcion de la unidad, este es el mismo que el Descripción requerido por el SAT, este es un dato de tipo alfanumerico, con 1000 caracteres.

## GASTOS_EMPLEADO
Esta entidad es la encargada de almacenar la informacion de los gastos que referentes a un empleado, esta entidad es de solo lectura, y no se podra modificar.

### Atributos
---
#### id_empleado
Este atributo es de tipo numerico, y es el identificador unico de cada empleado, este es el mismo que el id_empleado de la entidad EMPLEADO.

#### tipo
Este atributo es de tipo alfanumerico, y es el tipo de gasto, sus valores posibles son:
- Nomina
- Seguro
- Afore
- Prima vacacional

## CONTRATO
Esta entidad es la encargada de almacenar la informacion de los contratos de los empleados.

### Atributos
---
#### id_empleado
Este atributo es de tipo numerico, y es el identificador unico de cada empleado, este es el mismo que el id_empleado de la entidad EMPLEADO.

#### fecha_inicio
Este atributo es de tipo fecha, y es la fecha en la que se inicio el contrato.

#### fecha_fin
Este atributo es de tipo fecha, y es la fecha en la que se finaliza el contrato.

#### puesto
Este atributo es de tipo alfanumerico, y es el puesto que ocupa el empleado.

#### salario
Este atributo es de tipo numerico, y es el salario que se le paga al empleado.

#### dias_vacaciones
Este atributo es de tipo numerico, y es la cantidad de dias de vacaciones que tiene el empleado al año.

## REGISTRO_VACACIONES
Esta entidad es la encargada de almacenar la informacion de los registros de vacaciones de los empleados.

### Atributos
---
#### id_empleado
Este atributo es de tipo numerico, y es el identificador unico de cada empleado, este es el mismo que el id_empleado de la entidad EMPLEADO.

#### fecha_inicio
Este atributo es de tipo fecha, y es la fecha en la que se inicio el registro de vacaciones.

#### fecha_fin
Este atributo es de tipo fecha, y es la fecha en la que se finaliza el registro de vacaciones.


## FALTA
Esta entidad es la encargada de almacenar la informacion de las faltas de los empleados.

### Atributos
---
#### id_empleado
Este atributo es de tipo numerico, y es el identificador unico de cada empleado, este es el mismo que el id_empleado de la entidad EMPLEADO.

#### tipo
Este atributo es de tipo alfanumerico, y es el tipo de falta, sus valores posibles son:
- Inasistencia
- Retardo

#### fecha
Este atributo es de tipo fecha, y es la fecha en la que se registro la falta.

#### descripcion
Este atributo es de tipo alfanumerico, y es la descripcion de la falta.

#### impacto_productividad
Este atributo es de tipo numerico, y es el impacto que tiene la falta en la productividad del empleado, va del 0 al 1.

## OBJETIVO

Esta entidad es la encargada de almacenar la informacion de los objetivos de los empleados.

### Atributos
---
#### id_empleado
Este atributo es de tipo numerico, y es el identificador unico de cada empleado, este es el mismo que el id_empleado de la entidad EMPLEADO.

#### descripcion
Este atributo es de tipo alfanumerico, y es la descripcion del objetivo.

#### porcentaje_avance
Este atributo es de tipo numerico, y es el porcentaje de avance del objetivo, va del 0 al 1.

#### impacto_productividad
Este atributo es de tipo numerico, y es el impacto que tiene el objetivo en la productividad del empleado, va del 0 al 1.

## MOVIMIENTO
El `Movimiento` se refiere a cada entidad donde se requiera saber la cantidad de  articulos, el lugar donde se llevo el movimiento asi como la fecha y hora del movimiento; De esta entidad forman parte como hijas las entidades `TRANSLADO`, `VENTA`, `REBASTECIMIENTO` y `PERDIDA` las cuales son un tipo de movimiento.


### Atributos
---

#### id_movimiento
Cada movimiento debera ser identificado por un id para asi llevar un control de los translados, ventas, rebastecimiento y perdidas

#### cantidad_conceptos
Este atributo hace referencia a la cantidad de conceptos, es decir la cantidad total de articulos que tuvieron un movimiento

#### id_lugar
Cada movimiento sera realizado en un determinado lugar por lo que se necesitara el identificador unico de dicho lugar para tener establecido donde se realizo dicho movimiento

#### fecha
Cada movimiento ademas de ser realizado en un lugar determinado contara con una fecha especifica en la que se realizo, las fechas de estos movimientos empezaran desde la implementacion del sistema en la tienda.

#### hora
Ademas de la fecha tambien se contara con una hora en la cual se realizo el movimiento, esto para llevar un control mas exaustivo y preciso de cada movimiento.


## TRASLADO
El `TRASLADO`  es llevado a cabo cuando por algún motivo es necesario mover uno o más articulos de una tienda a otra, o en su caso, de un almacen a otro, o de una almacen a una tienda, ya sea parcial o totalmente; cada translado estara acargo de un empleado referente al lugar de donde se hizo dicho traslado; , esta operacion no representa ni un ingreso ni un egreso a la empresa.

Hereda de `MOVIMIENTO`

### Atributos
---

#### id_empleado
Este id es requerido para saber que empleado fue el responsable en realizar dicho tranlado

#### destino
Aqui se especifica el lugar destino del translado ya sea una tienda o un almacen.

## VENTA
En la `VENTA` se registrara todo el movimiento relacionado con la venta de los articulos de la tienda, para identificar cada venta sera necesario el id del empleado que realiza dicha venta, el id del cliente al cual va dirigida la venta, el numero de factura que tendra la venta asi como el subtotal, el iva y el total de la venta teniendo como ultimo el metodo de pago con el que se realizo la venta. 

Hereda de `MOVIMIENTO`

### Atributos
---

#### id_empleado
Este es requerido para saber que empleado fue el encargado de que venta, esta informacion se podra usar para saber el  grado de avance de objetivos de venta que tenga cada empleado.

#### id_cliente
Al igual que el id del empleado se requirar un id del cliente para identificar a quien fue realizada la venta.

#### numero_factura
El numero de factura nos ayudara a identificar de mejor manera cada venta realizada.

#### subtotal
El subtotal se refiere al total de la suma de los precios de los articulos que se venderan en dicha venta, esto se sabra a partir de la cantidad de articulos del movimiento y el precio de cada concepto asignado a dicho movimiento.

#### iva
Representa la cantidad de iva que se agregara al subtotal.

#### total
Es el resultado del subtotal mas el iva el cual nos da un total de la venta, lo cual sera lo que se le cobrara al cliente.

#### metodo_pago
Este atributo es utilizado para seleccionar el metodo de pago seleccionado por el cliente con el cual se llevara acabo la venta

## REABASTECEMIENTO
En el `REBASTECIMIENTO` se hara el registro de cada movimiento de rebastecimiento requerido por el lugar, para realizar un reabastecimiento se necesitara del id del provedor, el total de compra de los articulos por el reabastecimiento asi como la fecha en la que se entregara el reabastecimiento y a su vez el lugar donde se hara la entrega de este.

Hereda de `MOVIMIENTO`

### Atributos
---

#### id_provedor
Este es requerido para identificar a que provedor se le pedira el reabasecimiento de acuerdo a las necesidades que tenga el lugar.

#### total_compra
Es la suma total del precio de la cantidad de articulos pedidos para el reabastecimiento del lugar.

#### fecha
Se utilizara para identificar la fecha en la que se ralizara el reabastecimiento.

## PERDIDA
Una la `PERDIDA` se da por dos motivos, que un producto se deba desechar, o, que un producto haya sido robado, esto representa perdidas para la empresa.

### Atributos
---

#### motivo_perdida
Aqui simplemente se especificara entre las dos opciones cual fue el motivo de la perdida.

#### total_perdido
Tras realizar un inventario tras contabilizar las perdidas independientemente del motivo se podra registrar el total perdido dependiendo de la cantidad de articulos que fueron perdidos.

## GASTOS_LUGAR
Los `GASTOS_LUGAR` son los gastos que se realizan en cada lugar, ya sea en una tienda o en un almacen, estos gastos pueden ser de tipo fijo o variable, los gastos fijos son los que se realizan de manera constante, como por ejemplo el pago de la renta, el pago de la luz, el pago del agua, etc. mientras que los gastos variables son los que se realizan de manera ocasional, como por ejemplo el pago de un servicio de limpieza, el pago de un servicio de mantenimiento, etc.

### Atributos
---

#### tipo
Aqui se especificara si el gasto es fijo o variable.

#### monto
Es la cantidad de dinero que se gasto en dicho gasto.

#### fecha
Es la fecha en la que se realizo el gasto.

#### id_lugar
Es el id del lugar en el que se realizo el gasto.

#### descripcion
Es una breve descripcion del gasto realizado.

## DEPARTAMENTO
Los `DEPARTAMENTOS` son los departamentos que se encuentran en un `LUGAR` de tipo oficia.

### Atributos
---
#### id_departamento
Es el id del departamento, es un dato de tipo serial.

#### id_lugar
Es el id del lugar al que pertenece el departamento, hace referencia a la tabla `LUGAR`.

#### nombre
Es el nombre del departamento, es un dato de tipo alfanumerico.

#### id_gerente
Es el id del gerente del departamento, hace referencia a la tabla `EMPLEADO`.

## PAIS
Los `PAISES` son los paises en los que se encuentran algunos sujetos.

### Atributos
---

#### id_pais
Es el id del pais, es un dato de tipo alfanumarico.

#### nombre
Es el nombre del pais, es un dato de tipo alfanumerico.

## CIUDAD
Las `CIUDADES` son las ciudades en las que se encuentran algunos sujetos.

### Atributos
---

#### id_ciudad
Es el id de la ciudad, es un dato de tipo alfanumarico.

#### id_entidad
Es el id de la entidad a la que pertenece la ciudad, hace referencia a la tabla `ENTIDAD_FEDERATIVA`.

#### nombre
Es el nombre de la ciudad, es un dato de tipo alfanumerico.

## ENTIDAD_FEDERATIVA
Las `ENTIDADES_FEDERATIVAS` son las entidades federativas en las que se encuentran algunso sujetos.

### Atributos
---

#### id_entidad
Es el id de la entidad federativa, es un dato de tipo alfanumarico.

#### id_pais
Es el id del pais al que pertenece la entidad federativa, hace referencia a la tabla `PAIS`.

#### nombre
Es el nombre de la entidad federativa, es un dato de tipo alfanumerico.

# Analisis de las relaciones

## Nombre relacion
Descripcion relacionit

## Lugar-Empleado (responsable)
Un lugar puede tener uno y solo responsable y un empleado puede ser responsable de uno o más lugares. Por lo que que la relación es de un empleado a muchos lugares, implementando para esto .
## Empleado-Lugar
Un lugar puede tener muchos empleados y un empleado puede estar en un solo lugar lugares. Por lo que que la relación es de muchos empleados a un lugar.
## Lugar-Departamento
Un lugar puede tener muchos departamentos y un departamento puede estar en un solo lugar. Por lo que que la relación es de muchos departamentos a un lugar.
## Lugar-Gastos Lugar
Un lugar puede tener muchos gastos y un gasto puede estar en un solo lugar. Por lo que que la relación es de muchos gastos a un lugar.

## Lugar-Articulo
Un lugar puede almacenar muchos articulos y un articulo puede estar almacenado en muchos lugares. Por lo que que la relación es de muchos a muchos.

Dado que dicha relacion es ineficiente, se implementa una tabla intermedia `INVENTARIO` que relaciona a `LUGAR` y `ARTICULO` con los siguientes atributos:

### Lugar - Inventario
Un lugar puede tener muchos inventarios y un inventario puede estar en un solo lugar. Por lo que que la relación es de muchos inventarios a un lugar.

### Articulo - Inventario
Un articulo puede estar en muchos inventarios y un inventario puede tener un solo articulo. Por lo que que la relación es de muchos inventarios a un articulo.


## Lugar-Movimiento
Un lugar puede tener muchos movimientos y un movimiento sale de un solo lugar. Por lo que que la relación es de muchos movimientos a un lugar.

## Lugar-Traslado
Un lugar puede tener muchos traslados y un traslado puede llegar en un solo lugar. Por lo que que la relación es de muchos traslados a un lugar.


## Empleado-Contrato (contrato_activo)
Un empleado puede tener muchos contratos y un contrato puede ser de uno y solo un `EMPLEADO`. Por lo que que la relación es de muchos a uno.

## Empleado-Departamento (departamento)
Un empleado puede pertenecer a uno y solo un departamento y un departamento puede tener muchos empleados. Por lo que que la relación es de uno a muchos.

## ARTICULO-MOVIMIENTO
Esta relación es de muchos a muchos, puesto que un articulo puede estar en muchos movimientos y un movimiento puede tener muchos articulos.
Esto es inficiente, por lo que implementamos una tabla intermedia nombrada `CONCEPTO` que relaciona a `ARTICULO` y `MOVIMIENTO`.
Las relaciones entre estas tablas son las siguientes:

### ARTICULO-CONCEPTO
Esta relación es de uno a muchos, puesto que un articulo puede estar en muchos conceptos, pero un concepto solo puede ser de un articulo.

### MOVIMIENTO-CONCEPTO
Esta relación es de uno a muchos, puesto que un movimiento puede tener muchos conceptos, pero un concepto solo puede ser de un movimiento.
## CAT_PROD_SER-ARTICULO
Esta relación es de uno a muchos, puesto que un articulo puede tener una sola descripcion, pero una descripcion puede ser utilizada por muchos articulos.

Esta relacion tambien se da en el atributo categoría, donde funciona de la misma manera.

## CAT_UNIDAD-ARTICULO
Esta relación es de uno a muchos, puesto que un articulo puede tener una sola unidad, pero una unidad puede ser utilizada por muchos articulos.

## REABASTECIMIENTO-PROVEEDOR
Esta relación es de uno a muchos, puesto que un proveedor puede tener muchos reabastecimientos, pero un reabastecimiento solo puede ser de un proveedor.

## VENTA-CLIENTE
Esta relación es de uno a muchos, puesto que un cliente puede estar en muchas ventas, pero una venta solo puede ser de un cliente.

## VENTA-EMPLEADO
Esta relación es de uno a muchos, puesto que un empleado puede estar en muchas ventas, pero una venta solo puede ser efectuada un empleado.
## TRASLADO-EMPLEADO
Esta relación es de uno a muchos, puesto que un empleado puede encargarse en muchos traslados, pero un traslado solo puede ser supervisado por un empleado.
	
## DEPARTAMENTO-EMPLEADO
Esta relación es de uno a muchos, puesto que un empleado puede pertenecer en un solo departamentos, pero un departamento solo puede tener muchos empleados.

## EMPLEADO-DEPARTAMENTO
Esta relación es de uno a muchos, puesto que un empleado puede ser gerente en varios departamentos, pero un departamento solo puede tener un gerente.

## REGISTRO_VACASIONES-EMPLEADO
Esta relación es de uno a muchos, puesto que un empleado puede tener muchos registros de vacaciones, pero un registro solo puede ser de un empleado.

## CONTRATO-EMPLEADO
Esta relación es de uno a muchos, puesto que un empleado puede tener muchos contratos, pero un contrato solo puede ser de un empleado.

## EMPLEADO-OBJETIVO
Esta relación es de uno a muchos, puesto que un empleado puede tener muchos objetivos, pero un objetivo solo puede ser de un empleado.

## EMPLEADO-FALTA
Esta relación es de uno a muchos, puesto que un empleado puede tener muchas faltas, pero una falta solo puede ser de un empleado.

## EMPLEADO-GASTOS_EMPLEADO
Esta relación es de uno a muchos, puesto que un empleado puede generar muchos gastos, pero un gasto solo puede ser de un empleado.

## PAIS-ENTIDAD_FEDERATIVA
Esta relación es de uno a muchos, puesto que un pais puede tener muchas entidades federativas, pero una entidad federativa solo puede ser de un pais.

## ENTIDAD_FEDERATIVA-CIUDAD
Esta relación es de uno a muchos, puesto que una entidad federativa puede tener muchas ciudades, pero una ciudad solo puede ser de una entidad federativa.

## CIUDAD-SUJETO
Esta relación es de uno a muchos, puesto que una ciudad puede tener muchos sujetos, pero un sujeto solo puede ser de una ciudad.

# Analisis de las Entidades intermedias
## CONCEPTO
El `CONCEPTO` hace referencia a los articulos que estan en algun movimiento ya sea `TRANSLADO`, `VENTA`, `REBASTECIMIENTO` o `PERDIDA` teniendo como informacion a que `MOVIMIENTO` pertenecen, se especifica la cantidad de articulos en ese movimiento ademas de contar con el precio_unitario y monto de cada producto, a su vez tambien se especifica el tipo de movimiento en el que se encuentra el articulo.

### Atributos
---

#### cantidad
Especifica la cantidad de articulos del mismo tipo que estaran en un movimiento.

#### id_articulo
Necesario para identificar que articulo es el que esta en el movimiento.

#### id_movimiento
Nos permite identificar que conceptos estan en que movimiento, apartir de aqui se podra hacer la consulta de los preicos unitarios y montos para la realizacion de cualquiera de los movimientos.

#### precio_unitario
Nos especifica el precio por unidad del articulo que este en el movimiento.

#### tipo
Aqui se especifica el tipo de movimiento en el que se encuentra el articulo.

## INVENTARIO
El `INVENTARIO` es una entidad intermedia entre `ARTICULO` y `LUGAR`, el objetivo del inventario es el de llevar un control de los articulos que se encuentran en un determinado lugar ya sea una tienda o un almacen. Lo importante de esta entidad es que alamacenara la cantidad de cada producto que contenga a su vez que se sabra en que lugar esta ubicado dicho inventario. Ademas con ayuda de esta entidad las tiendas o almacenes se guiaran para realizar los "inventarios" y asi contar con un control exaustibo de los productos.

### Atributos
---

#### cantidad
Nos dara información sobre la cantidad de piezas que tiene un articulo en un almacen o en una tienda.

#### id_lugar
El id del lugar permite identificar a donde pertenece dicho inventario.

#### id_articulo
El id del articulo es utilizado para identificar que articulos se encuentran en dicho inventario.


![Diagrama entidad relacion](/images/DiagramaER.svg)
