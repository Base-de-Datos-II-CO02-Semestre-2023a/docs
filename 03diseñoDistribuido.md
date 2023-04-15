----------------------------------------------------------------------------------------------------------------------------------------------------------------
-------------------------------------------                     Base de datos Distribuidas                      ------------------------------------------------
----------------------------------------------------------------------------------------------------------------------------------------------------------------



----------------------------------------------------------------------------------------------------------------------------------------------------------------
1. Crear dos instancias de su base de datos en su sistema operativo físico (NO USARVIRTUALIZACION) para simular la base de datos distribuida.
----------------------------------------------------------------------------------------------------------------------------------------------------------------




----------------------------------------------------------------------------------------------------------------------------------------------------------------2. La   base   debe   estar   distribuida   en   2   sitios   diferentes   (simulado   en   una   mismacomputadora de preferencia).2. Puede ser una instancia en una versión de PostgreSQL 14 y otra en 15.
----------------------------------------------------------------------------------------------------------------------------------------------------------------



----------------------------------------------------------------------------------------------------------------------------------------------------------------
3. Conectar las 2 instancias en un clúster de postgres (explicar cuales son los pasos parahacerlo y documentarlo mínimo).
----------------------------------------------------------------------------------------------------------------------------------------------------------------




----------------------------------------------------------------------------------------------------------------------------------------------------------------
                                      4.Criterios de distribución de la base de datos.
----------------------------------------------------------------------------------------------------------------------------------------------------------------



----------------------------------------------------------------------------------------------------------------------------------------------------------------                                        5. Tipos, estrategias y modos de respaldos que se realizaran. 
----------------------------------------------------------------------------------------------------------------------------------------------------------------

El uso de pg_dump es importante en el resplado de una base de datos, por lo que tener este en una nuber como lo es dirve, es una idea factible, debido a que se encontraria facilmente en el internet en cualquier momento, y es posible su uso desde cualquier ordenador con solo tener el permiso de poder usarlo



Uso de protocolo 2PC




Es un sistema critico que no puede estar fuera de linea. Y que estrategias, procedimientos yguiás para recuperar información en caso de ser necesario


el uso de dos base de datos es indispenable para evitar tiempos muertosa (fuera de linea en el sistema), por lo que en casod e que una base de datos caiga, la otra base de datos debera entrar como un  auxiliar para de esta forma poder estar tabajando en el arreglo de la base de datos descompuesta sin que haya tiempo muerto

Cabe recalcar que la base de datos secundaria debe estar actualizada en tiempo real por asi decirlo con la princiapl, en pocas palabras debe estar empar3ejada.

El uso del protocolo 2PC, este protocolo asegura el commitment atomico entre las transacciones atomicas, poor lo que extiende los cambios de las transacciones distribuidas siempre y cuando ambas partes o las partes involucradas estene deacuerdo ejn confirmar la transaccion antes de los efectos permantentes.

de esta forma se estaria asegurando que ambas base de datos esten actualizadas y emprejadas para un posible error

