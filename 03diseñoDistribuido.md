# Base de datos Distribuidos

## 1. Crear dos instancias de su base de datos en su sistema operativo físico (NO USARVIRTUALIZACION) para simular la base de datos distribuida.
## 2. La   base   debe   estar   distribuida   en   2   sitios   diferentes   (simulado   en   una   mismacomputadora de preferencia).2. Puede ser una instancia en una versión de PostgreSQL 14 y otra en 15.
## 3. Conectar las 2 instancias en un clúster de postgres (explicar cuales son los pasos parahacerlo y documentarlo mínimo).
## 4.Criterios de distribución de la base de datos.

Con respecto a la fragmentación, se decidió realizarla en dos tablas: venta y artículo;
ya que son dos tablas que cuentan con los atributos adecuados para una fragmentación correcta 
y funcional. 

Para la tabla artículo se realizará una fragmentación horizontal ya que nos serviría 
de mejor forma ordenar los artículos y ver todas sus características, y así tener una mejor organización. 

Mientras que por otro lado, la tabla venta se realizará una fragmentación horizontal 
ya que al tener atributos prácticamente enteros y flotantes, sería la decisión más óptima 
de hacer su fragmentación de esa forma. 

Y de esta forma nos ayuda a mejorar el rendimiento, la escalabilidad, la redundancia y la privacidad de los datos.

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
    
    
  
## 5. Tipos, estrategias y modos de respaldos que se realizaran. 


El uso de pg_dump es importante en el resplado de una base de datos, por lo que tener este en una nube como lo es dirve, es una idea factible, debido a que se encontraria facilmente en el internet en cualquier momento, y es posible su uso desde cualquier ordenador con solo tener el permiso de poder usarlo

### Uso de protocolo 2PC

Es un sistema critico que no puede estar fuera de linea. Y que estrategias, procedimientos yguiás para recuperar información en caso de ser necesario

El uso de dos base de datos es indispenable para evitar tiempos muertosa (fuera de linea en el sistema), por lo que en casod e que una base de datos caiga, la otra base de datos debera entrar como un  auxiliar para de esta forma poder estar tabajando en el arreglo de la base de datos descompuesta sin que haya tiempo muerto

Cabe recalcar que la base de datos secundaria debe estar actualizada en tiempo real por asi decirlo con la princiapl, en pocas palabras debe estar empar3ejada.

El uso del protocolo 2PC, este protocolo asegura el commitment atomico entre las transacciones atomicas, poor lo que extiende los cambios de las transacciones distribuidas siempre y cuando ambas partes o las partes involucradas estene deacuerdo ejn confirmar la transaccion antes de los efectos permantentes.

De esta forma se estaria asegurando que ambas base de datos esten actualizadas y emprejadas para un posible error

