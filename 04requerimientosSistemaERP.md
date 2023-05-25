# Requerimientos
> No aceptamos devoluciones porque van a querer regresar el bolillo con el mordisco

> Hoy no fiamos, mañana sí


- iniciar sesion
- control asistencia
- CRUD por area:
  - Finanzas
  - Recursos Humanos
  - Inventario
  - Tienda

# Vistas
## Tienda
Cada que se hace una venta se registra al cliente en caso de que este desee factura, de lo contrario se asigna un cliente generico (Publico en General) a dicha venta
  - Registrar movimiento
  - registrar clientes y o proveedor (a la hora del movimiento)
  - Checar el inventario que hay en la tienda.
  - Buscar si un producto esta en el inventario local, en caso de que no verificar si existe en alguna otro lugar
  - ver si un producto tiene ofertas
  - Ver balance de ingresos, egresos del dia en curso.



## Recursos Humanos
  - registrar empleados
  - ver que empleados estan en que lugares/departamentos
  - dar de baja empleados
  - registrar prestaciones
  - mover empleados de una sucursal a otra
  - Ver informacion detallada del empleado
    - Modificaciones al contrato
    - Objetivos
    - Faltas
    - Registro de vacaciones
    - Vacaciones restantes en el año en curso
    - Sueldo actual
    - fecha de ingreso
  - Recomendaciones que empleado despedir, a que empleado aumentar sueldo, etc.
  - modificar contratos
  - dar de alta faltas, objetivos y actualizar objetivos
## Finanzas
  - Registrar gastos de lugar
  - Vista general de ingresos, egresos,
  - Mostrar informacion detallada de las ventas
    - Ganancias, ieps, iva (todas las ventas en general y por venta) 
    - prediccion de ventas
    - productos mas vendidos
    - productos menos vendidos
    - productos que generan mas y menos gancias
    - listado de ventas
    - Recomendaciones (productos a los que se le puede aumentar el porcentaje de ganancia)
  - Mostrar informacion detallada de gastos (empleado, lugar)
    - Listar los lugares y empleados que más y menos gastos generan
    - Promedio de gastos por empleado, lugar, departamento
    - Recomendaciones (en donde recortar gastos, que empleado despedir)
  - Actualizar precios base, iva, ieps y ganancia
## Inventario
  - Registrar articulos
  - Hacer reabastecimientos, traslados.
  - Eliminar productos del inventario
  - Actualizar cantidad, descuento
  - Mostrar productos en inventario general, y por lugar
  - Espacio disponible en cada lugar

# Tipos de usuario (puesto)
  - Empleado de mostrador (accede a vista de tienda)
  - Empleado de recursos humanos
  - Empleado de finanzas
  - Empleado de almacen (accede a vista de inventario)
  - Admin (accede a todo)

# Triggers
- Caducidad-descuento en inventario
  - Lo hace el backend
  - Cada dia se actualiza el campo descuento en la tabla inventario colocando ".25" en caso de que este campo sea menor, en todas las filas que tengan una caducidad < a una semana

- Concepto-Inventario
  - Cada que se crea un concepto, se verifica el tipo de movimiento.
    - si es de tipo venta o perdida, se disminuira el inventario más proximo a caducarse en la misma cantidad de dicho concepto.

    - si es de tipo reabastecimiento, se insertara una fila en inventario usando el id_articulo de concepto, el id_lugar y la caducidad del reabastecimiento.

    - si es de tipo traslado, se insertara o incrementara la cantidad del concepto en inventario usando el id_articulo y la caducidad de concepto y el destino del traslado, y se disminuira dicha cantidad de inventario donde el id del articulo y el lugar de concepto.

- Tipo de moviento-Movimiento
  - Cada de se crea un insert en una de las tablas hijas de movimiento (Venta, Translado, Perdida, Reabastecimiento), se realiza un insert en la tabla padre Movimiento con los datos correspondientes al registro.

- Registro_Contratos - Empleado
  (este insiso lo hace backend)- Cada que se cree un empleado se crea un contrato, se deberan mandar dos inserts primero el de empleado seguido del de contrato
  - Cuando se actualiza Registro_Contratos se inserta una fila en modificacion_contrato donde el json modificaciones tiene todos los campos que se modificaron en registro_contratos.

- Falta-Empleado
  -Cuando se inserta una falta en Falta, se actualiza el campo indice_productividad de la siguiente manera indice_productividad = indice_productividad - impacto_productividad.

- Objetivo-Empleado
  - Cuando se actualiza la tabla objetivo, si el campo porcentaje_avance es igual a 1, el indice_productividad de empleado se incrementa de la siguiente forma indice_productividad = indice_productividad + impacto_productividad.

# Particion
- Articulo : por unidad
