# RetailPro — Análisis de ventas

## Descripción
RetailPro es un proyecto de análisis de datos orientado a explorar información comercial de una tienda tecnológica. El trabajo utiliza una base relacional de ejemplo llamada `Ventas_Tech_DB`, consultas SQL de negocio y consultas con JOIN para integrar información de ventas con sus dimensiones.

## Tecnologías y herramientas
- Microsoft SQL Server.
- SQL Server Management Studio (SSMS).
- T-SQL.
- Git y GitHub para versionado y documentación.
- Power BI como posible herramienta de análisis/visualización posterior; los archivos SQL disponibles no incluyen un archivo `.pbix`.

## Modelo de datos
Las tablas principales del script de creación son:
- `categorias`: catálogo de categorías de productos.
- `clientes`: datos básicos de clientes.
- `productos`: catálogo, categoría, precio, stock y estado del producto.
- `ventas`: operaciones, cliente, producto, cantidad, precio unitario y fecha.

En la Pre-entrega 5 se incorpora además:
- `regiones`: dimensión geográfica de ejemplo.
- `clientes.id_region`: clave foránea hacia `regiones`.

**Importante:** el script de la Pre-entrega 5 asigna regiones mediante `(id_cliente % 3) + 1`. Es una distribución artificial para practicar relaciones; no representa una clasificación geográfica real.

## Estructura de scripts
1. `ventas_tech_db.sql.txt`: crea las tablas principales, inserta datos de ejemplo y realiza consultas de validación.
2. `m4_consultas_negocio.sql`: contiene consultas de resumen ejecutivo mensual, ranking de productos, clientes recurrentes y comparación contra el promedio.
3. `m5_consultas_joins.sql`: incorpora la dimensión `regiones` y contiene consultas con INNER JOIN, LEFT JOIN e UNION ALL.

## Cómo ejecutar
1. Abrir SQL Server Management Studio y conectarse a una instancia de SQL Server.
2. Ejecutar el script de creación de la base `Ventas_Tech_DB` y seleccionar la base.
3. Ejecutar `m4_consultas_negocio.sql`.
4. Ejecutar `m5_consultas_joins.sql` para agregar la dimensión `regiones` y ejecutar las consultas de integración.

> El script inicial contiene instrucciones `DROP TABLE IF EXISTS`; si se ejecuta nuevamente, elimina las tablas indicadas antes de recrearlas. No ejecutarlo sobre una base con información que se necesite conservar.

## Consultas y análisis
- **Resumen ejecutivo mensual:** calcula facturación, cantidad de pedidos y ticket promedio.
- **Ranking de productos:** ordena los productos por facturación total.
- **Clientes recurrentes:** identifica clientes con más de un pedido.
- **Vista base con INNER JOIN:** integra ventas, clientes, productos, categorías y regiones.
- **Clientes/productos sin ventas:** utiliza LEFT JOIN e IS NULL.
- **Consolidado por canal:** utiliza UNION ALL y asigna etiquetas `Online` y `Presencial` según períodos de fecha.

## Limitaciones y validaciones
- Los INSERT incluidos son datos de ejemplo y no representan necesariamente operaciones reales.
- La consulta mensual agrupa por número de mes, sin año. Para series históricas con más de un año debe incorporarse el año al agrupamiento.
- El ranking devuelve identificadores de producto; para mostrar nombres se debe agregar un JOIN con `productos`.
- Los INNER JOIN pueden excluir ventas si faltan relaciones con regiones o categorías.
- La asignación de regiones es ilustrativa y debe reemplazarse por datos geográficos confiables antes de realizar análisis regionales.
- La consulta de consolidado por canal crea las etiquetas a partir de un corte de fecha; el esquema no contiene una columna de canal. Por lo tanto, no debe interpretarse como un registro real del canal de venta.
- Facturación no equivale a rentabilidad: para analizar márgenes se necesitan costos y otros datos comerciales.

## Autoría y uso de IA
La documentación y la revisión de consultas pueden contar con asistencia de herramientas de IA. Las sugerencias deben validarse contra el esquema, los datos y las reglas de negocio antes de utilizarlas en reportes o decisiones.
