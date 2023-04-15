# Base de datos Distribuidos

## 4.Criterios de distribución de la base de datos.

El uso de la estrategia Top-Down design Process en el diseño de la base de dato distribuida,  va de un esquema global a uno especifico, para este caso se pueden ver 3 casos

###  1 caso Articulos
  
  El articulo se encuentra en un inventario 
    El inventario tiene un lugar 
     El lugar tiene gastos
 El articulo tiene un concepto  
  
###  2 caso Pais
  
  un pais tiene varias entidades federativas
    una entidad federativa tiene varias ciudades
      una ciudad tiene varios sujetos
        un sujeto puede ser un porvedor
        un sujeto puede ser un empleado
          el empleado supervisa un traslado
          el empleado es responsable de un lugar
            el lugar tiene gastos
          El empleado efectua una venta
            la venta es solicitada por un cliente
        un sujeto puede ser un cliente  
        un sujeto puede tiene un lugar 
  
###  3 caso Moviminentos
  
  Un movimiento debe tener varios conceptos
  Un movimiento puede tener una perdida
  un movimieto puede tener una venta
    La venta es solicitada por un cliente
  Un movimiento puede teenr un traslado
    un transalado llega a un lugar
      El lugar tiene gastos
  Un movimeito puede tener un reabastecimiento
    El reabastecimiento es hecho por un provedor
    

Teniendo en cuenta que una base de datos se encuentre en Zinacantepec y otra en Lerma, sera indispensable hacer unas particiones o fragmentaciones en algunas entidades para poder analizar la informacion por esas zonas.
  
Se decidió realizarla en dos tablas: venta y inventario; ya que son dos tablas que cuentan con el atributo lugar que es adecuado para una fragmentación correcta y funcional, En ambos caso se realizara la fragmentacion horizontal

La fragmentacion para la tabla inventario nos serviría para poder administrar lo relacionado con esta entidad y el lugar donde sucede

Mientras que por otro lado, la fragmentacion en la tabla venta se nos ayudara para administar lo relacionado a ella como lo son las ventas totales, metodos de pagos en los lugares.

De esta forma se logra mejorar el rendimiento, la escalabilidad, la redundancia y la privacidad de los datos.


## 5. Tipos, estrategias y modos de respaldos que se realizaran. 


El uso de pg_dump es importante en el resplado de una base de datos, por lo que tener este en una nube como lo es dirve, es una idea factible, debido a que se encontraria facilmente en el internet en cualquier momento, y es posible su uso desde cualquier ordenador con solo tener el permiso de poder usarlo

pg_dump es indispensable en el respaldo de informacion de una base de datos en cualquier caso, debido a que puede actuar como copia de base de datos, lo que podria permitir el traspaso de informacion a otra base de datos que actue como punto de salvacion en caso de falla.

### Uso de protocolo 2PC

Es un sistema critico que no puede estar fuera de linea. Y que estrategias, procedimientos yguiás para recuperar información en caso de ser necesario

El uso de dos base de datos es indispenable para evitar tiempos muertosa (fuera de linea en el sistema), por lo que en casod e que una base de datos caiga, la otra base de datos debera entrar como un  auxiliar para de esta forma poder estar tabajando en el arreglo de la base de datos descompuesta sin que haya tiempo muerto

Cabe recalcar que la base de datos secundaria debe estar actualizada en tiempo real por asi decirlo con la princiapl, en pocas palabras debe estar empar3ejada.

El uso del protocolo 2PC, este protocolo asegura el commitment atomico entre las transacciones atomicas, poor lo que extiende los cambios de las transacciones distribuidas siempre y cuando ambas partes o las partes involucradas estene deacuerdo ejn confirmar la transaccion antes de los efectos permantentes.

De esta forma se estaria asegurando que ambas base de datos esten actualizadas y emprejadas para un posible error



