# Prácticas de consultas SQL realizadas como aprendizaje de este lenguaje
Durante mi tiempo como estudiante de Ingeniería en Sistemas y Computación, adquirí conocimientos en el lenguaje SQL DML al resolver problemas mediante la ejecución de consultas en una base de datos de prueba. A continuación listo los tipos de problemas resueltos como prueba del nivel de conocimiento adquirido.


1. Consultar todos los productos cuyo proveedores estén localizados en Santiago
    ```sql
    SELECT Descripcion_Producto FROM TB_Producto, TB_Proveedor
    WHERE Direccion_Proveedor = 'santiago' and TB_Producto.Codigo_Proveedor = TB_Proveedor.Codigo_Proveedor 
    GO
    ```
1. Consultar todas las ventas registradas donde se ha comprado el producto cuyo codigo corresponde al 100001
    ```sql
    SELECT Cantidad , Descripcion_Producto FROM TB_Detalle_Factura_Venta, TB_Producto 
    WHERE TB_Producto.Codigo_Producto = 100001 AND TB_Producto.Codigo_Producto = TB_Detalle_Factura_Venta.Codigo_Producto 
    GO
    ```

1. Consultar todas las ventas donde se hayan vendido el producto 100004
    ```sql
    SELECT TB_Detalle_Factura_Venta.Codigo_Factura, TB_Detalle_Factura_Venta.Cantidad 
    FROM TB_Detalle_Factura_Venta 
    WHERE Codigo_Producto = 100004 
    GO
    ```

1. Consultar todos los datos del proveedor para las facturas donde se haya comprado el producto 100006
    ```sql
    SELECT DISTINCT TB_Proveedor.Codigo_Proveedor , TB_Proveedor.PrimerApellido_Proveedor, TB_Proveedor.SegundoApellido_Proveedor,  TB_Proveedor.TelefonoFijo_Proveedor,TB_Proveedor.TelefonoMovil_Proveedor, TB_Proveedor.Direccion_Proveedor, TB_Proveedor.Email_Proveedor 
    FROM TB_Proveedor, TB_Detalle_Factura_Compra, TB_Factura_Compra 
    WHERE TB_Detalle_Factura_Compra.Codigo_Producto = 100006 AND TB_Proveedor.Codigo_Proveedor = TB_Factura_Compra.Codigo_Proveedor 
    GO
    ```

1. Consultar el nombre del cliente y la dirección cuyos clientes hayan comprado el producto con el código registrado 100007
    ```sql
    SELECT TB_Cliente.Nombre_Cliente, TB_Cliente.Direccion_Cliente FROM TB_Cliente, TB_Factura_Venta , TB_Detalle_Factura_Venta
    WHERE TB_Cliente.Codigo_Cliente = TB_Factura_Venta.Codigo_Cliente  AND TB_Factura_Venta.Codigo_Factura = TB_Detalle_Factura_Venta.Codigo_Factura AND TB_Detalle_Factura_Venta.Codigo_Producto = 100007
    GO
    ```

1. Consultar el código del cliente, nombre o descripción del producto y precio de venta del producto para la factura Nº 1000
    ```sql
    SELECT TB_Cliente.Codigo_Cliente, TB_Producto.Descripcion_Producto, TB_Producto.Precio_Venta 
    FROM TB_Cliente, TB_Producto, TB_Detalle_Factura_Venta, TB_Factura_Venta 
    WHERE TB_Detalle_Factura_Venta.Codigo_Factura = 1000 AND TB_Detalle_Factura_Venta.Codigo_Producto = TB_Producto.Codigo_Producto AND TB_Detalle_Factura_Venta.Codigo_Factura = TB_Factura_Venta.Codigo_Factura 
    AND TB_Factura_Venta.Codigo_Cliente = TB_Cliente.Codigo_Cliente 
    GO
    ```

1. Consultar los datos de los Clientes (Nombre completo, dirección, teléfonos de contacto, Email )  que no hayan comprado el producto con el código asignado 10003.
    ```sql
    SELECT DISTINCT TB_Cliente.Nombre_Cliente, TB_Cliente.Direccion_Cliente, TB_Cliente.TelefonoMovil_Cliente, TB_Cliente.Email_Cliente 
    FROM TB_Cliente, TB_Detalle_Factura_Venta, TB_Factura_Venta 
    WHERE TB_Cliente.Codigo_Cliente = TB_Factura_Venta.Codigo_Cliente AND TB_Factura_Venta.Codigo_Factura = TB_Detalle_Factura_Venta.Codigo_Factura AND TB_Detalle_Factura_Venta.Codigo_Producto <> 100003
    GO
    ```

1. Seleccionar los datos de las facturas (Codigo_Factura,  Fecha_Factura, Nombre del Cliente, Nombre del Producto) de todas las ventas donde la dirección del cliente sea distinto de Santiago
    ```sql
    SELECT TB_Factura_Venta.Codigo_Factura, TB_Factura_Venta.Fecha_Factura, TB_Cliente.Nombre_Cliente, TB_Producto.Descripcion_Producto 
    FROM TB_Factura_Venta, TB_Cliente, TB_Detalle_Factura_Venta, TB_Producto 
    WHERE TB_Cliente.Codigo_Cliente = TB_Factura_Venta.Codigo_Cliente AND TB_Factura_Venta.Codigo_Factura = TB_Detalle_Factura_Venta.Codigo_Factura AND TB_Detalle_Factura_Venta.Codigo_Producto = TB_Producto.Codigo_Producto AND TB_Cliente.Direccion_Cliente <> 'Santiago' 
    GO
    ```

1. Consultar los datos de los Clientes (Nombre completo, dirección, teléfonos de contacto, Email )  para todas las ventas cuya fecha de venta se haya realizado el 02/04/2012 o dirección cliente sea distinto de Santiago.
    ```sql
    SELECT DISTINCT TB_Cliente.Nombre_Cliente, TB_Cliente.PrimerApellido_Cliente,TB_Cliente.Email_Cliente, TB_Cliente.TelefonoFijo_Cliente, TB_Cliente.TelefonoMovil_Cliente, TB_Cliente. Direccion_Cliente
    FROM TB_Cliente, TB_Factura_Venta 
    WHERE TB_Cliente.Codigo_Cliente = TB_Factura_Venta.Codigo_Cliente AND TB_Factura_Venta.Fecha_Factura = 02/04/2012 OR TB_Cliente.Direccion_Cliente <> 'Santiago'
    GO
    ```

1. Consultar la descripción o nombre del producto, el precio de venta y el precio de costo de aquellos productos cuyo proveedor  tenga el código 103 o el proveedor esté ubicado en ciudad de Panamá
    ```sql
    SELECT TB_Producto.Descripcion_Producto, TB_Producto.Precio_Venta, TB_Producto.Precio_Costo
    FROM TB_Producto, TB_Proveedor  
    WHERE TB_Proveedor.Codigo_Proveedor = TB_Producto.Codigo_Proveedor AND TB_Proveedor.Codigo_Proveedor = 103 OR TB_Proveedor.Direccion_Proveedor = 'Panama'
    GO
    ```

1. Consultar código de producto, nombre producto, código proveedor, nombre proveedor y teléfono fijo del proveedor  cuyo precio de costo esté en el rango de 0 a 350 y el proveedor esté localizado en Santiago
    ```sql
    SELECT TB_Proveedor.Codigo_Proveedor, TB_Proveedor.Nombre_Proveedor, TB_Proveedor.TelefonoFijo_Proveedor, TB_Producto.Codigo_Producto, TB_Producto.Descripcion_Producto 
    FROM TB_Producto, TB_Proveedor
    WHERE TB_Producto.Codigo_Proveedor = TB_Proveedor.Codigo_Proveedor AND TB_Producto.Precio_Costo BETWEEN 0 AND 350
    GO
    ```

1. Consultar  el código del proveedor, nombre del Proveedor, primer apellido y datos de contacto de los proveedores con localización en Chitré y  Panamá y vendan productos cuyo precio de costo sea superior a 50 balboas 
    ```sql
    SELECT DISTINCT TB_Proveedor.Codigo_Proveedor, TB_Proveedor.Nombre_Proveedor, TB_Proveedor.PrimerApellido_Proveedor, TB_Proveedor.TelefonoFijo_Proveedor 
    FROM TB_Proveedor, TB_Producto 
    WHERE (TB_Producto.Codigo_Proveedor = TB_Proveedor.Codigo_Proveedor) AND (TB_Producto.Precio_Costo >= 50) AND (TB_Proveedor.Direccion_Proveedor BETWEEN 'Chitre' AND 'Panama')
    GO
    ```

1. Consultar todos los proveedores que hayan proveídos productos al inventario de la empresa ordenándolos por la dirección del proveedor. 
    ```sql
    SELECT DISTINCT TB_Proveedor.Nombre_Proveedor, TB_Proveedor.Direccion_Proveedor  FROM TB_Proveedor, TB_Producto, TB_Detalle_Factura_Compra 
    WHERE TB_Producto.Codigo_Proveedor = TB_Proveedor.Codigo_Proveedor AND TB_Producto.Codigo_Producto = TB_Detalle_Factura_Compra.Codigo_Producto
    ORDER BY TB_Proveedor.Direccion_Proveedor 
    GO
    ```

1. Consultar todos las facturas de ventas mostrando información del código de factura, descripción del producto, cantidad y fecha de venta ordenando los resultados a partir de las ventas más recientes. 
    ```sql
    SELECT TB_Factura_Venta.Codigo_Factura, TB_Factura_Venta.Fecha_Factura, TB_Detalle_Factura_Venta.Cantidad, TB_Producto.Descripcion_Producto 
    FROM TB_Producto,TB_Factura_Venta, TB_Detalle_Factura_Venta 
    WHERE TB_Factura_Venta.Codigo_Factura  = TB_Detalle_Factura_Venta.Codigo_Factura AND TB_Detalle_Factura_Venta.Codigo_Producto =  TB_Producto.Codigo_Producto  
    ORDER BY TB_Factura_Venta.Fecha_Factura DESC
    GO
    ```

1. Contar todas las facturas para cada unos de los clientes registrados en las base de datos. 
    ```sql
    SELECT TB_Cliente.Nombre_Cliente, COUNT(TB_Factura_Venta.Codigo_Factura) AS "Cantidad de Facturas" FROM TB_Factura_Venta, TB_Cliente
    WHERE TB_Factura_Venta.Codigo_Cliente = TB_Cliente.Codigo_Cliente
    GROUP BY TB_Cliente.Nombre_Cliente 
    GO
    ```

1. Consultar la factura de venta cuyo valor sea el más alto y el más bajo. 
    ```sql
    SELECT MAX(TB_Factura_Venta.Monto_Total) AS "Maxima compra", MIN(TB_Factura_Venta.Monto_Total) AS "Minima Compra"
    FROM TB_Factura_Venta
    GO
    ```

1. Consultar las compras totales para cada uno de los Proveedores que han vendido productos a la Empresa.
    ```sql
    SELECT TB_Proveedor.Nombre_Proveedor, COUNT(TB_Factura_Compra.Codigo_Proveedor) AS "Compras Totales"
    FROM TB_Proveedor, TB_Factura_Compra 
    WHERE TB_Proveedor.Codigo_Proveedor = TB_Factura_Compra.Codigo_Proveedor
    GROUP BY TB_Proveedor.Nombre_Proveedor
    GO 
    ```

