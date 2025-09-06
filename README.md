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

La intención es analizar **cuál tipo de unidad ofrece mayor rentabilidad**, considerando variables como carga útil, tipo de carga, millaje, pago promedio por ruta, tiempo de entrega y zona de operación.

---

## 🎯 Objetivos del proyecto

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

## 👩‍💻 Autora

**Lauris Olivares** – Data Engineer | SAP Basis Consultant | Owner Operator  
GitHub: [laurisolivares-dev](https://github.com/laurisolivares-dev)  
LinkedIn: [lauris-olivares-06415553](https://linkedin.com/in/lauris-olivares-06415553)

---

