# 🚛 Logistic Owner Operator AI – POC

**📌 Tipo de proyecto:** Proof of Concept (POC)  
**🎯 Enfoque:** Ingeniería de Datos aplicada a transporte logístico  
**📍 Ubicación:** Estados Unidos  
**🧠 Tecnología:** Python · Web Scraping · ETL · Google Cloud Platform · BigQuery · Visualización · IA  

---

## 📘 Descripción general

**Logistic Owner Operator AI** es un **POC (Proof of Concept)** de ingeniería de datos enfocado en **transportistas independientes del sector logístico en EE.UU.**, utilizando **inteligencia artificial** como eje transformador.

Este proyecto busca ayudar a **validar brokers y dispatchers**, mejorar la **optimización de costos** y aumentar la **eficiencia de rutas**, particularmente para vehículos de carga como **Cargo Van, Sprinter Van, Box Truck y Semi Truck sin dry van**, con una capacidad útil de entre **3,600 lb y 26,000 lb**.

Además, se incorporarán variables relacionadas con los **plazos y costos de pago ofrecidos por los brokers**, ya que este factor tiene un impacto directo en la **liquidez y la rentabilidad final del operador**. Se analizarán tres modalidades comunes:

- **Same Day Payment** – 5% de comisión  
- **2–3 Business Days** – 3% de comisión  
- **14 Business Days** – 0% de comisión

Esto permitirá **comparar rutas, cargas y brokers no solo por ingresos brutos**, sino también por **efectivo neto recibido en función del tiempo de pago**.

La intención no es determinar una única unidad más rentable, **sino identificar bajo qué condiciones operativas cada tipo de unidad (Cargo Van, Sprinter, Box Truck, Semi sin dry van)** alcanza su **máximo potencial de rentabilidad.**

Aunque todas pueden ser rentables, el objetivo es descubrir **cómo, cuándo y dónde lo son,** considerando variables como **carga útil, tipo de carga, millaje, tarifa promedio por ruta, tiempo de entrega, zona de operación y modalidad de pago.**

---

## 🛠️ Metas del proyecto (POC Data Engineering)

1. 📦 **Validación de brokers/dispatchers confiables**
2. 📊 **Comparación de rentabilidad según tipo de unidad**
3. 💸 **Impacto de los plazos de pago en la rentabilidad neta**
4. 🛣️ **Optimización de rutas, millaje y zonas de entrega**
5. 🧠 **Exploración del uso de IA para análisis predictivo en logística**

---

## 💰 Tipos de pago ofrecidos por brokers

Dado que muchos brokers hoy ofrecen servicios de pago directo, se analizarán las siguientes opciones por su **impacto directo en el flujo de caja y la utilidad real**:

| Tipo de Pago           | Tiempo estimado   | Comisión típica |
|------------------------|-------------------|-----------------|
| Same Day Payment       | Mismo día         | 5%              |
| 2–3 Business Days      | 2–3 días hábiles  | 3%              |
| 14 Business Days       | 14 días hábiles   | 0%              |

Estas modalidades serán evaluadas en combinación con el ingreso bruto por carga para calcular el ingreso **neto real**.

---

## 🔍 Variables principales del análisis

- **Tipo de unidad (van, box truck, etc.)**
- **Peso y dimensiones de la carga**
- **Broker/dispatcher que ofrece la carga**
- **Región o estado**
- **Distancia de la ruta (millas)**
- **Tarifa por milla (USD/milla)**
- **Plazo y tipo de pago**
- **Tiempo estimado de entrega**
- **Costo estimado operativo (combustible, mantenimiento, etc.)**

---

## 📦 Fuentes de datos (en planificación)

- Web Scraping desde portales de brokers/fletes (ej. DAT, TruckSmarter)
- Documentos de carga reales anonimizados
- APIs logísticas públicas
- Bases de datos estructuradas en Google BigQuery

---

## 🧱 Etapas del Web Scraper
### ✅ Etapa 1: Extracción Estructurada por Bloques

En esta etapa inicial, se diseñó un scraper orientado a la extracción temática y ordenada de información crítica del sitio web SAFER FMCSA, utilizando exclusivamente el número MC como clave de búsqueda.

**Objetivo:**
Extraer bloques bien definidos de datos regulatorios y operativos para transportistas registrados en el sistema del Departamento de Transporte de EE.UU. (USDOT).

**Bloques extraídos:**

**🆔 Identificación de la entidad**

  - Legal Name, DBA Name, USDOT Number, MC Number.
  - Physical Address, Mailing Address, Phone.

**🏢 Estado del registro:**

  - Carrier/Broker Status, Entity Type.

**📊 Clasificación de operación:**

  - Operation Classification, Carrier Operation.

**🧯 Seguridad y cumplimiento:**

  - Inspecciones, % fuera de servicio.
  - Historial de accidentes.
  - Calificación de seguridad.
  - Técnicas utilizadas:
    - Requests para cargar HTML desde la web pública de FMCSA.
    - BeautifulSoup para el parseo estructurado.
    - Extracción selectiva por segmentos HTML con múltiples tables anidadas.
    - Consolidación final de los datos por bloques temáticos en un diccionario.
    - Exportación en formato .json para posteriores flujos ETL.