1. Consultar las ventas totales para cada uno de los Clientes que tienen registro en la base de datos de la empresa. 
    ```sql
    SELECT TB_Cliente.Codigo_Cliente, TB_Cliente.Nombre_Cliente, SUM(TB_Factura_Venta.Monto_Total) AS "Ventas Totales" 
    FROM TB_Cliente, TB_Factura_Venta
    WHERE TB_Cliente.Codigo_Cliente = TB_Factura_Venta.Codigo_Cliente 
    GROUP BY TB_Cliente.Codigo_Cliente, TB_Cliente.Nombre_Cliente 
    GO
    ```

1. Mostrar las ventas totales mayores de 1200 para cada uno de los Clientes que tienen registro en la base de datos de la empresa.
    ```sql
    SELECT TB_Cliente.Codigo_Cliente, TB_Cliente.Nombre_Cliente, SUM(TB_Factura_Venta.Monto_Total) AS "Ventas Totales"
    FROM TB_CLiente, TB_Factura_Venta 
    WHERE TB_Cliente.Codigo_Cliente = TB_Factura_Venta.Codigo_Cliente 
    GROUP BY TB_CLiente.Codigo_Cliente, Nombre_Cliente 
    HAVING SUM(TB_Factura_Venta.Monto_Total)>1200
    GO
    ```

1. Consultar el 50% de todos los productos listados en la base de datos mostrando la información: código del producto, descripción del producto, precio de venta, nombre y apellido del proveedor como un solo campo.
    ```sql
    SELECT TOP 50 PERCENT TB_Producto.Codigo_Producto, TB_Producto.Descripcion_Producto, TB_Producto.Precio_Venta,
    (TB_Proveedor.Nombre_Proveedor + ' ' + TB_Proveedor.PrimerApellido_Proveedor) AS "Proveedor" 
    FROM TB_Producto, TB_Proveedor 
    WHERE TB_Producto.Codigo_Proveedor = TB_Proveedor.Codigo_Proveedor 
    ORDER BY Codigo_Producto ASC
    GO
    ```

1. Consultar la descripcion del producto, el precio de venta, el precio de costo, codigo del proveedor, nombre del proveedor y dirección del proveedor para los proveedores con los códigos 100, 102, 103.
    ```sql
    SELECT TB_Producto.Descripcion_Producto, TB_Producto.Precio_Costo, TB_Proveedor.Codigo_Proveedor, TB_Proveedor.Nombre_Proveedor, TB_Proveedor.Direccion_Proveedor 
    FROM TB_Producto, TB_Proveedor 
    WHERE (TB_Proveedor.Codigo_Proveedor BETWEEN 100 AND 103) AND TB_Producto.Codigo_Proveedor = TB_Proveedor.Codigo_Proveedor 
    ORDER BY Codigo_Proveedor ASC
    GO
    ```

1. Consultar la información de todos los productos con descripción Tipo “USB” cuyo precio de costo oscile entre 40 a 100 balboas.
    ```sql
    SELECT * FROM TB_Producto 
    WHERE (Descripcion_Producto LIKE '%USB%') AND (TB_Producto.Precio_Costo BETWEEN 40 AND 100)
    GO
    ```

1. 29.	Consultar todas las facturas de ventas mostrando la siguiente información: código de factura, nombre completo del cliente, fecha de venta y la cantidad de Ítems adquiridos por cada factura. Ordenar los resultados a partir de las facturas con mayor cantidad  de productos comprados.
    ```sql
    SELECT TB_Factura_Venta.Codigo_Factura, Nombre_Cliente, Fecha_Factura, SUM(TB_Detalle_Factura_Venta.Cantidad) AS "Cantidad de items" 
    FROM TB_Factura_Venta, TB_Cliente, TB_Detalle_Factura_Venta 
    WHERE TB_Cliente.Codigo_Cliente=TB_Factura_Venta.Codigo_Cliente and TB_Factura_Venta.Codigo_Factura=TB_Detalle_Factura_Venta.Codigo_Factura 
    GROUP BY TB_Factura_Venta.Codigo_Factura, Nombre_Cliente, Fecha_Factura 
    ORDER BY [Cantidad de items] DESC
    GO
    ```

1. Totalizar las cantidades de productos vendidos por Factura y presentar sólo aquellas aquellas facturas donde se haya comprado una cantidad superior a tres productos.
    ```sql
    SELECT TB_Factura_Venta.Codigo_Factura, COUNT(TB_Detalle_Factura_Venta.Codigo_Producto) AS "Cantidad de Productos Diferentes" 
    FROM TB_Detalle_Factura_Venta, TB_Factura_Venta
    WHERE TB_Factura_Venta.Codigo_Factura = TB_Detalle_Factura_Venta.Codigo_Factura 
    GROUP BY TB_Factura_Venta.Codigo_Factura
    HAVING COUNT(TB_Detalle_Factura_Venta.Codigo_Producto) > 3
    GO
    ```

1. Consultar la información de los productos (codigo, descripción, precio venta, precio costo, nombre del proveedor), dirección del proveedor cuyo precio de venta este en el rango 100 a 500 y proveedor localizado en Santiago (Clausula Distinct).
    ```sql
    SELECT DISTINCT TB_Producto.Codigo_Producto, TB_Producto.Descripcion_Producto, TB_Producto.Precio_Venta, TB_Producto.Precio_Costo, TB_Proveedor.Nombre_Proveedor, TB_Proveedor.Direccion_Proveedor 
    FROM TB_Producto, TB_Proveedor 
    WHERE TB_Proveedor.Codigo_Proveedor = TB_Producto.Codigo_Proveedor  AND (TB_Producto.Precio_Venta BETWEEN 100 AND 500) AND Direccion_Proveedor = 'Santiago'
    GO
    ```

1. Consultar todos los productos cuyo proveedores estén localizados en Santiago.
    ```sql
    SELECT TB_Producto.Descripcion_Producto  FROM TB_Proveedor INNER JOIN TB_Producto ON TB_Proveedor.Codigo_Proveedor = TB_Producto.Codigo_Proveedor 
    WHERE TB_Proveedor.Direccion_Proveedor = 'Santiago'
    GO
    ```

1. Consultar todas las ventas registradas donde se ha comprado el producto cuyo código corresponde al 100001
    ```sql
    SELECT * FROM TB_Detalle_Factura_Venta INNER JOIN TB_Producto ON TB_Detalle_Factura_Venta.Codigo_Producto = TB_Producto.Codigo_Producto 
    WHERE TB_Producto.Codigo_Producto =  100001
    GO
    ```

1. Consultar todas las ventas donde se hayan vendido el producto 100004
    ```sql
    SELECT * FROM TB_Detalle_Factura_Venta INNER JOIN TB_Producto ON TB_Detalle_Factura_Venta.Codigo_Producto = TB_Producto.Codigo_Producto 
    WHERE TB_Producto.Codigo_Producto = 100004
    GO
    ```

1. Consultar todos los datos del proveedor para las facturas donde se haya comprado el producto 100006.
    ```sql
    SELECT * FROM TB_Proveedor INNER JOIN TB_Factura_Compra ON TB_Proveedor.Codigo_Proveedor = TB_Factura_Compra.Codigo_Proveedor INNER JOIN TB_Detalle_Factura_Compra ON TB_Factura_Compra.Codigo_Factura = TB_Detalle_Factura_Compra.Codigo_Factura 
    WHERE TB_Detalle_Factura_Compra.Codigo_Producto = 100006
    GO

    ```

1. Consultar los datos de los Clientes (Nombre completo, dirección, teléfonos de contacto, Email)  para todas las ventas cuya fecha de venta se haya realizado el 02/04/2012 o dirección cliente sea distinto de Santiago.
    ```sql
    SELECT DISTINCT (TC.Nombre_Cliente +' '+ TC.PrimerApellido_CLiente +' '+ TC.SegundoApellido_Cliente) AS 'Nombre Completo Cliente', TC.TelefonoMovil_Cliente, TC.Direccion_Cliente, TC.Email_Cliente
    FROM TB_Cliente AS TC INNER JOIN TB_Factura_Venta AS TFV ON TC.Codigo_Cliente = TFV.Codigo_Cliente
    WHERE TFV.Fecha_Factura = '02/04/2012' OR TC.Direccion_Cliente <> 'Santiago'
    GO
    ```

1. Consultar  el código del proveedor, nombre del Proveedor, primer apellido y datos de contacto de los proveedores con localización en Chitré y  Panamá y vendan productos cuyo precio de costo sea superior a 50 balboas.
    ```sql
    SELECT DISTINCT TP.Codigo_Proveedor, TP.Nombre_Proveedor, TP.PrimerApellido_Proveedor, (TP.TelefonoFijo_Proveedor+ ' / ' + TP.TelefonoMovil_Proveedor+ '/'+ TP.Email_Proveedor) AS 'Telefono Fijo/ Celular / Correo'
    FROM TB_Proveedor AS TP INNER JOIN TB_Producto AS TPR ON TP.Codigo_Proveedor = TPR.Codigo_Proveedor 
    WHERE TP.Direccion_Proveedor = 'Chitre' OR TP.Direccion_Proveedor = 'Panama' AND TPR.Precio_Venta > 50
    GO
    ```

1. Contar todas las facturas para cada uno de los clientes registrados en las base de datos. Mostrar código del cliente, nombre y apellido del cliente y teléfono y cantidad de facturas. 
    ```sql
    SELECT COUNT(TFV.Codigo_Factura) AS 'Cantidad de Facturas', TC.Codigo_Cliente, TC.Nombre_Cliente, TC.Codigo_Cliente, TC.PrimerApellido_Cliente, TC.TelefonoMovil_Cliente
    FROM TB_Factura_Venta AS TFV INNER JOIN TB_Cliente AS TC ON TFV.Codigo_Cliente = TC.Codigo_Cliente 
    GROUP BY TC.Nombre_Cliente, TC.Codigo_Cliente, TC.PrimerApellido_Cliente, TC.TelefonoMovil_Cliente
    GO
    ```

1. Consultar las compras totales para cada uno de los Proveedores que han vendido productos a la Empresa. Mostrar código del proveedor, nombre y  apellido del proveedor, teléfono de contacto y el monto total de facturas. 
    ```sql
    SELECT SUM(TFC.Monto_Total) AS 'Monto Total de las Facturas' , TP.Codigo_Proveedor, TP.Nombre_Proveedor, TP.PrimerApellido_Proveedor 
    FROM TB_Factura_Compra AS TFC INNER JOIN TB_Proveedor AS TP ON TP.Codigo_Proveedor = TFC.Codigo_Proveedor 
    GROUP BY TP.Codigo_Proveedor, TP.Nombre_Proveedor, TP.PrimerApellido_Proveedor
    GO
    ```

1. Consultar las ventas totales mayores de 1200 para cada uno de los Clientes que tienen registro en la base de datos de la empresa.
    ```sql
    SELECT SUM(TFV.Monto_Total) AS 'Monto de Compra' , TC.Nombre_Cliente 
    FROM TB_Cliente AS TC INNER JOIN TB_Factura_Venta AS TFV ON TC.Codigo_Cliente = TFV.Codigo_Cliente 
    GROUP BY TC.Nombre_Cliente
    HAVING SUM(TFV.Monto_Total) > 1200
    GO
    ```

