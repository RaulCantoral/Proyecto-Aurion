# Proyecto-Aurion
1. Tema, problema y solución
Tema: Análisis de clientes morosos y su impacto en las ventas

Problema:
La empresa ha detectado que un porcentaje significativo de clientes acumula deudas o pagos atrasados, afectando el flujo de caja y la disponibilidad de capital para reinversión. No existe un sistema automatizado que identifique de manera temprana a los clientes morosos ni sus patrones de compra previos.

Solución:
Diseñar un algoritmo que permita detectar y clasificar clientes morosos, basándose en los datos de ventas y pagos registrados. Este algoritmo calculará el total adeudado por cliente y determinará si supera un umbral definido. A partir de esto, se podrán tomar decisiones sobre crédito, promociones y bloqueo temporal de ventas.

2. Dataset de referencia
Fuente: Sistema de gestión de ventas Aurelion
Archivos utilizados:

ventas.xlsx — Registra las ventas con fechas, clientes y medios de pago.
detalle_ventas.xlsx — Contiene las cantidades e importes de cada producto vendido.
productos.xlsx — Catálogo de productos, precios y categorías.
clientes.xlsx — Información de clientes (ID, nombre, correo, estado de pago).
Definición: Catálogo de productos que ofrece la tienda Aurelion para la venta, utilizado para identificar, clasificar y valorizar las transacciones comerciales.

tabla_detalles_ventas ~343 filas

Campo	Tipo	Escala
id_producto	int	Nominal
id_venta	int	Nominal
nombre_producto	str	Nominal
cantidad	int	Razón
precio_unitario	float	Razón
importe	float	Razón
tabla_productos ~100 filas

Campo	Tipo	Escala
id_producto	int	Nominal
categoria	str	Nominal
nombre_producto	str	Nominal
precio_unitario	float	Razón
tabla_ventas ~120 filas

Campo	Tipo	Escala
id_venta	int	Nominal
id_cliente	int	Nominal
fecha	datetime	Intervalo
nombre_cliente	str	Nominal
email	str	Nominal
medio_pago	str	Nominal
3. Pasos del programa
Cargar los archivos Excel (clientes.xlsx, ventas.xlsx, detalle_ventas.xlsx, productos.xlsx).
Combinar las tablas mediante los campos clave (id_cliente, id_venta, id_producto).
Calcular el total de compras realizadas y el total de pagos efectuados.
Determinar deuda:
Deuda = Total de compras - Total pagado.
Clasificar clientes:
Si deuda > 0 → “Moroso”.
Si deuda = 0 → “Al día”.
Generar un reporte que liste los clientes morosos y su monto adeudado.
Visualizar estadísticas (porcentaje de morosos, montos acumulados, etc.).
4. Pseudocódigo
INICIO  
  PARA cada cliente EN lista_clientes HACER  
    SI deuda > 0 ENTONCES  
        estado ← "Moroso"  
    SINO  
        estado ← "Al día"  
    FIN SI  

    GUARDAR (cliente.id, cliente.nombre, deuda, estado)  
  FIN PARA  

  MOSTRAR "Lista de clientes morosos"  
  EXPORTAR reporte a Excel  
FIN
5. Diagrama de Flujo
            ┌────────────────────────┐
            │         INICIO         │
            └──────────┬─────────────┘
                       │
        ┌──────────────▼───────────────┐
        │     Cargar archivos Excel    │
        └───────────────┬──────────────┘
                        │
        ┌───────────────▼──────────────┐
        │   Combinar tablas por claves │
        └───────────────┬──────────────┘
                        │
        ┌───────────────▼──────────────┐
        │ Calcular total de compras y  │
        │ total pagado por cliente     │
        └───────────────┬──────────────┘
                        │
        ┌───────────────▼──────────────┐
        │   deuda = compras - pagado   │
        └───────────────┬──────────────┘
                        │
        ┌───────────────▼──────────────┐
        │         deuda > 0 ?          │
        ├───────────────┬──────────────┤
        │       Sí      │      No      │
        ▼               ▼              ▼
┌────────────────┐     ┌────────────────┐
│ Cliente MOROSO │     │ Cliente AL DÍA │
└────────┬───────┘     └───────┬────────┘
         │                     │
         └────────────┬────────┘
                      │
      ┌───────────────▼──────────────┐
      │  Generar reporte y exportar  │
      └───────────────┬──────────────┘
                      │
        ┌─────────────▼─────────────┐
        │           FIN             │
        └───────────────────────────┘
6. Sugerencias Copilot
Visualizar deudas acumuladas por mes.
Normalización de datos
Convierte los tipos de datos correctamente (int, float, datetime).
Homogeneiza nombres de cliente ("Juan Pérez" vs "JUAN PEREZ").
Redondea valores monetarios a 2 decimales.
Cálculo de deuda con verificación
Evita errores por ventas sin pago o pagos sin venta
Generar reportes visuales con inteligencia de negocios (BI) avanzada.
Clasificación de clientes según nivel de riesgo
Condición	Estado
deuda = 0	Al día
0 < deuda < 500	Leve
500 ≤ deuda < 2000	Riesgo medio
deuda ≥ 2000	Moroso grave