Esta segmentación estructurada permitirá modularizar las próximas etapas del scraper, conectar con bases de datos (como BigQuery) y escalar el scraping a múltiples MC Numbers automáticamente.

### 🔄 Etapa 2: Serialización en JSON

**Objetivo:**
Transformar y almacenar toda la información extraída por bloques temáticos desde el portal SAFER de la FMCSA en un archivo estructurado en formato .json, identificable por su número MC.

**Descripción:**
En esta etapa, el scraper evoluciona de ser un simple visualizador a convertirse en una herramienta de recolección persistente de datos, al guardar cada consulta en un archivo `.json` con nombre único según el MC consultado (ej. `MC_1498383.json`).

El diseño modular por bloques permite estructurar la información en categorías fácilmente reutilizables:

  - USDOT Information.
  - Operating Authority Status.
  - Company Information.
  - Operation Classification.
  - Carrier Operation.
  - Inspections Summary.
  - Crash History.
  - Carrier Safety Rating.


**Ejemplo de archivo generado:**

```json
{
  "USDOT Information": {
    "Entity Type": "CARRIER",
    "USDOT Status": "ACTIVE",
    "USDOT Number": "3992838",
    "MCS-150 Form Date": "01/19/2025",
    "Out of Service Date": "None",
    "State Carrier ID Number": "N/A",
    "MCS-150 Mileage (Year)": "N/A"
  },
  "Operating Authority Status": "AUTHORIZED FOR Property For Licensing and Insurance details click here.",
  "Company Information": {
    "Legal Name": "MYDELIVERYS919 LLC",
    "DBA Name": "",
    "Physical Address": "8226 ROLLINGHITCH CT MAINEVILLE, OH   45039",
    "Mailing Address": "8226 ROLLINGHITCH CT MAINEVILLE, OH   45039",
    "Phone": "(513) 828-7166",
    "DUNS Number": "--",
    "Power Units": "0",
    "Non-CMV Units": "1",
    "Drivers": "1"
  },
  "Operation Classification": [
    "Auth. For Hire",
    "Interstate",
    "General Freight",
    "Metal: sheets, coils, rolls",
    "Building Materials",
    "Utilities"
  ],
  "Carrier Operation": "Interstate",
  "Inspections Summary": {
    "Inspections": {
      "Vehicle": "0",
      "Driver": "0",
      "Hazmat": "0",
      "IEP": "0"
    },
    "Out of Service": {
      "Vehicle": "0",
      "Driver": "0",
      "Hazmat": "0",
      "IEP": "0"
    },
    "Out of Service %": {
      "Vehicle": "0%",
      "Driver": "0%",
      "Hazmat": "0%",
      "IEP": "0%"
    },
    "Natl Avg %": {
      "Vehicle": "22.26%",
      "Driver": "6.67%",
      "Hazmat": "4.44%",
      "IEP": "N/A"
    }
  },
  "Crash History": {
    "Fatal": "0",
    "Injury": "0",
    "Tow": "0",
    "Total": "0"
  },
  "Carrier Safety Rating": {
    "Rating Date": "None",
    "Review Date": "None",
    "Rating": "None",
    "Type": "None"
  }
}
```

**📁 Ubicación de los archivos JSON generados:**  
Todos los archivos se almacenan en la carpeta `outputs/` del entorno local, por ejemplo:  
`C:\outputs\MC_1498383.json`

**💡 Beneficio:**  
Esta estructura permite consultas posteriores, integración con pipelines ETL, análisis comparativo entre MCs, o visualización en dashboards externos.

---

## 🔄 Futuros pasos del proceso ETL

A continuación se describen las acciones pendientes para completar el flujo ETL (Extracción, Transformación y Carga) del scraper de MCs:

### 🧪 Extracción (E)
- [x] Extraer y estructurar los bloques principales desde FMCSA SAFER:
  - Información USDOT
  - Autoridad Operativa
  - Datos de la Compañía
  - Clasificación de Operaciones
  - Historial de Inspecciones
  - Historial de Colisiones
  - Calificación de Seguridad del Transportista
- [ ] Añadir bloques adicionales:
  - Actualización Bienal (Biennial Update)
  - Información de Seguro (Insurance)
  - Licencias suspendidas / desactivadas

### 🔧 Transformación (T)
- [ ] Normalizar campos comunes (fechas, N/A, valores vacíos)
- [ ] Agregar validación de estructura antes de guardar cada JSON
- [ ] Consolidar etiquetas para facilitar análisis en BigQuery
- [ ] Establecer estructura uniforme por bloque de datos

### 🚀 Carga (L)
- [ ] Crear bucket en Google Cloud Storage (GCS)
- [ ] Automatizar carga de archivos JSON desde carpeta local a GCS
- [ ] Crear tabla en BigQuery con esquema adaptable a los JSON
- [ ] Cargar los datos en BigQuery desde GCS