1. Consultar los datos de las facturas (Código Factura,  Fecha Factura, Nombre del Cliente, Nombre del Producto) de todas las ventas donde la dirección del cliente sea distinto de Santiago
    ```sql
    SELECT TFV.Codigo_Factura, TFV.Fecha_Factura, TC.Nombre_Cliente, TP.Descripcion_Producto
    FROM TB_Factura_Venta AS TFV INNER JOIN TB_Cliente AS TC ON TC.Codigo_Cliente  = TFV.Codigo_Cliente INNER JOIN TB_Detalle_Factura_Venta AS TDFV ON TFV.Codigo_Factura = TDFV.Codigo_Factura 
    INNER JOIN TB_Producto AS TP ON TDFV.Codigo_Producto = TP.Codigo_Producto
    WHERE TC.Direccion_Cliente <> 'Santiago'
    GO
    ```

1. Consultar el monto total de cada factura para todos los clientes registrados en la base de datos, sin importar si tienen facturas asociadas.
    ```sql
    SELECT TFV.Monto_Total AS 'Monto Factura' , TC.Nombre_Cliente 
    FROM TB_Cliente AS TC LEFT JOIN TB_Factura_Venta AS TFV ON TC.Codigo_Cliente = TFV.Codigo_Cliente 
    GROUP BY TC.Nombre_Cliente, TFV.Monto_Total 
    GO
    ```

1. Consultar los datos del Proveedor, Nombre, Apellido, datos de la  Factura y Monto de cada Factura. Sin embargo, se requiere traer todos los  proveedores aun cuando no tengan facturas asociadas.
    ```sql
    SELECT TP.Nombre_Proveedor, TP.PrimerApellido_Proveedor, TFC.Fecha_Factura, TFC.Monto_Total, TFC.Impuesto, TFC.Descuento
    FROM TB_Proveedor AS TP LEFT JOIN TB_Factura_Compra AS TFC ON TP.Codigo_Proveedor = TFC.Codigo_Proveedor 
    GO
    ```

1. Consultar el código del proveedor, nombre y apellido del proveedor, código de la factura, código del producto, descripción del producto  y cantidad de productos vendidos por el proveedor por factura, mostrando todos los proveedores aún sin haber proveído productos.
    ```sql
    SELECT TP.Codigo_Proveedor, TP.Nombre_Proveedor, TP.PrimerApellido_Proveedor, TDFC.Codigo_Factura, TPR.Codigo_Producto, TPR.Descripcion_Producto, TDFC.Cantidad
    FROM TB_Proveedor AS TP LEFT JOIN TB_Factura_Compra AS TFC ON TP.Codigo_Proveedor = TFC.Codigo_Proveedor LEFT JOIN TB_Detalle_Factura_Compra AS TDFC ON TFC.Codigo_Factura = TDFC.Codigo_Factura 
    LEFT JOIN TB_Producto AS TPR ON TDFC.Codigo_Producto = TPR.Codigo_Producto 
    GROUP BY TP.Codigo_Proveedor, TP.Nombre_Proveedor, TP.PrimerApellido_Proveedor, TDFC.Codigo_Factura, TPR.Codigo_Producto, TPR.Descripcion_Producto, TDFC.Cantidad
    GO
    ```

1. Consultar el Producto cartesiano de las tabla Cliente y Factura Venta.
    ```sql
    SELECT * FROM TB_Cliente CROSS JOIN TB_Factura_Venta 
    GO
    ```

1. Consultar el Producto cartesiano de las tablas Producto y Proveedor. 
    ```sql
    SELECT * FROM TB_Producto CROSS JOIN TB_Proveedor 
    GO
    ```

1. Consultar todas las Ventas y Compras en un única consulta. Se debe mostrar la siguiente información tanto para las ventas como para las compras en la consulta: Número de Factura, Fecha de transacción, y Monto total. Adicional, se debe agregar un campo que permita  identificar cual registro pertenece a venta y cual a compra. 
    ```sql
    SELECT 'Facturas Compra' AS 'Tipo Factura', TFC.Monto_Total, TFC.Fecha_Factura, TFC.Codigo_Factura
    FROM TB_Factura_Compra AS TFC
    UNION ALL
    SELECT 'Facturas Venta' AS 'Tipo Factura' ,TFV.Monto_Total, TFV.Fecha_Factura, TFV.Codigo_Factura
    FROM TB_Factura_Venta AS TFV
    GO
    ```

1. Consultar todos los Clientes y Proveedores en un única consulta. Se debe mostrar la siguiente información tanto para las Clientes como para las Proveedores en la consulta: Código de Cliente/Proveedor, Nombre y Apellido de la Persona, y Monto Total de todas las Facturas. Adicional, se debe agregar un campo que permita  identificar cual registro pertenece a Cliente y cual a Proveedor.
    ```sql
    SELECT 'Informacion Cliente' AS 'Tipo Usuario' , (TC.Nombre_Cliente +' '+ TC.PrimerApellido_Cliente) AS 'Nombre Completo' , TC.Codigo_Cliente, SUM(TFV.Monto_Total) AS 'Monto total de todas las facturas'
    FROM TB_Cliente AS TC INNER JOIN TB_Factura_Venta AS TFV ON TC.Codigo_Cliente = TFV.Codigo_Cliente 
    GROUP BY (TC.Nombre_Cliente +' '+ TC.PrimerApellido_Cliente), TC.Codigo_Cliente
    UNION ALL
    SELECT 'Informacion Proveedor' AS 'Tipo Usuario' , (TP.Nombre_Proveedor +' '+ TP.PrimerApellido_Proveedor ) AS 'Nombre Completo' , TP.Codigo_Proveedor, SUM(TFC.Monto_Total) AS 'Monto total de todas las facturas'
    FROM TB_Proveedor AS TP INNER JOIN TB_Factura_Compra AS TFC ON TP.Codigo_Proveedor = TFC.Codigo_Proveedor 
    GROUP BY (TP.Nombre_Proveedor +' '+ TP.PrimerApellido_Proveedor), TP.Codigo_Proveedor
    GO
    ```

1. Crear una Vista de la tabla proveedores sólo mostrando el nombre del proveedor, primer apellido y la información de contacto disponible.
    ```sql
    CREATE VIEW V_TB_Proveedor
    AS
    SELECT TB_Proveedor.Nombre_Proveedor, TB_Proveedor.PrimerApellido_Proveedor, (TB_Proveedor.TelefonoFijo_Proveedor + ' / ' +  TB_Proveedor.TelefonoMovil_Proveedor + ' / ' + TB_Proveedor.Email_Proveedor) AS 'Informacion de contacto'
    FROM TB_Proveedor 
    GO

    SELECT * FROM V_TB_Proveedor
    GO

    ```

1. Crear una Vista que consulte todos las facturas de ventas mostrando información del código de factura, descripción del producto, cantidad y fecha de venta ordenando los resultados a partir de las ventas más recientes.
    ```sql
    CREATE VIEW V_TB_Factura_Venta
    AS
    SELECT TDFV.Codigo_Factura, TBPRO.Descripcion_Producto, TDFV.Cantidad, TFV.Fecha_Factura
    FROM TB_Producto AS TBPRO INNER JOIN TB_Detalle_Factura_Venta AS TDFV ON TBPRO.Codigo_Producto = TDFV.Codigo_Producto 
    INNER JOIN TB_Factura_Venta AS TFV ON TDFV.Codigo_Factura = TFV.Codigo_Factura 
    GO

    SELECT * FROM V_TB_Factura_Venta 
    ORDER BY V_TB_Factura_Venta.Fecha_Factura DESC
    GO
    ```

1. Crear una vista que consulte las compras totales para cada uno de los Proveedores que han vendido productos a la Empresa.
    ```sql
    CREATE VIEW V_TB_Compras_Totales
    AS
    SELECT TBPRO.Nombre_Proveedor, TFC.Monto_Total FROM TB_Factura_Compra AS TFC LEFT JOIN TB_Proveedor AS TBPRO ON TFC.Codigo_Proveedor = TBPRO.Codigo_Proveedor 
    GO

    SELECT * FROM V_TB_Compras_Totales 
    ```

1. Crear una vista que consulte las ventas totales para cada uno de los Clientes que tienen registro en la base de datos de la empresa. 
    ```sql
    CREATE VIEW V_Ventas_Clientes
    AS
    SELECT TC.Nombre_Cliente, TFV.Monto_Total FROM TB_Factura_Venta AS TFV LEFT JOIN TB_Cliente AS TC ON TFV.Codigo_Cliente = TC.Codigo_Cliente 
    GO

    SELECT V_Ventas_Clientes.Nombre_Cliente , V_Ventas_Clientes.Monto_Total AS 'Ventas Totales' FROM V_Ventas_Clientes 
    GO
    ```

1. Crear una vista que muestre todos los nombres de los clientes y proveedores en una única consulta, permitiendo identificar si es cliente o proveedor.
    ```sql
    CREATE VIEW V_Proveedor_Cliente
    AS
    SELECT 'Cliente' AS 'Tipo Usuario', TC.Nombre_Cliente 
    FROM TB_Cliente AS TC
    UNION ALL
    SELECT 'Proveedor' AS 'Tipo Usuario', TPR.Nombre_Proveedor
    FROM TB_Proveedor AS TPR
    GO

    SELECT * FROM V_Proveedor_Cliente
    ```

1. Crear una vista que muestre todas las Ventas y Compras en un única consulta. Tanto para las Ventas como para las Compras se debe mostrar la siguiente información: codigo de factura, nombre de la persona, fecha de la factura, monto total y Tipo de Transacción para identificar si es una venta o una compra. 
    ```sql
    CREATE VIEW V_Transacciones
    AS
    SELECT 'Compra' AS 'Tipo de Transaccion', TFC.Codigo_Factura, TPRO.Nombre_Proveedor, TFC.Fecha_Factura, TFC.Monto_Total
    FROM TB_Factura_Compra AS TFC INNER JOIN TB_Proveedor AS TPRO ON TFC.Codigo_Proveedor = TPRO.Codigo_Proveedor 
    UNION ALL
    SELECT 'Venta' AS 'Tipo de Transaccion', TFV.Codigo_Factura, TC.Nombre_Cliente, TFV.Fecha_Factura, TFV.Monto_Total
    FROM TB_Factura_Venta AS TFV INNER JOIN TB_Cliente AS TC ON TFV.Codigo_Cliente = TC.Codigo_Cliente 
    GO

    SELECT * FROM V_Transacciones
    ```

1. Insertar 2 registros nuevos de clientes. 
    ```sql
    Insert Into TB_CLIENTE (Codigo_Cliente, Cedula_Cliente, Nombre_Cliente, PrimerApellido_Cliente, SegundoApellido_Cliente, TelefonoFijo_Cliente, TelefonoMovil_Cliente, Direccion_Cliente, Email_Cliente, Saldo_Cliente) 
    Values ('00011', '9-752-1198', 'Jair', 'Hernandez', 'Juarez', '998-3536', '6697-0347', 'Santiago', 'jairjuarez@gmail.com', 0)
    GO

    Insert Into TB_CLIENTE (Codigo_Cliente, Cedula_Cliente, Nombre_Cliente, PrimerApellido_Cliente, SegundoApellido_Cliente, TelefonoFijo_Cliente, TelefonoMovil_Cliente, Direccion_Cliente, Email_Cliente, Saldo_Cliente) 
    Values ('00012', '9-52-199', 'Temistocles', 'Bartolio', 'Vernaza', '998-4166', '6777-1638', 'Chorrera', 'temisbarto@gmail.com', 44.97)
    GO
    ```

1. Insertar un nuevo producto.
    ```sql
    INSERT INTO TB_Producto (Codigo_Producto, Descripcion_Producto, Cantidad_Inventario, Precio_Venta, Precio_Costo, Codigo_Proveedor) 
    VALUES (100008, 'Procesador Ryzen 2200G', 15, 114.90, 94.00, 103)
    GO
    ```

