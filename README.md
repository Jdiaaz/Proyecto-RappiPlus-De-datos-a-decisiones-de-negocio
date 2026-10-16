# RappiPlus: de datos a decisiones de negocio

Análisis de punta a punta de **RappiPlus**, el servicio de suscripción de Rappi: calidad de datos, rentabilidad, embudo de conversión, retención por cohortes, prueba A/B y dashboard en Power BI.

> Proyecto final del bootcamp de Análisis de Datos de TripleTen (datasets proporcionados por TripleTen).

## Objetivo

Evaluar el desempeño de RappiPlus para apoyar decisiones de negocio basadas en datos, respondiendo seis preguntas:

1. ¿Podemos confiar en los datos?
2. ¿El negocio es rentable?
3. ¿Dónde se pierden los usuarios?
4. ¿Los usuarios regresan?
5. ¿Los cambios en el checkout generan impacto?
6. ¿Cómo comunicar los resultados?

## Herramientas

- **Python** (pandas, SQLAlchemy, SciPy): limpieza, métricas y prueba estadística
- **SQL (PostgreSQL)**: embudo de conversión y retención por cohortes
- **Power BI**: dashboard ejecutivo y de detalle
- **Jupyter Notebook**: documentación del análisis

## Contenido del repositorio

| Archivo | Descripción |
|---|---|
| `S12 Estudiante_Proyecto_Final.ipynb` | Notebook con todo el análisis |
| `RappiPlus_Dashboard.pbix` | Dashboard de Power BI |
| `orders_clean.csv` | Pedidos limpios |
| `marketing_clean.csv` | Inversión en marketing limpia |
| `catalog_clean.csv` | Catálogo de productos |

## Resultados

### 1. Calidad de datos

Se limpiaron tres datasets (pedidos, catálogo y marketing):

- Fechas convertidas a formato correcto
- 100 pedidos duplicados eliminados
- Texto estandarizado (países, categorías con tildes inconsistentes)
- Cantidades inválidas eliminadas (negativas y valores absurdos como 10.000 o 20.000)
- Filas con nulos en columnas clave eliminadas
- Canal de marketing recuperado a partir del `id_campaña`

Resultado: de **25.100** pedidos crudos quedaron **24.610** pedidos limpios.

### 2. Rentabilidad

| Métrica | Valor |
|---|---|
| Revenue total | $9.498.030,89 |
| Costo total (COGS) | $3.785.159,27 |
| Gasto en marketing | $2.871.843,53 |
| Gross profit | $5.712.871,62 |
| **Net profit** | **$2.841.028,09** |
| **Margen neto** | **29,91%** |

- Ticket promedio por orden: **$385,94**, con **1,51** productos por orden en promedio
- Producto más vendido, tanto en unidades como en revenue: **Vacuum-Pro-Black**
- Gasto en marketing por canal: social $976.818, orgánico $972.651, búsqueda paga $922.374 (reparto casi parejo)

### 3. Embudo de conversión (SQL)

| Etapa | Usuarios únicos | Conversión vs. paso anterior |
|---|---|---|
| first_visit | 7.796 | — |
| select_item | 7.582 | 97,26% |
| add_to_cart | 7.634 | 100,69% |
| begin_checkout | 7.208 | 94,42% |
| add_payment_info | 6.250 | **86,71%** |
| purchase | 6.240 | 99,84% |

- La mayor fuga está entre **iniciar el checkout y agregar el método de pago**: se pierden 958 usuarios.
- Conversión final de punta a punta: **80,04%**.
- Nota: `add_to_cart` tiene más usuarios que `select_item`, es decir, algunos usuarios agregan al carrito sin pasar por ese evento.

### 4. Retención por cohortes (SQL)

Retención semanal de las cohortes de enero a mayo de 2025:

| Cohorte | Usuarios | Semana 1 | Semana 2 | Semana 3 |
|---|---|---|---|---|
| 2025-01 | 1.627 | 42,84% | 41,06% | 40,32% |
| 2025-02 | 1.444 | 42,31% | 42,17% | 43,98% |
| 2025-03 | 1.636 | 41,38% | 43,09% | 42,18% |
| 2025-04 | 1.606 | 42,34% | 43,40% | 41,28% |
| 2025-05 | 1.687 | 41,20% | 40,07% | 41,85% |

La retención se mantiene estable, entre **40% y 44%**, en todas las cohortes y semanas.

### 5. Prueba A/B: nueva interfaz de checkout

- Control: 779 de 4.965 usuarios convirtieron (**15,69%**)
- Tratamiento: 820 de 5.035 usuarios convirtieron (**16,29%**)
- Prueba chi-cuadrado: χ² = 0,6178, **p = 0,4319** (α = 0,05)
- **Conclusión:** no hay evidencia suficiente de una diferencia significativa; la nueva interfaz no demostró mejorar la conversión.

### 6. Dashboard (Power BI)

Dashboard de 3 páginas (`RappiPlus_Dashboard.pbix`) construido sobre los CSV limpios, con una tabla de fechas para análisis temporal.

| Página | Contenido |
|---|---|
| Resumen ejecutivo | KPIs de revenue, costo, profit, gasto en marketing, ticket promedio y cantidad promedio; revenue y profit por categoría; evolución mensual y revenue acumulado del año (YTD) |
| Detalle de órdenes | Tabla de órdenes con profit resaltado en verde o rojo, cantidad vendida por producto y filtros por categoría y fecha |
| Detalle de producto | Drill-through: al seleccionar un producto se ven todos sus pedidos |

![Resumen ejecutivo](imagenes/dashboard_1.png)
![Detalle de órdenes](imagenes/dashboard_2.png)
![Detalle de producto](imagenes/dashboard_3.png)

## Autor

Juan David Díaz Bogotá, Colombia
https://www.linkedin.com/in/juanddiaz82/

