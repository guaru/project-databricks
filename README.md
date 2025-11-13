<div align="center">

# 🍏 Apple Store Sales and Warranty ETL Pipeline
### Arquitectura Medallion en Azure Databricks

[![Databricks](https://img.shields.io/badge/Databricks-FF3621?style=for-the-badge&logo=databricks&logoColor=white)](https://databricks.com/)
[![Azure](https://img.shields.io/badge/Azure-0078D4?style=for-the-badge&logo=microsoft-azure&logoColor=white)](https://azure.microsoft.com/)
[![PySpark](https://img.shields.io/badge/PySpark-E25A1C?style=for-the-badge&logo=apache-spark&logoColor=white)](https://spark.apache.org/)
[![Delta Lake](https://img.shields.io/badge/Delta_Lake-00ADD8?style=for-the-badge&logo=delta&logoColor=white)](https://delta.io/)
[![Power BI](https://img.shields.io/badge/Power_BI-F2C811?style=for-the-badge&logo=power-bi&logoColor=black)](https://powerbi.microsoft.com/)
[![CI/CD](https://img.shields.io/badge/CI%2FCD-GitHub_Actions-2088FF?style=for-the-badge&logo=github-actions&logoColor=white)](https://github.com/features/actions)

*Pipeline automatizado de datos para análisis de ventas y garantias de Apple Stores con arquitectura de tres capas y despliegue continuo*

</div>

---

## 🎯 Descripción

Pipeline ETL enterprise-grade que transforma datos crudos de ventas y garantias de tiendas Apple de diferentes años y paises, implementando la **Arquitectura Medallion** (Bronze-Silver-Gold) en Azure Databricks con **CI/CD completo** y **Delta Lake** para garantizar consistencia ACID.

### ✨ Características Principales

- 🔄 **ETL Automatizado** - Pipeline completo con despliegue automático via GitHub Actions
- 🏗️ **Arquitectura Medallion** - Separación clara de capas Bronze → Silver → Gold
- 📊 **Modelo Dimensional** - Star Schema optimizado para análisis de negocio
- 🚀 **CI/CD Integrado** - Deploy automático en cada push a master
- 📈 **Power BI Ready** - Conexión directa con SQL Warehouse
- ⚡ **Delta Lake** - ACID transactions y time travel capabilities
- 🔔 **Monitoreo** - Notificaciones automáticas y logs detallados

---

## 🏛️ Arquitectura

### Flujo de Datos

```
📄 CSV (Raw Data)
    ↓
🥉 Bronze Layer (Ingesta sin transformación)
    ↓
🥈 Silver Layer (Limpieza + Modelo Dimensional)
    ↓
🥇 Gold Layer (Agregaciones de Negocio)
    ↓
📊 Power BI (Visualización)
```

### 📦 Capas del Pipeline

<table>
<tr>
<td width="33%" valign="top">

#### 🥉 Bronze Layer
**Propósito**: Zona de aterrizaje

**Tablas**: 
- `category` 
- `products` 
- `warranty`
- `sales` 
- `stores`

**Características**:
- ✅ Datos tal como vienen de origen
- ✅ Timestamp de ingesta
- ✅ Preservación histórica
- ✅ Sin validaciones

</td>
<td width="33%" valign="top">

#### 🥈 Silver Layer
**Propósito**: Modelo dimensional

**Tablas**:
- `category_sales`
- `product_sales`
- `store_sales`
- `store_warranty_status`
- `waranty_products`

**Características**:
- ✅ Star Schema
- ✅ Datos normalizados
- ✅ Validaciones completas

</td>
<td width="33%" valign="top">

#### 🥇 Gold Layer
**Propósito**: Analytics-ready

**Tablas**:
- kpi_category_sales        : Monto total en ventas agrupado por categoría y año
- kpi_product_sales         : Monto total en ventas agrupado por producto y año
- kpi_store_sales           : Monto total en ventas agrupado por tienda y año
- kpi_store_warranty_status : Total de reclamos por tienda en los diferentes estatus pivot
- kpi_product_warranty      : Productos con mayor reclamos post venta (garantía)

**Características**:
- ✅ Pre-agregados
- ✅ Optimizado para BI
- ✅ Performance máximo
- ✅ Actualizaciones automáticas

</td>
</tr>
</table>

---

## 📁 Estructura del Proyecto

```
etl-apple/
│
├── 📂 .github/
│   └── 📂 workflows/
│       └── 📄 deploy-certification.yml    # Pipeline CI/CD deploy a certification workspace databricks
├── 📂 process/
│   ├── 🐍 ingest_catalogs.py           # Bronze layer
│   ├── 🐍 ingest_sales.py              # Bronze Layer
│   ├── 🐍 ingest_warranty.py           # Bronze Layer
│   ├── 🐍 transform_sales.py           # Silver Layer
│   ├── 🐍 transform_warranty.py        # Silver Layer
│   └── 🐍 load_sales.py                # Gold Layer
│   └── 🐍 load_warranty.py             # Gold Layer
├── 📂 security/
|   ├── 🐍 Enviroment preparation.py    # Create Schema, Tables, External location
├── 📂 security/
|   ├── 🐍 Permissions.py               # Sql Grant
└── 📄 README.md
```
##  ETL
![Texto descriptivo](CICD_ETL_APPLE.png)
---

## 🛠️ Tecnologías

<div align="center">

| Tecnología | Propósito |
|:----------:|:----------|
| ![Databricks](https://img.shields.io/badge/Azure_Databricks-FF3621?style=flat-square&logo=databricks&logoColor=white) | Motor de procesamiento distribuido Spark |
| ![Delta Lake](https://img.shields.io/badge/Delta_Lake-00ADD8?style=flat-square&logo=delta&logoColor=white) | Storage layer con ACID transactions |
| ![PySpark](https://img.shields.io/badge/PySpark-E25A1C?style=flat-square&logo=apache-spark&logoColor=white) | Framework de transformación de datos |
| ![ADLS](https://img.shields.io/badge/ADLS_Gen2-0078D4?style=flat-square&logo=microsoft-azure&logoColor=white) | Data Lake para almacenamiento persistente |
| ![GitHub Actions](https://img.shields.io/badge/GitHub_Actions-2088FF?style=flat-square&logo=github-actions&logoColor=white) | Automatización CI/CD |
| ![Power BI](https://img.shields.io/badge/Power_BI-F2C811?style=flat-square&logo=power-bi&logoColor=black) | Business Intelligence y visualización |

</div>

---

## ⚙️ Requisitos Previos

- ☁️ Cuenta de Azure con acceso a Databricks
- 💻 Workspace de Databricks configurado
- 🖥️ Cluster activo (nombre: `CLUSTER COFFEE SHOP`)
- 🐙 Cuenta de GitHub con permisos de administrador
- 📦 Azure Data Lake Storage Gen2 configurado
- 📊 Power BI Desktop (opcional para visualización)

---

## 🚀 Instalación y Configuración

### 1️⃣ Clonar el Repositorio

```bash
git clone https://github.com/guaru/project-databricks.git
cd project-databricks
```

### 2️⃣ Configurar Databricks Token

1. Ir a Databricks Workspace
2. **User Settings** → **Developer** → **Access Tokens**
3. Click en **Generate New Token**
4. Configurar:
   - **Comment**: `GitHub CI/CD`
   - **Lifetime**: `90 days`
5. ⚠️ Copiar y guardar el token

### 3️⃣ Configurar GitHub Secrets

En tu repositorio: **Settings** → **Secrets and variables** → **Actions**

| Secret Name | Valor Ejemplo |
|------------|---------------|
| `DATABRICKS_HOST` | `https://adb-xxxxx.azuredatabricks.net` |
| `DATABRICKS_TOKEN` | `dapi_xxxxxxxxxxxxxxxx` |

### 4️⃣ Verificar Storage Configuration

```python
storage_path = "abfss://raw@adlsprojectsmartdata.dfs.core.windows.net"
```

<div align="center">

✅ **¡Configuración completa!**

</div>

---

## 💻 Uso

### 🔄 Despliegue Automático (Recomendado)

```bash
git add .
git commit -m "✨ feat: mejoras en pipeline"
git push origin master
```

**GitHub Actions ejecutará**:
- 📤 Deploy de notebooks a `/Production/ETL-APPLE`
- 🔧 Creación del workflow `WF_PROD_ETL_APPLE_SALES`
- ▶️ Ejecución completa:  Bronze → Silver → Gold
- 📧 Notificaciones de resultados

### 🖱️ Despliegue Manual desde GitHub

1. Ir al tab **Actions** en GitHub
2. Seleccionar **Coffee Shop ETL - Databricks Deploy**
3. Click en **Run workflow**
4. Seleccionar rama `master`
5. Click en **Run workflow**

### 🔧 Ejecución Local en Databricks

Navegar a `/Production/ETL-APPLE` y ejecutar en orden:

```
- Enviroment preparation.py         → Crear esquema
- ingest_catalogs.py                → Bronze Layer
- ingest_sales.py                   → Bronze Layer
- ingest_warranty.py                → Bronze Layer
- transform_sales.py                → Silver Layer
- transform_warranty.py             → Silver Layer
- load_sales.py                     → Gold Layer
- load_warranty.py                  → Gold Layer
```

---

## 📊 Modelo de Datos

### 🥈 Silver Layer - Star Schema

```
                    DIM_FECHA
                        |
                        |
DIM_CAFE -------- HECHO_VENTAS -------- DIM_PAGO
                        |
                   (Fact Table)
```

#### 🎯 HECHO_VENTAS (Fact Table)

| Campo | Tipo | Descripción |
|-------|------|-------------|
| `fecha` | DATE | Fecha de transacción (FK) |
| `hora` | TIMESTAMP | Hora exacta de venta |
| `id_cafe` | INT | Producto vendido (FK) |
| `id_pago` | INT | Método de pago (FK) |
| `cantidad` | INT | Unidades vendidas |
| `precio_unitario` | DOUBLE | Precio por unidad |
| `monto_total` | DOUBLE | Total de transacción |
| `franja_horaria` | STRING | Mañana/Tarde/Noche |
| `fecha_procesamiento` | TIMESTAMP | Audit timestamp |

#### ☕ DIM_CAFE (Product Dimension)

| Campo | Tipo | Descripción |
|-------|------|-------------|
| `id_cafe` | INT | Clave primaria |
| `coffee_name` | STRING | Nombre del producto |
| `categoria` | STRING | Espresso, Latte, Bebida Fría, Otros |
| `tamanio` | STRING | Grande, Mediano, Pequeño |
| `precio_base` | DOUBLE | Precio promedio histórico |
| `activo` | BOOLEAN | Estado del producto |
| `fecha_vigencia` | DATE | Fecha de alta |

#### 💳 DIM_PAGO (Payment Dimension)

| Campo | Tipo | Descripción |
|-------|------|-------------|
| `id_pago` | INT | Clave primaria |
| `cash_type` | STRING | card, cash, online |
| `proveedor` | STRING | Visa/Mastercard, PayPal, null |
| `activo` | BOOLEAN | Estado del método |

#### 📅 DIM_FECHA (Date Dimension)

| Campo | Tipo | Descripción |
|-------|------|-------------|
| `fecha` | DATE | Fecha completa (PK) |
| `anio` | INT | Año |
| `trimestre` | INT | Trimestre (1-4) |
| `mes` | INT | Mes (1-12) |
| `month_name` | STRING | Nombre del mes |
| `dia_semana` | INT | Día de la semana (1-7) |
| `weekday` | STRING | Nombre del día |
| `es_fin_semana` | BOOLEAN | Sábado o domingo |
| `es_feriado` | BOOLEAN | Día feriado |

### 🥇 Gold Layer - Agregados de Negocio

| Tabla | Descripción | Actualización |
|-------|-------------|---------------|
| `AGG_VENTAS_DIARIAS` | Métricas diarias consolidadas | Diaria |
| `AGG_VENTAS_POR_CAFE` | Performance por producto | Diaria |
| `AGG_VENTAS_POR_PAGO` | Distribución de métodos de pago | Diaria |
| `AGG_VENTAS_POR_DIA_SEMANA` | Patrones semanales | Diaria |
| `AGG_VENTAS_POR_FRANJA_HORARIA` | Análisis por hora del día | Diaria |
| `AGG_TOP_PRODUCTOS` | Ranking mensual de productos | Mensual |
| `AGG_RESUMEN_MENSUAL` | Dashboard ejecutivo | Mensual |

---

## 🔄 CI/CD

### Pipeline de GitHub Actions

```yaml
Workflow: Coffee Shop ETL - Databricks Deploy
├── Deploy notebooks → /prod/coffee_shop
├── Eliminar workflow antiguo (si existe)
├── Buscar cluster configurado
├── Crear nuevo workflow con 4 tareas
├── Ejecutar pipeline automáticamente
└── Monitorear y notificar resultados
```

### Configuración del Workflow Databricks

```
Tasks:
├── create_tables_ddl    (30min, 1 retry)
├── ingest_bronze        (60min, 2 retries)
├── transform_silver     (60min, 2 retries)
└── aggregate_gold       (60min, 2 retries)

⏰ Schedule: Diario 10:00 AM (Lima)
⏱️ Timeout total: 4 horas
🔒 Max concurrent runs: 1
📧 Notificaciones: lchaponant@gmail.com
```

---

## 📈 Conexión con Power BI

### Prerequisitos

- ✅ SQL Warehouse activo en Databricks
- ✅ Personal Access Token generado
- ✅ Power BI Desktop instalado

### Pasos de Conexión

#### 1️⃣ Obtener Credenciales de Databricks

En Databricks: **SQL Warehouses** → Seleccionar warehouse → **Connection Details**

Copiar:
- `Server hostname`: `adb-xxxxx.azuredatabricks.net`
- `HTTP Path`: `/sql/1.0/warehouses/xxxxx`

#### 2️⃣ Conectar Power BI Desktop

1. Abrir Power BI Desktop
2. **Get Data** → **More** → **Azure Databricks**
3. Ingresar credenciales copiadas
4. **Data Connectivity mode**: `DirectQuery` (recomendado)
5. **Autenticación**: Personal Access Token
6. Click **Connect**

#### 3️⃣ Seleccionar Tablas Gold

```
catalog_prod
└── golden
    ├── AGG_VENTAS_DIARIAS
    ├── AGG_VENTAS_POR_CAFE
    ├── AGG_VENTAS_POR_PAGO
    ├── AGG_VENTAS_POR_DIA_SEMANA
    ├── AGG_VENTAS_POR_FRANJA_HORARIA
    ├── AGG_TOP_PRODUCTOS
    └── AGG_RESUMEN_MENSUAL
```

#### 4️⃣ Configurar Modo de Conectividad

**DirectQuery (Recomendado)**
- ✅ Datos siempre actualizados
- ✅ No ocupa espacio en Power BI
- ✅ Queries se ejecutan en Databricks

**Import Mode**
- ✅ Más rápido para visualizaciones
- ⚠️ Requiere refresh programado
- ⚠️ Limitación de volumen de datos

### 📊 Dashboards Recomendados

- 📈 **Ventas Diarias**: Line chart con tendencias temporales
- 🏆 **Top Productos**: Bar chart con ranking de cafés
- 💳 **Análisis de Pagos**: Pie chart con distribución
- ⏰ **Patrones Horarios**: Heatmap de ventas por hora
- 📊 **Resumen Ejecutivo**: KPIs consolidados con cards

---

## 🔍 Monitoreo

### En Databricks

**Workflows**:
- Ir a **Workflows** en el menú lateral
- Buscar `CoffeeShopWFDeploy`
- Ver historial de ejecuciones

**Logs por Tarea**:
- Click en una ejecución específica
- Click en cada tarea para ver logs detallados
- Revisar stdout/stderr en caso de errores

### En GitHub Actions

- Tab **Actions** del repositorio
- Ver historial de workflows
- Click en ejecución específica para detalles
- Revisar logs de cada step

### Notificaciones

- 📧 **Email**: Configurado para `lchaponant@gmail.com` en caso de fallo
- 🔔 **GitHub**: Notificaciones en el repositorio

---

## 🐛 Troubleshooting

<details>
<summary><b>Error: Cluster not found</b></summary>

**Solución**: Verificar que el cluster `CLUSTER COFFEE SHOP` esté activo en Databricks.

```bash
# Verificar nombre exacto del cluster en Databricks
```
</details>

<details>
<summary><b>Error: Authentication failed</b></summary>

**Solución**: Regenerar Personal Access Token y actualizar GitHub Secrets.
</details>

<details>
<summary><b>Error: Storage path not found</b></summary>

**Solución**: Verificar que el ADLS Gen2 esté montado correctamente:

```python
storage_path = "abfss://coffeeshop@adlsdevluis25.dfs.core.windows.net"
```
</details>

---

## 👤 Autor

<div align="center">

### Alejandro de Jesus Ventura Martinez

[![LinkedIn](https://img.shields.io/badge/LinkedIn-0077B5?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/luis-chaponan-tejada/)
[![GitHub](https://img.shields.io/badge/GitHub-100000?style=for-the-badge&logo=github&logoColor=white)](https://github.com/ltechdev)
[![Email](https://img.shields.io/badge/Email-D14836?style=for-the-badge&logo=gmail&logoColor=white)](mailto:lchaponant@gmail.com)

**Data Engineering** | **Azure Databricks** | **Delta Lake** | **CI/CD**

</div>

---

## 📄 Licencia

Este proyecto está bajo la Licencia MIT - ver el archivo [LICENSE](LICENSE) para más detalles.

---

<div align="center">

**Proyecto**: Data Engineering - Arquitectura Medallion  
**Tecnología**: Azure Databricks + Delta Lake + CI/CD  
**Última actualización**: 2025


</div>