1. Insertar un nuevo proveedor 
    ```sql
    INSERT INTO TB_Proveedor (Codigo_Proveedor, Nombre_Proveedor, PrimerApellido_Proveedor, SegundoApellido_Proveedor, TelefonoFijo_Proveedor, TelefonoMovil_Proveedor, Direccion_Proveedor, Email_Proveedor) 
    VALUES (105, 'Alibaba', 'Rodriguez', 'Perez', '998-8180', '6760-2106', 'Colon', 'babaperez@gmail.com')
    GO
    ```

1. Insertar un registro completo de Factura de Venta con uno de los clientes nuevos. La factura de vente debe incluir como mínimo 2 productos. 
    ```sql
    INSERT INTO TB_Factura_Venta (Codigo_Factura, Fecha_Factura, Codigo_Cliente, Monto_Total, Impuesto, Descuento)
    VALUES (1007, '19/04/2014', '00012', 2345.00, 153.41,0)
    GO
    INSERT INTO TB_Detalle_Factura_Venta (IdDetalle, Codigo_Factura, Codigo_Producto, Cantidad) 
    VALUES (1, 1007, 100008, 4)
    GO
    INSERT INTO TB_Detalle_Factura_Venta (IdDetalle, Codigo_Factura, Codigo_Producto, Cantidad) 
    VALUES (2, 1007, 100004, 2)

    ```

1. Actualizar el correo electrónico de los clientes ‘00005’, ‘00006’
    ```sql
    UPDATE TB_Cliente SET Email_Cliente = 'peras@gmail.com' WHERE Codigo_Cliente = '00005'
    GO
    UPDATE TB_Cliente SET Email_Cliente = 'manzanas@gmail.com' WHERE Codigo_Cliente = '00006'
    ```

1. Escriba el código SQL para actualizar el precio de venta de todos los productos cuyo precio de venta este en el rango de 30 a 100. Se debe actualizar el precio de venta decrementando en un 5% el precio de venta actual. 
    ```sql
    UPDATE TB_Producto SET Precio_Venta = (Precio_Venta - (Precio_Venta*0.05)) WHERE Precio_Venta BETWEEN 30 AND 100
    GO
    ```

1. Eliminar todos los clientes con saldo cero.
    ```sql
    DELETE FROM TB_Cliente WHERE Saldo_Cliente = 0
    GO
    ```

1. Eliminar la nueva factura adicionada con todos los detalles 
    ```sql
    DELETE FROM TB_Factura_Venta WHERE Codigo_Factura = 1007
    GO
    DELETE FROM TB_Detalle_Factura_Venta WHERE Codigo_Factura = 1007
    GO
    ```

1. Escriba el código SQL para eliminar todos los clientes  cuyo saldo este coincida con los siguientes valores  del conjunto  indicado (10, 20, 60, 100) saldo pendiente.
    ```sql
    DELETE FROM TB_Cliente WHERE Saldo_Cliente IN (10,20,60,100)
    GO
    ```

1. Escriba el código SQL para validar la introducción de nuevos productos a la base de datos DB_Empresa_ZYZ utilizando estructura de control a través del campo “Descripcion_Producto”. Si el producto no existe, se registra el nuevo producto en la tabla correspondiente. De lo contrario si el producto ya aparece registrado con la descripción enviada, se envía un mensaje al usuario indicando que el “Producto ya está registrado”
    ```sql
    DECLARE @Des_Product VARCHAR(40)
    DECLARE @Product INT
    SET @Des_Product = 'Disco duro portatil de 1 TB' 
    IF EXISTS(SELECT * FROM TB_Producto  WHERE  TB_Producto.Descripcion_Producto = @Des_Product) 
        BEGIN
            PRINT 'Producto ya está registrado'
            --SELECT @Product = TB_Producto.Cantidad_Inventario FROM TB_Producto 
            --PRINT @Product
        END
    ELSE
        BEGIN
            INSERT INTO TB_Producto (Codigo_Producto, Descripcion_Producto, Cantidad_Inventario, Precio_Venta, Precio_Costo, Codigo_Proveedor) VALUES (100009, 'Disco duro portatil de 1 TB', 13, 30.05, 89.90, 100)   
            PRINT 'Producto agregado'
        END
    GO

    SELECT * FROM TB_Producto 

    ```

1. Escriba el código SQL de una función para categorizar los proveedores de la base de datos DB_EmpresaXYZ a partir de un monto almacenado pasado como parámetro a la función. A partir del monto total acumulado de las ventas realizadas por cada proveedor se desea categorizar los proveedores como “Proveedor VIP” si supera el monto umbral de compras. “Proveedor Frecuente” si está en el rango de menor que el monto umbral  y mayor que el 30% del monto umbral establecido. “Proveedor Regular” si está por debajo del 30% del monto umbral establecido. 
    ```sql
    CREATE FUNCTION ClasificardorProveedor (@umbral FLOAT)
    RETURNS TABLE
    AS
    RETURN
    (
    SELECT TB_Proveedor.Codigo_Proveedor, TB_Proveedor.Nombre_Proveedor, TB_Proveedor.PrimerApellido_Proveedor AS 'Apellido Proveedor', SUM(Monto_Total) AS 'Monto Total',
    CASE WHEN SUM(Monto_Total) > @umbral THEN 'Proveedor VIP'
    WHEN SUM(Monto_Total) < @umbral And SUM(Monto_Total) > @umbral*0.3 THEN 'Proveedor frecuente'
    Else 'Proveedor Regular' END AS 'Tipo'
    FROM TB_Proveedor Left Join TB_Factura_Compra ON TB_Proveedor.Codigo_Proveedor = TB_Factura_Compra .Codigo_Proveedor 
    GROUP BY TB_Proveedor.Codigo_Proveedor, Nombre_Proveedor, PrimerApellido_Proveedor 
    );
    GO

    SELECT * FROM ClasificardorProveedor(1250)
    ```

1. Escriba el código SQL  para reservar 5 códigos de productos nuevos pendientes por definir. La información de los campos restantes se completarán con datos por defecto, que luego se pueden modificar. Se debe realizar un procedimiento  mediante una estructura repetitiva para crear los nuevos códigos de los productos. Adicional, se debe determinar internamente cuál es el último identificador de producto registrado para iniciar la reservación de los nuevos códigos, el resto de información (Descripcion_Producto, Cantidad_Inventario, Precio_Venta, Precio_Costo, codigo_Proveedor) es la siguiente: Descripcion_Producto=”Nuevo Producto Por Definir”, Cantidad_Inventario=0, Precio_Venta=0, Precio_Costo=0, Codigo_proveedor=100
    ```sql
    SET IMPLICIT_TRANSACTIONS OFF;

    BEGIN TRANSACTION 
    CREATE PROCEDURE ReservaArticulos
    AS
    DECLARE @Ultimo Int
    DECLARE @Indice Int
    SET @Indice = 1
    SELECT @Ultimo = MAX(TB_Producto.Codigo_Producto) FROM TB_Producto
    --PRINT @Ultimo
    WHILE @Indice <= 5
    BEGIN
        SET @Ultimo =  @Ultimo +1
        --PRINT @Ultimo
        SET @Indice = @Indice + 1
        INSERT INTO TB_Producto (Codigo_Producto, Descripcion_Producto, Cantidad_Inventario, Precio_Venta, Precio_Costo, Codigo_Proveedor) VALUES (@Ultimo, 'Nuevo Producto Por Definir', 0, 0, 0, 100)   
    END

    GO
    ROLLBACK
    SELECT * FROM TB_Producto
    ```

1. Escriba el código del Procedimiento Almacenado que permita verificar la existencia de registros en las base de datos antes de insertarlo. Para ello se debe verificar los campos nombres, apellidos, correo y teléfono móvil. El resto de los campos se completan con valores por defecto al insertarse. 
    ```sql
    CREATE PROC EXISTENCIA_REGISTROS 
    @Nom VARCHAR(15),
    @Ap VARCHAR(15),
    @Tel_Movil VARCHAR(15),
    @Correo VARCHAR(50)
    AS
    DECLARE @ID INT
    DECLARE @Direc VARCHAR(15)
    DECLARE @Tel_Fijo VARCHAR(15)
    DECLARE @Cod_Carrera INT
    IF EXISTS(SELECT * FROM TB_ESTUDIANTES AS TBE WHERE (TBE.Nombre_Estudiante LIKE @Nom) AND (TBE.Apellido_Estudiante LIKE @Ap) AND (TBE.Telefono_Movil_Estudiante LIKE @Tel_Movil) AND (TBE.Correo_Estudiante LIKE @Correo))
        BEGIN
            PRINT 'Producto ya está registrado'
        END
    ELSE
        BEGIN
            SET @Tel_Fijo = 'defecto'
            SET @Cod_Carrera = 1001
            SET @Direc = 'defecto'
            SELECT @ID = (MAX(TBE.ID_Estudiante) + 1)  FROM TB_ESTUDIANTES AS TBE 
            INSERT INTO TB_ESTUDIANTES (ID_Estudiante ,Nombre_Estudiante,Apellido_Estudiante,Direccion_Estudiante ,Telefono_Fijo_Estudiante,Telefono_Movil_Estudiante ,Cod_Carrera )
            VALUES(@ID , @Nom , @Ap , @Direc , @Tel_Fijo ,@Tel_Movil , @Cod_Carrera)
            PRINT 'Insertando Valores'
        END	
    GO

    EXEC EXISTENCIA_REGISTROS 'Pedro','Gonzalez','6789-0356','jaltamira@utp.ac.pa'
    ```

1. Escriba el código del Procedimiento Almacenado que permita listar a través de un cursor cada uno de los cursos registrados presentando los la siguiente información: identificador de estudiante, nombre completo del estudiante y la calificación obtenida. 
    ```sql
    CREATE PROC Proc_Estudiantes_Cursos
    AS
    DECLARE @IdEstudiante Int
    DECLARE @NombreEstudiante Varchar(20)
    DECLARE @ApellidoEstudiante Varchar(20)
    DECLARE @Calificacion Int
    DECLARE @IdCurso Int
    DECLARE @IndiceCurso Int
    DECLARE @Aux Int

    DECLARE Proc_Lista_Curso CURSOR SCROLL GLOBAL
        FOR SELECT TBE.ID_Estudiante, TBE.Nombre_Estudiante,TBE.Apellido_Estudiante, TBCE.Calificacion_Curso, TBCE.ID_Curso 
            FROM TB_ESTUDIANTES AS TBE INNER JOIN TB_CURSO_ESTUDIANTE AS TBCE ON TBE.ID_Estudiante = TBCE.ID_Estudiante 
            ORDER BY TBCE.ID_Curso ASC

    DECLARE Proc_Cod_Cursos CURSOR SCROLL GLOBAL
        FOR SELECT TB_CURSO_ESTUDIANTE.ID_Curso
        FROM TB_CURSO_ESTUDIANTE 
        GROUP BY TB_CURSO_ESTUDIANTE.ID_Curso

    OPEN Proc_Cod_Cursos
    OPEN Proc_Lista_Curso

    FETCH FIRST FROM Proc_Cod_Cursos INTO @IndiceCurso
    FETCH FIRST FROM Proc_Lista_Curso INTO  @IdEstudiante, @NombreEstudiante, @ApellidoEstudiante, @Calificacion, @IdCurso

    WHILE (@@FETCH_STATUS = 0)
    BEGIN
    PRINT '--------------- Nuevo Curso --------------- '+ CAST(@IndiceCurso AS Varchar(10))
        WHILE (@@FETCH_STATUS = 0)
        BEGIN
            If @IdCurso = @IndiceCurso  
            BEGIN
                PRINT CAST(@IdEstudiante AS Varchar(10))+ ' / ' + @NombreEstudiante+ ' / ' + @ApellidoEstudiante + ' / ' + CAST(@IdCurso AS Varchar(10)) + ' / ' + CAST(@Calificacion AS Varchar(10)) 
            END
        FETCH NEXT FROM Proc_Lista_Curso INTO  @IdEstudiante, @NombreEstudiante, @ApellidoEstudiante, @Calificacion, @IdCurso
        END
    FETCH FIRST FROM Proc_Lista_Curso INTO  @IdEstudiante, @NombreEstudiante, @ApellidoEstudiante, @Calificacion, @IdCurso
    FETCH NEXT FROM Proc_Cod_Cursos INTO @IndiceCurso
    END

    CLOSE Proc_Lista_Curso
    CLOSE Proc_Cod_Cursos

    DEALLOCATE Proc_Cod_Cursos
    DEALLOCATE Proc_Lista_Curso

    GO

    EXEC Proc_Estudiantes_Cursos
    ```