---
### 🔍 Retos técnicos y soluciones aplicadas

Durante esta primera etapa de desarrollo, enfrentamos y superamos varios desafíos clave en la construcción de un scraper robusto y preciso:

#### 🧱 1. Navegación basada en DOM y estructura inconsistente
- **Reto**: La estructura HTML del portal de la FMCSA (SAFER) varía sutilmente entre diferentes perfiles MC.
- **Solución**: Diseñamos extractores modulares por bloque (USDOT Info, Company Info, Classification, Inspections, etc.) utilizando `BeautifulSoup` y un enfoque centrado en etiquetas `<th>` con expresiones regulares. Esto permitió extraer datos aún cuando los valores no están directamente alineados con los `label`.

#### ⏱️ 2. Sincronización y tiempos de espera
- **Reto**: La carga de la página no es inmediata; algunas tablas pueden tardar unos segundos en aparecer completamente.
- **Solución**: Implementamos `WebDriverWait` junto a condiciones explícitas (`EC.presence_of_element_located`) para asegurarnos de que el DOM esté completamente cargado antes de iniciar el parseo con BeautifulSoup.

#### ⚠️ 3. Errores de navegación o datos ausentes
- **Reto**: Algunos números MC no devuelven información completa o presentan errores de carga.
- **Solución**: Se incorporaron bloques `try/except` y validación de contenido con `if not soup.find(...)`, permitiendo capturar errores sin detener el flujo del scraper.

#### 🧩 4. Modularidad y funciones helper
- **Reto**: Repetición de patrones en la extracción de valores similares.
- **Solución**: Creamos funciones auxiliares (`get_value_by_label`, `get_address_block`, `extract_table_data`, etc.) para reducir código duplicado y mejorar la legibilidad. Esto permite una arquitectura flexible por bloques temáticos.

#### 🔒 5. Cierre de sesión y liberación de recursos
- **Reto**: El uso de WebDriver puede dejar procesos abiertos en segundo plano.
- **Solución**: Añadimos un cierre limpio del navegador con `driver.quit()` y aseguramos el uso del navegador dentro de un bloque `try/finally` para prevenir fugas de memoria.

---

### 📦 Resumen técnico de la Etapa 2

A diferencia de la Etapa 1, esta fase no presentó grandes complicaciones técnicas. Aprovechando la estructura modular de extractores temáticos (`extract_usdot_information`, `extract_company_information`, `extract_classifications`, etc.), fue posible consolidar todos los bloques en un diccionario principal y exportarlos fácilmente a formato `.json`.

#### ✅ Lo que se logró:

- Recolección temática por bloques (USDOT Info, Company Info, Classification, Inspections, Crash, Rating).
- Armado de un único diccionario estructurado (`carrier_data`) con claves temáticas.
- Inclusión del número MC como identificador único en el nombre del archivo.
- Exportación usando `json.dump()` con formato legible (`indent=4`) para facilitar futuras validaciones y análisis.
- Guardado automático en la carpeta `/outputs/`, por ejemplo:

```json```
📁 outputs/MC_1498383.json

---

✨ Gracias a estos enfoques, logramos construir una **Etapa 1 sólida, modular y resiliente**, capaz de adaptarse a múltiples perfiles del sitio web de la FMCSA.

---

## 📌 Resultados esperados

- Cuadro comparativo de rentabilidad neta según tipo de unidad y modalidad de pago
- Recomendaciones para transportistas independientes
- Dashboard interactivo (Looker Studio o Python) con visualización por estado, unidad y tipo de broker
- Flujo ETL documentado y reproducible
- Oportunidades de escalado hacia dry vans o cargas LTL/FTL

---

## 🚧 Estado actual del proyecto

- [x] Concepto definido (POC)  
- [x] Objetivos priorizados  
- [ ] Diseño del flujo ETL  
- [ ] Construcción del scraper inicial  
- [ ] Carga a BigQuery  
- [ ] Análisis exploratorio (EDA)  
- [ ] Visualizaciones  
- [ ] Documentación final

---

## 🤝 Impacto en la comunidad

Este proyecto está inspirado y dirigido especialmente a la comunidad de transportistas independientes de EE.UU., con quienes comparto experiencias a través de un grupo en Facebook. Una vez finalizado, los hallazgos serán compartidos con el grupo para validar resultados, recibir retroalimentación y contribuir al crecimiento colectivo del gremio.

Este POC busca ser una herramienta útil, realista y escalable para mejorar la toma de decisiones diarias de los owner-operators.

---

## 👩‍💻 Autora

**Lauris Olivares** – Data Engineer | SAP Basis Consultant | Owner Operator  
GitHub: [laurisolivares-dev](https://github.com/laurisolivares-dev)  
LinkedIn: [lauris-olivares-06415553](https://linkedin.com/in/lauris-olivares-06415553)

---

