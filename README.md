<!-- ============================================================
     ENCABEZADO (rúbrica: universidad, asignatura, paralelo, integrantes, fecha)
     ============================================================ -->

<div align="center">

# ESCUELA POLITÉCNICA NACIONAL
### Facultad de Ingeniería de Sistemas

**Asignatura:** Business Intelligence
**Paralelo:** _[Completar]_

## Práctica 1. Implementación de un proceso ETL y Staging Area con Pentaho Data Integration

**Integrantes:**
- Alvaro Montalvan
- Ruben Cuenca
- Jonathan Cuasapaz
- Ruben Cuenca

**Fecha:** _[10/10/2026]_

</div>

---

<!-- ============================================================
     ÍNDICE CON HIPERVÍNCULOS (rúbrica)
     Si cambian un título, actualicen también el ancla del enlace.
     ============================================================ -->

## Índice

1. [Objetivo del proceso](#1-objetivo-del-proceso)
2. [Fuentes de datos utilizadas](#2-fuentes-de-datos-utilizadas)
3. [Problemas encontrados en los datos](#3-problemas-encontrados-en-los-datos)
   - 3.1 [Problemas en el archivo Excel (.xls)](#31-problemas-en-el-archivo-excel-xls)
   - 3.2 [Problemas en el archivo JSON (.json)](#32-problemas-en-el-archivo-json-json)
   - 3.3 [Problemas en el archivo CSV (.csv)](#33-problemas-en-el-archivo-csv-csv)
4. [Transformaciones aplicadas](#4-transformaciones-aplicadas)
   - 4.1 [Transformaciones sobre el Excel](#41-transformaciones-sobre-el-excel)
   - 4.2 [Transformaciones sobre el JSON](#42-transformaciones-sobre-el-json)
   - 4.3 [Transformaciones sobre el CSV](#43-transformaciones-sobre-el-csv)
5. [Flujo ETL desarrollado](#5-flujo-etl-desarrollado)
   - 5.1 [Diagrama Excel](#51-diagrama-excel)
   - 5.2 [Diagrama JSON](#52-diagrama-json)
   - 5.3 [Diagrama CSV](#53-diagrama-csv)
6. [Evidencia del resultado](#6-evidencia-del-resultado)
   - 6.1 [Excel](#61-excel)
   - 6.2 [JSON](#62-json)
   - 6.3 [CSV](#63-csv)
7. [Relación con una arquitectura de Data Warehouse](#7-relación-con-una-arquitectura-de-data-warehouse)
8. [Conclusiones](#8-conclusiones)
9. [Referencias bibliográficas](#9-referencias-bibliográficas)
10. [Declaración de uso de Inteligencia Artificial](#10-declaración-de-uso-de-inteligencia-artificial)
- [Índice de figuras](#índice-de-figuras)
- [Índice de tablas](#índice-de-tablas)

---

## Índice de figuras

<!-- Numerar todas las figuras de forma correlativa. Cada figura debe tener: número, título y ser referenciada en el texto ("como se observa en la Figura X"). -->

| N.º | Título | Sección |
|-----|--------|---------|
| Figura 1 | Configuración de _[transformación 1]_ en Pentaho (Excel) | [4.1.1](#411-transformación-1) |
| Figura 2 | Configuración de _[transformación 2]_ en Pentaho (Excel) | [4.1.2](#412-transformación-2) |
| Figura 3 | Configuración de Mapeo de valores en Pentaho | [4.2.1](#421-mapeo-de-valores) |
| Figura 4 | Configuración de Filtrar Filas en Pentaho | [4.2.2](#422-filtrar-filas) |
| Figura 5 | Configuración de _[transformación 1]_ en Pentaho (CSV) | [4.3.1](#431-transformación-1) |
| Figura 6 | Configuración de _[transformación 2]_ en Pentaho (CSV) | [4.3.2](#432-transformación-2) |
| Figura 7 | Flujo ETL Excel | [5.1](#51-diagrama-excel) |
| Figura 8 | Flujo ETL JSON | [5.2](#52-diagrama-json) |
| Figura 9 | Flujo ETL CSV | [5.3](#53-diagrama-csv) |
| Figura 10 | Datos Excel antes de la transformación | [6.1.1](#611-excel-antes) |
| Figura 11 | Datos Excel después de la transformación | [6.1.2](#612-excel-después) |
| Figura 12 | Datos JSON antes de la transformación | [6.2.1](#621-json-antes) |
| Figura 13 | Datos JSON después de la transformación | [6.2.2](#622-json-después) |
| Figura 14 | Datos CSV antes de la transformación | [6.3.1](#631-csv-antes) |
| Figura 15 | Datos CSV después de la transformación | [6.3.2](#632-csv-después) |
| Figura 16 | Arquitectura de Data Warehouse y ubicación del proceso desarrollado | [7](#7-relación-con-una-arquitectura-de-data-warehouse) |

## Índice de tablas

| N.º | Título | Sección |
|-----|--------|---------|
| Tabla 1 | Resumen de las fuentes de datos utilizadas | [2](#2-fuentes-de-datos-utilizadas) |
| Tabla 2 | Problemas de calidad de datos en el archivo Excel | [3.1](#31-problemas-en-el-archivo-excel-xls) |
| Tabla 3 | Problemas de calidad de datos en el archivo JSON | [3.2](#32-problemas-en-el-archivo-json-json) |
| Tabla 4 | Problemas de calidad de datos en el archivo CSV | [3.3](#33-problemas-en-el-archivo-csv-csv) |
| Tabla 5 | Declaración de uso de IA | [10](#10-declaración-de-uso-de-inteligencia-artificial) |

---

## 1. Objetivo del proceso

<!-- Describir qué se busca lograr con el proceso ETL: qué datos se integran, para qué y cuál es el resultado esperado. -->

_[Completar]_

---

## 2. Fuentes de datos utilizadas

<!-- Requisito: al menos dos tipos diferentes de fuentes de datos. Aquí se documentan tres: XLS, JSON y CSV. -->

**Tabla 1.** _Resumen de las fuentes de datos utilizadas._

| Fuente | Tipo / Formato | Origen | Descripción | N.º de registros | N.º de campos |
|--------|----------------|--------|-------------|------------------|---------------|
| _[nombre_archivo.xls]_ | Excel | _[ ]_ | _[ ]_ | _[ ]_ | _[ ]_ |
| h9gi-nx95.json | JSON | [NYC Motor Vehicle Collisions Dataset](https://data.cityofnewyork.us/resource/h9gi-nx95.json?select=collision_id,crash_date,borough,vehicle_type_code1,contributing_factor_vehicle_1,number_of_persons_injured&where=borough%20is%20not%20null&limit=2000&offset=300000) | Registros de choques de vehículos en la ciudad de Nueva York, obtenidos de la API de NYC Open Data. Cada registro tiene el identificador del choque, la fecha, el distrito (borough), el tipo de vehículo, el factor que contribuyó al choque y el número de personas heridas. | 2000 | 6 |
| _[nombre_archivo.csv]_ | CSV | _[ ]_ | _[ ]_ | _[ ]_ | _[ ]_ |


---

## 3. Problemas encontrados en los datos

<!-- Identificar problemas de calidad: valores inconsistentes, mayúsculas/minúsculas, espacios, nulos, fechas inválidas, duplicados, formatos distintos, etc. -->

### 3.1 Problemas en el archivo Excel (.xls)

**Tabla 2.** _Problemas de calidad de datos en el archivo Excel._

| Campo | Descripción del problema |
|-------|--------------------------|
| _[ ]_ | _[ ]_ |
| _[ ]_ | _[ ]_ |

### 3.2 Problemas en el archivo JSON (.json)

**Tabla 3.** _Problemas de calidad de datos en el archivo JSON._

| Campo | Descripción del problema |
|-------|--------------------------|
| vehicle_type_code1 | Tiene demasiadas etiquetas sueltas para el mismo tipo de vehículo. Sedan y 4 dr sedan son lo mismo. PK es una abreviatura de Pick-up Truck. Dump y Tractor Truck Diesel son camiones.  |
| contributing_factor_vehicle_1 | Tiene el valor Unspecified que significa “no se sabe” y no es una causa real|

### 3.3 Problemas en el archivo CSV (.csv)

**Tabla 4.** _Problemas de calidad de datos en el archivo CSV._

| Campo | Descripción del problema |
|-------|--------------------------|
| _[ ]_ | _[ ]_ |
| _[ ]_ | _[ ]_ |

---

## 4. Transformaciones aplicadas

<!-- Requisitos:
     - Parte 1 (dataset provisto / Excel): corregir nombres y apellidos; validar fechas.
     - Parte 2: al menos dos transformaciones de limpieza o estandarización.
     Para cada transformación: nombre, descripción breve y captura de la configuración en Pentaho.
     Al poner el nombre real de la transformación, actualicen también el enlace en el Índice de figuras. -->

### 4.1 Transformaciones sobre el Excel

#### 4.1.1 _[Transformación 1]_
_[Descripción breve de lo que hace la transformación.]_
![Configuración del paso en Pentaho](img/EXCELtrans1.png)
**Figura 1.** _Configuración de [transformación 1] en Pentaho._

#### 4.1.2 _[Transformación 2]_
_[Descripción breve de lo que hace la transformación.]_
![Configuración del paso en Pentaho](img/EXCELtrans2.png)
**Figura 2.** _Configuración de [transformación 2] en Pentaho._

### 4.2 Transformaciones sobre el JSON

#### 4.2.1 Mapeo de valores
Reemplaza los valores de un campo por otros, según una tabla de equivalencias definida.

Se aplicó sobre el campo `vehicle_type_code1`, sobrescribiendo el mismo campo, para agrupar las distintas etiquetas de un mismo tipo de vehículo en categorías estándar:

- **Sedan:** 4 dr sedan, Convertible
- **SUV:** Station Wagon/Sport Utility Vehicle, Carry All
- **Pickup:** Pick-up Truck, PK
- **Camión pesado:** Dump, Tractor Truck Diesel
- **Transporte público:** Taxi, Bus
- **Moto/Bici:** Motorcycle, E-Bike

Los valores que no están en la tabla (por ejemplo, "Sedan") se mantienen sin cambios.

![Configuración del paso en Pentaho](img/JSONtrans1.png)
**Figura 3.** _Configuración de Mapeo de valores en Pentaho._

#### 4.2.2 Filtrar filas
Revisa cada fila con una condición y decide si pasa o se descarta.

Solo pasan al paso **JSON output** las filas que cumplen ambas condiciones:

- `contributing_factor_vehicle_1 <> Unspecified`: se descartan los choques cuya causa es desconocida.
- `vehicle_type_code1 IS NOT NULL`: se descartan los choques sin tipo de vehículo registrado.

Las filas que no cumplen la condición no se envían a ningún paso, por lo que se eliminan del resultado.

![Configuración del paso en Pentaho](img/JSONtrans2.png)
**Figura 4.** _Configuración de Filtrar Filas en Pentaho._

### 4.3 Transformaciones sobre el CSV

#### 4.3.1 _[Transformación 1]_
_[Descripción breve de lo que hace la transformación.]_
![Configuración del paso en Pentaho](img/CSVtrans1.png)
**Figura 5.** _Configuración de [transformación 1] en Pentaho._

#### 4.3.2 _[Transformación 2]_
_[Descripción breve de lo que hace la transformación.]_
![Configuración del paso en Pentaho](img/CSVtrans2.png)
**Figura 6.** _Configuración de [transformación 2] en Pentaho._

---

## 5. Flujo ETL desarrollado

### 5.1 Diagrama Excel
![Flujo ETL Excel](img/flujoEXCEL.png)
**Figura 7.** _Flujo ETL Excel._

### 5.2 Diagrama JSON
El flujo tiene cuatro pasos:

1. **JSON input (Extract):** lee el archivo `h9gi-nx95.json` y extrae los 6 campos.
2. **Mapeo de valores (Transform):** estandariza los tipos de vehículo en `vehicle_type_code1`.
3. **Filtrar filas (Transform):** descarta los registros con causa `Unspecified` o sin tipo de vehículo.
4. **JSON output (Load):** escribe los registros limpios en un nuevo archivo JSON.

![Flujo ETL JSON](img/flujoJSON.png)
**Figura 8.** _Flujo ETL JSON._

### 5.3 Diagrama CSV
![Flujo ETL CSV](img/flujoCSV.png)
**Figura 9.** _Flujo ETL CSV._

---

## 6. Evidencia del resultado

<!-- Capturas de los datos antes y después de la transformación. -->

### 6.1 Excel
#### 6.1.1 Excel antes
![Excel antes de la transformacion](img/EXCELantes.png)
**Figura 10.** _Datos antes de la transformacion._

#### 6.1.2 Excel después
![Excel despues de la transformacion](img/EXCELdespues.png)
**Figura 11.** _Datos despues de la transformacion._

### 6.2 JSON
#### 6.2.1 JSON antes
Vista previa del paso JSON input con los datos originales. En `vehicle_type_code1` aparecen etiquetas distintas para un mismo tipo de vehículo, por ejemplo "Station Wagon/Sport Utility Vehicle", "Carry All", "4 dr sedan", "PK" o "Dump". En `contributing_factor_vehicle_1` hay muchos registros con valor "Unspecified".

![JSON antes de la transformacion](img/JSONantes.png)
**Figura 12.** _Datos antes de la transformacion._

#### 6.2.2 JSON después
Vista previa del archivo de salida, leído de nuevo con un JSON input. Los tipos de vehículo quedan agrupados en categorías estándar: Sedan, SUV, Pickup, Camión pesado y Transporte público. Ya no aparecen registros con causa "Unspecified"; por ejemplo, el choque 4287811, que tenía causa "Unspecified", ya no está en la salida.

![JSON despues de la transformacion](img/JSONdespues.png)
**Figura 13.** _Datos despues de la transformacion._

### 6.3 CSV
#### 6.3.1 CSV antes
![CSV antes de la transformacion](img/CSVantes.png)
**Figura 14.** _Datos antes de la transformacion._

#### 6.3.2 CSV después
![CSV despues de la transformacion](img/CSVdespues.png)
**Figura 15.** _Datos despues de la transformacion._

---

## 7. Relación con una arquitectura de Data Warehouse

<!-- Explicar cómo cada parte del proceso (fuentes, staging area, transformación, destino) se corresponde con los componentes de un Data Warehouse / Data Mart. -->

_[Completar]_

![Arquitectura de Data Warehouse](img/arquitecturaDW.png)
**Figura 16.** _Arquitectura de Data Warehouse y ubicación del proceso desarrollado._

---

## 8. Conclusiones

- _[Conclusión 1]_
- _[Conclusión 2]_
- _[Conclusión 3]_

---

## 9. Referencias bibliográficas

<!-- Usar norma APA 7 o IEEE de forma consistente. Citar en el texto. -->

1. _[Referencia en formato APA / IEEE]_
2. _[Referencia en formato APA / IEEE]_

---

## 10. Declaración de uso de Inteligencia Artificial

<!-- Declarar herramienta(s), para qué se usaron y el porcentaje aproximado de uso. -->

**Tabla 5.** _Declaración de uso de IA._

| Herramienta | Uso / Actividad | Sección(es) | Porcentaje aproximado |
|-------------|-----------------|-------------|-----------------------|
| _[ ]_ | _[ ]_ | _[ ]_ | _[ ]_ % |

**Porcentaje total de uso de IA en el trabajo:** _[ ]_ %

_[Declaración breve de los integrantes sobre la revisión y validación del contenido generado.]_