1. Escriba el código del Procedimiento Almacenado que permita listar a través de un cursor la siguiente información: Nombre completo del estudiante, calificación obtenida en el curso y la letra correspondiente a la calificación. El procedimiento almacenado debe recibir como parámetro de entrada el código del curso. 
    ```sql
    CREATE PROC Proc_Cursor_Calificacion 
    @Cod_Curso Int
    AS
    DECLARE @NombreEstudiante Varchar(20)
    DECLARE @ApellidoEstudiante Varchar(20)
    DECLARE @IdCurso Int
    DECLARE @Calificacion Int
    DECLARE @LetraCalificacion Varchar(1)
    DECLARE C_Cursor_Estudiante CURSOR SCROLL GLOBAL
        FOR SELECT TBE.Nombre_Estudiante,TBE.Apellido_Estudiante,TBCE.ID_Curso, TBCE.Calificacion_Curso FROM TB_ESTUDIANTES AS TBE INNER JOIN TB_CURSO_ESTUDIANTE AS TBCE ON TBE.ID_Estudiante = TBCE.ID_Estudiante 

    OPEN C_Cursor_Estudiante

    FETCH FIRST FROM C_Cursor_Estudiante INTO @NombreEstudiante, @ApellidoEstudiante , @IdCurso, @Calificacion

    WHILE (@@FETCH_STATUS = 0 )
        BEGIN
            IF @IdCurso = @Cod_Curso 
                BEGIN
                    SET @LetraCalificacion = (CASE WHEN @Calificacion >= 91 THEN 'A'
                    WHEN @Calificacion <= 91 AND @Calificacion >= 81 THEN 'B'
                    WHEN @Calificacion <= 81 AND @Calificacion >= 71 THEN 'C'
                    WHEN @Calificacion <= 71 AND @Calificacion >= 61 THEN 'D'
                    ELSE 'F'
                    END)
                    PRINT @NombreEstudiante+' '+@ApellidoEstudiante+ ' / ' + CAST(@IdCurso AS VARCHAR(6)) +' / ' +CAST(@Calificacion AS VARCHAR(6))+' / ' + 'Nota del estudiante:'+ @LetraCalificacion
                END
        FETCH NEXT FROM C_Cursor_Estudiante INTO @NombreEstudiante, @ApellidoEstudiante, @IdCurso, @Calificacion
        END

    CLOSE C_Cursor_Estudiante
    DEALLOCATE C_Cursor_Estudiante
    GO

    EXEC Proc_Cursor_Calificacion 7020
    ```

1. Escribir el código SQL de un procedimiento almacenado que permita verificar el inventario disponible de productos. Se debe etiquetar la salida dependiendo del Stock de la siguiente manera: 'Solicitar' si está por debajo, 'Suficiente' si está por arriba del stock y al 'Limite' si es igual al stock. El procedimiento almacenado recibe como parámetro de entrada el stock de referencia.
    ```sql
    CREATE PROC Proc_Inventario
    @referencia Int
    AS
    SELECT TBP.Codigo_Producto, TBP.Descripcion_Producto, TBP.Cantidad_Inventario,
    CASE WHEN TBP.Cantidad_Inventario > @referencia THEN 'Suficiente'
    WHEN TBP.Cantidad_Inventario = @referencia THEN 'Limite'
    WHEN TBP.Cantidad_Inventario < @referencia THEN 'Solicitar'
    END AS 'Estatus'
    FROM TB_Producto AS TBP
    GO

    EXEC Proc_Inventario 30
    ```

1. Escribir el código SQL de un procedimiento almacenado que permita catalogar los vendedores en '5 Estrellas' o 'Regulares' dependiendo de la meta establecida de venta. El procedimiento almacenado recibe como parámetro de entrada la meta de referencia.
    ```sql
    CREATE PROC Proc_Catalogar_Proveedores
    @referencia Int
    AS
    SELECT TBP.Nombre_Proveedor, TBP.PrimerApellido_Proveedor, SUM(TBFC.Monto_Total) AS 'MONTO',
    CASE WHEN SUM(TBFC.Monto_Total) > @referencia THEN '5 Estrellas'
    WHEN SUM(TBFC.Monto_Total) < @referencia THEN 'Regular'
    END AS 'CATEGORIA'
    FROM TB_Proveedor AS TBP INNER JOIN TB_Factura_Compra AS TBFC ON TBP.Codigo_Proveedor = TBFC.Codigo_Proveedor
    GROUP BY TBP.Nombre_Proveedor, TBP.PrimerApellido_Proveedor
    GO

    EXEC Proc_Catalogar_Proveedores 10000
    ```

1. Recorrer el Cursor con la consulta estudiantes imprimiendo los datos generales de los estudiantes.
    ```sql
    DECLARE @NombreEstudiante Varchar(20)
    DECLARE @ApellidoEstudiante Varchar(20)
    DECLARE @DireccionEstudiante Varchar(50)
    --DECLARE @CorreoEstudiante Varchar(20)

    DECLARE C_Estudiantes_Consulta CURSOR SCROLL GLOBAL
    FOR SELECT TBE.Nombre_Estudiante, TBE.Apellido_Estudiante, TBE.Direccion_Estudiante
        FROM TB_ESTUDIANTES AS TBE

    OPEN C_Estudiantes_Consulta

    FETCH FIRST FROM C_Estudiantes_Consulta INTO @NombreEstudiante, @ApellidoEstudiante, @DireccionEstudiante

    WHILE (@@FETCH_STATUS = 0)
    BEGIN
        PRINT @NombreEstudiante + ' / ' + @ApellidoEstudiante+ ' / '+@DireccionEstudiante
        FETCH NEXT FROM C_Estudiantes_Consulta INTO @NombreEstudiante, @ApellidoEstudiante, @DireccionEstudiante
    END
    GO

    CLOSE C_Estudiantes_Consulta

    DEALLOCATE C_Estudiantes_Consulta
    ```

1. Creación de un Cursor para mover registros de una tabla a otra. Se debe crear una tabla temporal con los siguientes campos ID_Estudiante, Nombre_Estudiante, Apellido_Estudiante, Correo_Estudiante, Cod_Carrera. Posteriormente se debe crear un cursor que permita mover los registros de los estudiantes de la Tabla ESTUDIANTES a la nueva tabla temporal, verificando que los registros no se repitan. 
    ```sql
    CREATE TABLE #TB_Temporal
    (ID_Estudiante INT, 
    Nombre_Estudiante Varchar(20), 
    Apellido_Estudiante Varchar(20),  
    Cod_Carrera Int
    )

    --DROP TABLE #TB_Temporal 

    DECLARE @IdEstudiante Int
    DECLARE @NombreEstudiante Varchar(20)
    DECLARE @ApellidoEstudiante Varchar(20)
    DECLARE @CodCarrera Int


    DECLARE C_Cursor_Tabla CURSOR SCROLL GLOBAL
    FOR SELECT TBE.ID_Estudiante, TBE.Nombre_Estudiante,TBE.Apellido_Estudiante,TBE.Cod_Carrera 
        FROM TB_ESTUDIANTES AS TBE

    DECLARE @TempIdEstudiante Int
    DECLARE @Band Int

    DECLARE C_Cursor_TB_Temporal CURSOR SCROLL GLOBAL
    FOR SELECT TBT.ID_Estudiante FROM #TB_Temporal AS TBT 

    OPEN C_Cursor_Tabla
    FETCH FIRST FROM C_Cursor_Tabla INTO @IdEstudiante, @NombreEstudiante, @ApellidoEstudiante, @CodCarrera
    INSERT INTO #TB_Temporal (ID_Estudiante,Nombre_Estudiante, Apellido_Estudiante, Cod_Carrera) VALUES (@IdEstudiante, @NombreEstudiante, @ApellidoEstudiante, @CodCarrera)
    FETCH NEXT FROM C_Cursor_Tabla INTO @IdEstudiante, @NombreEstudiante, @ApellidoEstudiante, @CodCarrera

    OPEN C_Cursor_TB_Temporal
    FETCH FIRST FROM C_Cursor_TB_Temporal INTO @TempIdEstudiante 
    
    --INSERT INTO #TB_Temporal (ID_Estudiante,Nombre_Estudiante, Apellido_Estudiante, Cod_Carrera) VALUES (@IdEstudiante, @NombreEstudiante, @ApellidoEstudiante, @CodCarrera)
    
    WHILE( @@FETCH_STATUS = 0)
    BEGIN
    SET @Band = 0
        WHILE(@@FETCH_STATUS = 0)
        BEGIN
            IF(@TempIdEstudiante = @IdEstudiante )
            BEGIN
                PRINT 'Estudiante ya registrado'
                SET @Band = 1
                BREAK
            END
            FETCH NEXT FROM C_Cursor_TB_Temporal INTO @TempIdEstudiante 
        END

        IF (@Band = 0)
        BEGIN
            INSERT INTO #TB_Temporal (ID_Estudiante,Nombre_Estudiante, Apellido_Estudiante, Cod_Carrera) VALUES (@IdEstudiante, @NombreEstudiante, @ApellidoEstudiante, @CodCarrera)
        END
        FETCH FIRST FROM C_Cursor_TB_Temporal INTO @TempIdEstudiante 
        FETCH NEXT FROM C_Cursor_Tabla INTO @IdEstudiante, @NombreEstudiante, @ApellidoEstudiante, @CodCarrera
    END

    CLOSE C_Cursor_Tabla
    CLOSE C_Cursor_TB_Temporal

    DEALLOCATE C_Cursor_Tabla
    DEALLOCATE C_Cursor_TB_Temporal

    SELECT * FROM #TB_Temporal
    ```

