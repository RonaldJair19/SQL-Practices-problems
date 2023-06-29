# Prácticas de consultas SQL realizadas como aprendizaje de este lenguaje
Durante mi tiempo como estudiante de Ingeniería en Sistemas y Computación, adquirí conocimientos en el lenguaje SQL DML al resolver problemas mediante la ejecución de consultas en una base de datos de prueba. A continuación listo los tipos de problemas resueltos como prueba del nivel de conocimiento adquirido.


### Problema resuelto 1
Consultar todos los productos cuyo proveedores estén localizados en Santiago
```sql
SELECT Descripcion_Producto FROM TB_Producto, TB_Proveedor
WHERE Direccion_Proveedor = 'santiago' and TB_Producto.Codigo_Proveedor =
TB_Proveedor.Codigo_Proveedor
GO
```


## Authors



- [@RonaldJair19](https://github.com/RonaldJair19)