1. Escribir el código SQL que ejecute un cursor. El cursor deberá imprimir registro a registro el identificador del estudiante, el identificador del curso, nombre completo del estudiante, y la letra (A, B, C, D, Reprobado para la F) correspondiente a la nota de acuerdo al sistema de calificación de la UTP para el código del curso ingresado como parámetro.
    ```sql
    ALTER PROC Proc_Nota_Estudiantes 
    @Cod_Curso Int
    AS
    DECLARE @IdEstudiante Int
    DECLARE @NombreEstudiante Varchar(20)
    DECLARE @ApellidoEstudiante Varchar(20)
    DECLARE @IdCurso Int
    DECLARE @Calificacion Int
    DECLARE @LetraCalificacion Varchar(1)
    DECLARE C_Cursor_Estudiante CURSOR SCROLL GLOBAL
        FOR SELECT TBE.ID_Estudiante, TBE.Nombre_Estudiante,TBE.Apellido_Estudiante,TBCE.ID_Curso, TBCE.Calificacion_Curso FROM TB_ESTUDIANTES AS TBE INNER JOIN TB_CURSO_ESTUDIANTE AS TBCE ON TBE.ID_Estudiante = TBCE.ID_Estudiante 

    OPEN C_Cursor_Estudiante

    FETCH FIRST FROM C_Cursor_Estudiante INTO @IdEstudiante, @NombreEstudiante, @ApellidoEstudiante , @IdCurso, @Calificacion

    WHILE (@@FETCH_STATUS = 0 )
        BEGIN
            IF @IdCurso = @Cod_Curso 
                BEGIN
                    SET @LetraCalificacion = (CASE WHEN @Calificacion >= 91 THEN 'A'
                    WHEN @Calificacion <= 91 AND @Calificacion >= 81 THEN 'B'
                    WHEN @Calificacion <= 81 AND @Calificacion >= 71 THEN 'C'
                    WHEN @Calificacion <= 71 AND @Calificacion >= 61 THEN 'D'
                    ELSE 'F'
                    END)
                    PRINT CAST(@IdEstudiante AS Varchar(10)) +' / '+ CAST(@IdCurso AS Varchar(10))+' / '+(@NombreEstudiante+ ' '+@ApellidoEstudiante)+ ' / ' + @LetraCalificacion
                END
        FETCH NEXT FROM C_Cursor_Estudiante INTO @IdEstudiante, @NombreEstudiante, @ApellidoEstudiante , @IdCurso, @Calificacion

        END

    CLOSE C_Cursor_Estudiante
    DEALLOCATE C_Cursor_Estudiante
    GO

    EXEC Proc_Nota_Estudiantes 7020
    ```

1. Función Escalar para Obtener el nombre del Estudiante a través de un valor Literal dentro de la función.
    ```sql
    CREATE FUNCTION DBO.FUNC_Nombre_Estudiante_Sin_Parametro()
    RETURNS VARCHAR(50)
    AS
    BEGIN
    DECLARE @Nombre_Estudiante Varchar (50)
    SELECT @Nombre_Estudiante = Nombre_Estudiante + ' '+ Apellido_Estudiante
    FROM TB_CURSO_ESTUDIANTE, TB_ESTUDIANTES
    WHERE TB_CURSO_ESTUDIANTE.Id_Estudiante = TB_ESTUDIANTES.ID_Estudiante
    AND TB_CURSO_ESTUDIANTE.Id_Estudiante  = 9001
    RETURN @Nombre_Estudiante

    END
    GO
    --Imprmir el Resultado de la Función
    PRINT 'El Nombre del Estudiante es: ' + DBO.FUNC_Nombre_Estudiante_Sin_Parametro()
    ```

1. Modificar la función con el comando ALTER
    ```sql
    ALTER FUNCTION DBO.FUNC_Nombre_Estudiante_Sin_Parametro()
    RETURNS VARCHAR(50)
    AS
    BEGIN
    DECLARE @Nombre_Estudiante Varchar (25)
    DECLARE @Apellido_Estudiante Varchar(25)
    SELECT @Nombre_Estudiante = Nombre_Estudiante, @Apellido_Estudiante=Apellido_Estudiante
    FROM TB_CURSO_ESTUDIANTE, TB_ESTUDIANTES
    WHERE TB_CURSO_ESTUDIANTE.Id_Estudiante = TB_ESTUDIANTES.ID_Estudiante
    AND TB_CURSO_ESTUDIANTE.Id_Estudiante  = 9001
    RETURN @Nombre_Estudiante + ' ' + @Apellido_Estudiante
    END
    GO
    ```

1. Eliminar la Función Nombre-de-la-Función
    ```sql
    DROP FUNCTION DBO.FUNC_Nombre_Estudiante_Sin_Parametro
    GO
    ```

1. Función Escalar para Obtener el Nombre Completo del Estudiante ingresando como parámetro de la función el código del estudiante.
    ```sql
    CREATE FUNCTION FUNC_Nombre_Estudiante_Con_Parametro
    ( @Id_Estudiante Int )
    RETURNS VARCHAR (50)
    AS
    BEGIN
    DECLARE @Nombre_Estudiante Varchar (50)
    SELECT @Nombre_Estudiante = Nombre_Estudiante + ' '+ Apellido_Estudiante
    FROM TB_CURSO_ESTUDIANTE, TB_ESTUDIANTES
    WHERE TB_CURSO_ESTUDIANTE.Id_Estudiante = TB_ESTUDIANTES.ID_Estudiante
    AND TB_CURSO_ESTUDIANTE.Id_Estudiante  = @Id_Estudiante
    RETURN @Nombre_Estudiante
    END
    GO
    --Ejecutar la Función
    PRINT 'El Nombre del Estudiane es: '+ DBO.FUNC_Nombre_Estudiante_Con_Parametro(9001)
    GO
    ```

1. Función en Línea para obtener lista de estudiantes matriculados en todos los cursos.
    ```sql
    CREATE FUNCTION FUNC_Lista_Estudiantes_Matriculados_Sin_Parametro()
    RETURNS TABLE
    AS
    RETURN (SELECT DISTINCT (Nombre_Estudiante + ' '+ Apellido_Estudiante) AS ESTUDIANTE
    FROM TB_CURSO_ESTUDIANTE, TB_ESTUDIANTES
    WHERE TB_CURSO_ESTUDIANTE.Id_Estudiante = TB_ESTUDIANTES.ID_Estudiante)
    GO
    --Ejecutar función
    SELECT * FROM DBO.FUNC_Lista_Estudiantes_Matriculados_Sin_Parametro()
    GO
    ```

1. Función Con Valores de Tabla de Múltiples Instrucciones.
Problema: Consultar la cantidad de estudiantes y cursos disponibles para una carrera pasada como parámetro a la función.
    ```sql
    CREATE FUNCTION FUNC_Multiple_Lista_Estudiantes_Matriculados_Carrera_Con_Parametro(@Carrera Int)
    RETURNS @Tabla TABLE(Id_Carrera Int, Nombre_Carrera Varchar(50), Cantidad_Estudiantes Int,
    Cantidad_Cursos Int )
    AS
    BEGIN 
    INSERT INTO @Tabla SELECT  C.Cod_Carrera,  C.Nombre_Carrera, COUNT(DISTINCT(CE.ID_ESTUDIANTE)), COUNT(DISTINCT(CU.Cod_Asignatura)) FROM TB_CARRERAS C INNER JOIN TB_ESTUDIANTES E ON C.Cod_Carrera = E.Cod_Carrera JOIN TB_ASIGNATURA A ON C.Cod_Carrera = A.Cod_Carrera 
    JOIN TB_CURSOS CU ON CU.Cod_Asignatura = A.Cod_Asignatura JOIN TB_CURSO_ESTUDIANTE CE ON CE.ID_Curso =CU.ID_Curso WHERE C.Cod_Carrera = @Carrera GROUP BY C.Cod_Carrera,  C.Nombre_Carrera
    RETURN
    END
    GO
    ```

1. Realice una Función que permita devolver el promedio de las Ventas.
    ```sql
    ALTER FUNCTION Func_Prom_Ventas()
    RETURNS FLOAT
    AS
    BEGIN
    DECLARE @PromedioVentas FLOAT
    SELECT @PromedioVentas = AVG(TBFV.Monto_Total) FROM TB_Factura_Venta AS TBFV
    RETURN @PromedioVentas
    END

    PRINT 'El promedio de ventas es: ' + CAST(DBO.Func_Prom_Ventas() AS VARCHAR(10))
    ```

1. Realice una Función que permita obtener La Factura más alta de Venta.
    ```sql
    ALTER FUNCTION Func_Factura_Alta()
    RETURNS INT
    AS
    BEGIN
    DECLARE @FacturaAlta INT
    DECLARE @MontoTotal FLOAT

    SELECT @MontoTotal = MAX(TBFV.Monto_Total) 
    FROM TB_Factura_Venta AS TBFV

    SELECT @FacturaAlta = TBFV.Codigo_Factura 
    FROM TB_Factura_Venta AS TBFV
    WHERE TBFV.Monto_Total = @MontoTotal

    RETURN @FacturaAlta
    END

    PRINT 'La factura mas alta es: ' + CAST(DBO.Func_Factura_Alta() AS VARCHAR(10))
    ```

1. Realice una Función que permita devolver el cliente con el monto total de factura más alto
    ```sql
    CREATE FUNCTION F_Cliente_Mayor_Monto()
    RETURNS VARCHAR(150)
    AS
    BEGIN
    DECLARE @CodCliente Int
    DECLARE @NombreCliente Varchar(15)
    DECLARE @ApellidoCLiente Varchar(15)
    DECLARE @MontoTotal Float
    DECLARE @Aux Float
    DECLARE @AuxCliente Int
    DECLARE @Retorno Varchar(100)

    DECLARE C_Cliente_Maximo CURSOR SCROLL LOCAL
    FOR SELECT TBC.Codigo_Cliente, TBC.Nombre_Cliente, TBC.PrimerApellido_Cliente,  SUM(TBFV.Monto_Total) AS 'Monto total de todas las facturas'
        FROM TB_Cliente AS TBC INNER JOIN TB_Factura_Venta AS TBFV ON TBC.Codigo_Cliente = TBFV.Codigo_Cliente
        GROUP BY TBC.Codigo_Cliente, TBC.Nombre_Cliente, TBC.PrimerApellido_Cliente

    OPEN C_Cliente_Maximo

    FETCH FIRST FROM C_Cliente_Maximo INTO @CodCliente, @NombreCliente, @ApellidoCliente, @MontoTotal
    SET @Aux = @MontoTotal 

    WHILE(@@FETCH_STATUS = 0)
    BEGIN
        If(@MontoTotal > @Aux )
        BEGIN
            SET @Aux = @MontoTotal 
            SET @AuxCliente = @CodCliente 
        END
    FETCH NEXT FROM C_Cliente_Maximo INTO @CodCliente, @NombreCliente, @ApellidoCliente, @MontoTotal
    END

    FETCH FIRST FROM C_Cliente_Maximo INTO @CodCliente, @NombreCliente, @ApellidoCliente, @MontoTotal
    WHILE (@@FETCH_STATUS = 0)
    BEGIN
        If(@CodCliente = @AuxCliente )
        BEGIN
            SET @Retorno = 'El cliente '+ (@NombreCliente+' '+@ApellidoCliente)+' cuenta con el monto total de facturas  '+ CAST(@MontoTotal AS Varchar(10))+' dolares'
        BREAK
        END
    FETCH NEXT FROM C_Cliente_Maximo INTO @CodCliente, @NombreCliente, @ApellidoCliente, @MontoTotal
    END

    CLOSE C_Cliente_Maximo
    DEALLOCATE C_Cliente_Maximo
    RETURN @Retorno

    END

    PRINT DBO.F_Cliente_Mayor_Monto()
    ```

1. Escribir una Función SQL que permita obtener datos de la Factura como Descripción del Producto, precio de costo, precio de venta. El identificador de la Factura es pasado como parámetro a la Función. 
    ```sql
    ALTER FUNCTION Func_Factura(@CodFactura Int)
    RETURNS @Tabla TABLE(Descripcion_Producto Varchar(50),
                        Precio_Venta Money,
                        Precio_Costo Money
                        )
    AS
    BEGIN
    INSERT INTO @Tabla 
    SELECT TBP.Descripcion_Producto, TBP.Precio_Venta, TBP.Precio_Costo 
    FROM TB_Producto AS TBP INNER JOIN TB_Detalle_Factura_Venta AS TBDFV ON TBP.Codigo_Producto = TBDFV.Codigo_Producto 
    WHERE TBDFV.Codigo_Factura = @CodFactura
    RETURN
    END
    GO

    SELECT * FROM DBO.Func_Factura(1003)
    ```

1. Escribir el código SQL de la función que  permita verificar el inventario disponible. Dado un valor de inventario pasado como parámetro a la función, listar el código del producto, la descripción, cantidad de inventario y el estatus que puede ser: 'solicitar' si está por debajo del inventario, 'Suficiente' si está por arriba del inventario y al 'limite' si es igual al inventario.
    ```sql
    CREATE FUNCTION Inventario_Disponible(@referencia Int)
    RETURNS TABLE
    AS
    RETURN (SELECT TBP.Codigo_Producto, TBP.Descripcion_Producto, TBP.Cantidad_Inventario,
    CASE WHEN TBP.Cantidad_Inventario > @referencia THEN 'Suficiente'
    WHEN TBP.Cantidad_Inventario = @referencia THEN 'Limite'
    WHEN TBP.Cantidad_Inventario < @referencia THEN 'Solicitar'
    END AS 'Estatus'
    FROM TB_Producto AS TBP)
    GO

    SELECT * FROM Inventario_Disponible(60)
    ```

1. Explique qué hace el siguiente código del Disparadores. 
    ```sql
    CREATE TABLE TB_HORARIO
    (
        Cod_Horario int not null primary key,
        Descripcion_horario varchar (50) not null,
    )
    GO
    --Creación del Trigger
    CREATE TRIGGER TR_SEGURIDAD_BD
        ON DATABASE FOR DROP_TABLE, ALTER_TABLE

        AS
        BEGIN
    RAISERROR ('No está permitido borrar ni modificar tablas!', 16, 1)
            ROLLBACK TRANSACTION
    END
    GO
    --Eliminando el Disparador
    DROP TABLE TB_HORARIO
    GO
    ```

1. Explique qué hace el siguiente código del Disparadores. 
    ```sql
    CREATE TRIGGER TR_Insertar_Nuevo_Registro_Facultad
    ON TB_FACULTAD 
    FOR INSERT
    AS
    PRINT 'Se ha adicionado nuevo Registro en la Tabla Facultad.'
    GO

    --Probando el Trigger. Insertando nuevo registro.
    INSERT INTO TB_FACULTAD (Cod_Facultad, Nombre_Facultad) 
    VALUES (115, 'Facultad de Ingeniería en Sistemas Computacionales')
    GO

    ```

1. Explique qué hace el siguiente código del Disparadores. 
    ```sql
    CREATE TABLE DB_INSERCION_REGISTRO
    (
    IdRegistro INT NOT NULL IDENTITY(1,1) PRIMARY KEY,
    Fecha_Hora DATETIME NOT NULL DEFAULT (GETDATE()),
    Usuario VARCHAR(60) NOT NULL DEFAULT (USER_NAME()),
    Accion VARCHAR(50) NOT NULL,
    Descripcion VARCHAR(500) NOT NULL
    )
    GO

    INSERT INTO DB_INSERCION_REGISTRO(Accion, Descripcion)
    VALUES('Prueba de Almacenamiento', 'Insertar')
    GO

    SELECT * FROM DB_INSERCION_REGISTRO
    GO
    ```

1. Explique qué hace el siguiente código del Disparadores
    ```sql
    CREATE TRIGGER Tr_Insercion_Facultad
        ON TB_FACULTAD
        AFTER INSERT
        AS
            BEGIN
                DECLARE @nombre_facultad VARCHAR(60)
                SELECT @nombre_facultad = TB_FACULTAD.Nombre_Facultad 
                FROM INSERTED TB_FACULTAD
    INSERT INTO DB_INSERCION_REGISTRO (Accion, Descripcion)
                    VALUES ('Inserción de datos',
    'Se ha insertado un nuevo registro en la tabla facultad con el nombre: ' + @nombre_facultad)
            END
    GO


    -- Insertando nuevos registros
    INSERT INTO TB_FACULTAD (Cod_Facultad, Nombre_Facultad) 
    VALUES (145, 'Facultad de Astronomia')

    ```

1. Escriba el código SQL de un disparador que permita bloquear la eliminación de objetos de la Base de Datos DB_EmpresaXYZ, deshaciendo la transacción. 
    ```sql
    CREATE TRIGGER TR_SEGURIDAD_BD
    ON DATABASE FOR DROP_TABLE, ALTER_TABLE
    AS
    BEGIN
        RAISERROR ('No esta permitido borrar ni modificar tablas!',16,1)
        --Comando para mandar mensajes de error
        ROLLBACK TRANSACTION 
    END
    GO
    Create Table TB_Proveedor1
    (
    Codigo_Proveedor INT NOT NULL,
    Nombre_Proveedor VARCHAR (20) NOT NULL,
    PrimerApellido_Proveedor VARCHAR (20) NOT NULL,
    SegundoApellido_Proveedor VARCHAR (20),
    TelefonoFijo_Proveedor VARCHAR (8),
    TelefonoMovil_Proveedor VARCHAR (9),
    Direccion_Proveedor VARCHAR (50),
    Email_Proveedor VARCHAR (30),
    )
    GO
    DROP TABLE TB_Proveedor1

    ```

1. Escriba el código SQL de un disparador que envié un mensaje inmediatamente cuando se realiza el registro de un nuevo proveedor, imprimiendo el mensaje: “Se ha adicionado nuevo Registro en la Tabla PROVEEDOR”
    ```sql
    CREATE TRIGGER TR_Insertar_Nuevo_Registro_Proveedor
    ON TB_Proveedor1
    FOR INSERT
    AS
        PRINT 'Se ha adicionado nuevo registro en la tabla proveedor'
    GO

    --Probando Trigeer
    INSERT INTO TB_Proveedor1 (Codigo_Proveedor, Nombre_Proveedor, PrimerApellido_Proveedor, SegundoApellido_Proveedor, TelefonoFijo_Proveedor, TelefonoMovil_Proveedor, Direccion_Proveedor, Email_Proveedor) VALUES (104, 'Mirta', 'Figueroa', 'Gutierrez', '236-1515', '6031-8567', 'Panama', 'mirtaFigu10@yahoo.es')
    GO

    ```

1. Escriba el código SQL de un disparador que realicé un log en una tabla, creada previamente con los campos: identificador de registro (incremento automático), fecha/hora, usuario activo,  acción realizada (inserción) y descripción con el dato del nuevo registro, una vez se realicé el registro de un nuevo producto. 
    ```sql
    CREATE TABLE DB_Log_Usuario_Producto
    (
    IdRegistro INT NOT NULL IDENTITY(1,1) PRIMARY KEY,
    Fecha_Hora DATETIME NOT NULL DEFAULT (GETDATE()),
    Usuario VARCHAR(60) NOT NULL DEFAULT (USER_NAME()),
    Accion VARCHAR(50) NOT NULL,
    Descripcion VARCHAR(500) NOT NULL
    )
    GO

    CREATE TRIGGER Tr_Insercion_Producto
    ON TB_Producto
    AFTER INSERT
    AS
        BEGIN
            DECLARE @nombre_producto VARCHAR(60)
            SELECT @nombre_producto = TB_PRODUCTO.Descripcion_Producto 
            FROM INSERTED TB_Producto 
            INSERT INTO DB_Log_Usuario_Producto(Accion, Descripcion)
                VALUES('Inserccion de datos',
                        'Se ha insetado un nuevo registro en la tabla PRODUCTO con el nombre: ' + @nombre_producto )
            END
    GO

    INSERT INTO TB_Producto (Codigo_Producto, Descripcion_Producto, Cantidad_Inventario, Precio_Venta, Precio_Costo, Codigo_Proveedor) VALUES (000101, 'Disco Duro', 75, 60.05, 51.90, 103)   
    GO
    SELECT * FROM DB_Log_Usuario_Producto
    ```

1. Escriba el código SQL que permita darle mantenimiento a la base de datos. A través de un procedimiento almacenado se debe eliminar un curso de la base de datos y al mismo tiempo, a través de un evento de un disparador, eliminar las calificaciones correspondientes de ese curso. Se debe pasar como parámetro de entrada, del procedimiento almacenado, el código del curso a eliminar.
    ```sql
    CREATE PROC P_BORRAR_CURSO
    @CodCurso INT
    AS
    DELETE FROM TB_CURSOS WHERE TB_CURSOS.ID_Curso = @CodCurso

    EXEC P_BORRAR_CURSO 7020

    CREATE TRIGGER TR_ELIMINANDO_CALIFICACIONES
    ON TB_CURSOS
    INSTEAD OF DELETE
    AS
    BEGIN
    DECLARE @Cod_Curso INT
    SELECT @Cod_Curso = ID_Curso 
    FROM deleted
    DELETE FROM TB_CURSO_ESTUDIANTE WHERE TB_CURSO_ESTUDIANTE.ID_Curso = @Cod_Curso
    END


    SELECT * FROM TB_CURSOS
    SELECT * FROM TB_CURSO_ESTUDIANTE

    ```

1. Escriba el código de un Disparador que permita una vez actualizado el nombre de la carrera, actualizar todos los correos de los estudiantes afiliados a la carrera actualizada. El Correo Electrónico debe quedar con el nuevo nombre de la carrera más el servidor '@utp.ac.pa'.
    ```sql
    CREATE TRIGGER TR_ACTUALIZANDO_CORREOS
    ON TB_CARRERAS
    AFTER UPDATE
    AS
    DECLARE @Codigo_Carrera INT
    DECLARE @Nombre_Carrera VARCHAR(100)
    SELECT @Codigo_Carrera = TB_CARRERAS.Cod_Carrera FROM inserted TB_CARRERAS
    SELECT @Nombre_Carrera = TB_CARRERAS.Nombre_Carrera FROM inserted TB_CARRERAS
    UPDATE TB_ESTUDIANTES SET Correo_Estudiante = @Nombre_Carrera + '@utp.ac.pa'
    WHERE TB_ESTUDIANTES.Cod_Carrera = @Codigo_Carrera


    UPDATE TB_CARRERAS SET Nombre_Carrera = 'IA' WHERE Cod_Carrera = 1001


    SELECT * FROM TB_CARRERAS
    SELECT * FROM TB_ESTUDIANTES

    ```

1. Escriba el código que permita actualizar las calificaciones de los estudiantes matriculados en un curso a través de un evento de un disparador, una vez que se actualicen todos los registros de un curso para un docente en un año y semestre, a través de un procedimiento almacenado. Dentro del disparador se debe actualizar todas las calificaciones de los estudiantes matriculados para dicho curso, con una nota equivalente a cero. Se deben pasar como parámetros de entrada del procedimiento almacenado: El año a corregir, el nuevo año, el código del docente y el semestre.
    ```sql
    CREATE TRIGGER TR_ACTUALIZAR_DOCENTES 
    ON TB_CURSOS 
    AFTER UPDATE
    AS
    BEGIN
    PRINT 'REGISTROS DEL CURSO PARA DOCENTE ACTUALIZADOS!!' 
    DECLARE @CURSO INT
    SELECT @CURSO = TB_CURSOS.ID_Curso 
    FROM deleted TB_CURSOS

    --SET NOCOUNT ON;
    PRINT CAST(@CURSO AS VARCHAR(10))
    UPDATE TB_CURSO_ESTUDIANTE SET Calificacion_Curso = 0 WHERE ID_Curso = @CURSO
    END
    GO

    CREATE PROC P_ACTUALIZAR_CURSO_DOCENTE
    @AÑO_V INT,
    @AÑO_N INT,
    @DOCENTE INT,
    @SEMESTRE VARCHAR(2),
    @IDMateria INT
    AS
    UPDATE TB_CURSOS SET Semestre_Curso = @SEMESTRE, Año_Curso = @AÑO_N, Cod_Profesor = @DOCENTE, Cod_Asignatura = @IDMateria  WHERE Año_Curso = @AÑO_V AND Cod_Profesor = @DOCENTE AND Cod_Asignatura = @IDMateria
    GO

    EXEC P_ACTUALIZAR_CURSO_DOCENTE 2014, 2017, 3001, 'II',2003

    SELECT *FROM TB_CURSOS

    SELECT *FROM TB_CURSO_ESTUDIANTE

    ```

1. Escribir el código SQL que permita verificar si existe el registro de un docente con los datos de entrada. Si el registro existe con el nombre y el apellido, se genere un error indicando que ya existe un registro del docente utilizando la instrucción RAISERROR
    ```sql
    DECLARE @Nombre VARCHAR(15)
    DECLARE @Apellido VARCHAR(15)

    SET @Nombre = 'Carlos'
    SET @Apellido = 'Herrera'

    IF EXISTS(SELECT Nombre_Profesor, Apellido_Profesor FROM TB_PROFESOR WHERE (Nombre_Profesor LIKE @Nombre) AND (Apellido_Profesor LIKE @Apellido))
        BEGIN
        RAISERROR('Ya existe un registro de profesor con estos datos!' ,16,1)
        END

    ```

1. Escriba el código SQL para lanzar una advertencia cuando un curso especificado no tiene cupos disponibles según una cantidad establecida. Cuando la cantidad es por debajo del umbral igual se indica con un mensaje que hay cupos disponibles. 
    ```sql
    CREATE PROC Cupos_Disponibles
    @CodCurso VARCHAR(15),
    @Umbral INT
    AS
    DECLARE @Cant INT
    SELECT @Cant = COUNT(TBCE.ID_ESTUDIANTE)
    FROM TB_CURSOS AS TBC INNER JOIN TB_CURSO_ESTUDIANTE AS TBCE ON TBC.ID_Curso = TBCE.ID_Curso
    WHERE TBC.ID_Curso = @CodCurso

    IF @Cant < @Umbral
        RAISERROR('Cantidad de cupos por debajo del umbral!',9,1)
    ELSE
        RAISERROR ('Cantidad de cupos por encima del umbral!',16,1)

    EXEC Cupos_Disponibles '7020', 2

    ```

1. Escribir el código de la Vista para consultar el código del proveedor, nombre del Proveedor, primer apellido, datos de contacto de los proveedores, descripción del producto, precio de costo cuya localización de proveedores sea en Chitre y  Panamá y vendan productos cuyo precio de costo sea superior a 50 balboas. Ordenar los resultados por el campo Precio de Costo. 
    ```sql
    CREATE VIEW V_PROVEEDORES_PRODUCTOS
    AS
    SELECT TBP.Codigo_Proveedor, TBP.Nombre_Proveedor, TBP.PrimerApellido_Proveedor, (TBP.TelefonoFijo_Proveedor+' / '+TBP.TelefonoMovil_Proveedor) AS 'Datos de contacto',TBP.Direccion_Proveedor, TBPRO.Codigo_Producto, TBPRO.Descripcion_Producto, TBPRO.Precio_Costo
    FROM TB_Proveedor AS TBP INNER JOIN TB_Producto AS TBPRO ON TBP.Codigo_Proveedor = TBPRO.Codigo_Proveedor
    WHERE TBP.Direccion_Proveedor LIKE 'Chitre' OR TBP.Direccion_Proveedor LIKE 'Panama' AND TBPRO.Precio_Costo > 50
    GROUP BY TBP.Codigo_Proveedor, TBP.Nombre_Proveedor, TBP.PrimerApellido_Proveedor,(TBP.TelefonoFijo_Proveedor+' / '+TBP.TelefonoMovil_Proveedor), TBP.Direccion_Proveedor, TBPRO.Codigo_Producto, TBPRO.Descripcion_Producto, TBPRO.Precio_Costo
    GO

    SELECT * FROM V_PROVEEDORES_PRODUCTOS AS VPPRO
    ORDER BY VPPRO.Precio_Costo DESC
    ```

1. Escribir el código SQL de la Vista para consultar datos del cliente (código, nombre, apellido, teléfono móvil, correo electrónico, dirección) cuyo nombre están registrados en la base de datos iniciando con la letra "J" y cuya dirección de residencia sea Santiago.
    ```sql
    CREATE VIEW V_CLIENTE_J
    AS
    SELECT TBC.Codigo_Cliente, TBC.Nombre_Cliente, TBC.PrimerApellido_Cliente, TBC.TelefonoMovil_Cliente, TBC.Email_Cliente, TBC.Direccion_Cliente
    FROM TB_Cliente AS TBC
    WHERE SUBSTRING(Nombre_Cliente,1,1) = 'J' AND Direccion_Cliente LIKE 'Santiago'
    GO

    SELECT * FROM V_CLIENTE_J
    ```

1. Escribir el código SQL  para crear una vista que permita Totalizar las Compras de todos los Clientes. Mostrar en un solo campo el nombre y apellido del Cliente y el monto total. 
    ```sql
    CREATE VIEW V_MONTO_CLIENTE
    AS
    SELECT (TBC.Nombre_Cliente+' '+TBC.PrimerApellido_Cliente) AS 'Datos del Cliente', SUM(TBFV.Monto_Total) AS 'Monto Total'
    FROM TB_Cliente AS TBC INNER JOIN TB_Factura_Venta AS TBFV ON TBC.Codigo_Cliente = TBFV.Codigo_Cliente
    GROUP BY (TBC.Nombre_Cliente+' '+TBC.PrimerApellido_Cliente)
    GO

    SELECT * FROM V_MONTO_CLIENTE

    ```

1. Escribir el código SQL  para crear una vista que permita Consultar el monto total de los pagos realizados a cada uno de los proveedores mostrando solo aquellos cuyo monto total sea mayor 5,000. Se debe mostrar en la consulta nombre del proveedor, monto total. 
    ```sql
    CREATE VIEW V_MONTO_PROVEDORES
    AS
    SELECT TBP.Nombre_Proveedor, TBFC.Monto_Total AS 'Monto total'
    FROM TB_Proveedor AS TBP INNER JOIN TB_Factura_Compra AS TBFC ON TBP.Codigo_Proveedor = TBFC.Codigo_Proveedor
    WHERE TBFC.Monto_Total > 5000

    SELECT * FROM V_MONTO_PROVEDORES

    ```

1. Escribir el código SQL  para crear una vista que permita modificar la dirección de los proveedores localizados en Santiago a Bocas del Toro.
    ```sql
    CREATE VIEW V_DIRECCION_BOCAS
    AS
    SELECT TBP.Nombre_Proveedor, TBP.Direccion_Proveedor
    FROM TB_Proveedor AS TBP
    GO

    UPDATE V_DIRECCION_BOCAS SET Direccion_Proveedor = 'Bocas del Toro' 
    WHERE Direccion_Proveedor LIKE 'Santiago'
    ```

1. Escribir el código SQL  para crear una vista que permita eliminar todos aquellos clientes cuyo saldo sea cero.
    ```sql
    CREATE VIEW V_SALDO_CLIENTE
    AS
    SELECT TBC.Nombre_Cliente, TBC.Saldo_Cliente
    FROM TB_Cliente AS TBC
    GO

    DELETE FROM V_SALDO_CLIENTE
    WHERE Saldo_Cliente = 0
    ```

1. Escriba el código SQL de una Subconsulta que permita eliminar todos los estudiantes de la Tabla Estudiantes que no tengan Cursos Matriculados (TB_CURSO_ESTUDIANTE)
    ```sql
    SELECT COUNT(TBE.ID_Estudiante) AS 'Cantidad de estudiante antes' FROM TB_ESTUDIANTES AS TBE

    DELETE FROM TB_ESTUDIANTES 
    WHERE NOT EXISTS (SELECT TB_CURSO_ESTUDIANTE.Calificacion_Curso FROM TB_CURSO_ESTUDIANTE WHERE TB_ESTUDIANTES.ID_Estudiante = TB_CURSO_ESTUDIANTE.ID_Estudiante)

    SELECT COUNT(TBE.ID_Estudiante) AS 'Cantidad de estudiante ahora' FROM TB_ESTUDIANTES AS TBE

    SELECT * FROM TB_ESTUDIANTES

    ```

1. Escriba el código SQL de una Subconsulta utilizando la cláusula EXISTS para Consultar los datos de los clientes donde se ha comprado el producto 100001
    ```sql
    SELECT * FROM TB_Cliente AS TBC
    WHERE EXISTS(SELECT TBFV.Codigo_Cliente FROM TB_Detalle_Factura_Venta AS TBDFV INNER JOIN TB_Factura_Venta AS TBFV ON TBDFV.Codigo_Factura = TBFV.Codigo_Factura AND TBC.Codigo_Cliente = TBFV.Codigo_Cliente AND TBDFV.Codigo_Producto = 100001)
    ```

1. Escriba el código SQL de una Subconsulta utilizando la cláusula IN para Consultar los datos de los clientes donde se ha comprado el conjunto de productos (100001, 100003, 100005)
    ```sql
    SELECT * FROM TB_Cliente AS TBC
    WHERE EXISTS(SELECT TBFV.Codigo_Cliente FROM TB_Detalle_Factura_Venta AS TBDFV INNER JOIN TB_Factura_Venta AS TBFV ON TBDFV.Codigo_Factura = TBFV.Codigo_Factura AND TBC.Codigo_Cliente = TBFV.Codigo_Cliente AND TBDFV.Codigo_Producto IN (100001, 100003, 100005))
    ```

1. Escriba el código SQL de una Subconsulta para obtener los datos de los proveedores que tengan productos referenciados en la tabla producto
    ```sql
    SELECT * FROM TB_Proveedor AS TBPRO
    WHERE EXISTS (SELECT TBP.Codigo_Producto FROM TB_Producto AS TBP WHERE TBPRO.Codigo_Proveedor = TBP.Codigo_Proveedor)


    SELECT * FROM TB_Proveedor

    ```

1. Escriba el código SQL de una Subconsulta que permita consultar los clientes que registran un monto total de facturas mayor o igual al porcentaje indicado del total de Ventas. La subconsulta debe estar contenida en un en un Procedimiento Almacenado y debe tener como parámetro de entrada el porcentaje a consultar. 
    ```sql
    CREATE PROC P_SubConsulta_Mayor
    @Porcentaje FLOAT
    AS
    SELECT TBC.Codigo_Cliente, TBC.Cedula_Cliente, TBC.Nombre_Cliente, TBC.PrimerApellido_Cliente FROM TB_Cliente AS TBC
    WHERE (SELECT SUM(TBFV.Monto_Total) FROM TB_Factura_Venta AS TBFV WHERE TBFV.Codigo_Cliente = TBC.Codigo_Cliente) >= ((SELECT SUM(TBFV.Monto_Total) FROM TB_Factura_Venta AS TBFV)*(@Porcentaje/100))

    EXEC P_SubConsulta_Mayor 25
    ```

## Authors



- [@RonaldJair19](https://github.com/RonaldJair19)
