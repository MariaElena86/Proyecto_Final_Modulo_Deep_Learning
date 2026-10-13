#### 🧱 Diagnóstico de Marca Empleadora — KFC vs. Peers
#### Sentiment Analysis (Transformers) + Topic Modeling (BERTopic)

#### Glassdoor Reviews · Caso Práctico NLP · Evolve Academy

Identificar las fortalezas y áreas de mejora de **KFC** como empleador a partir de las opiniones de sus trabajadores en Glassdoor, comparándolas con sus competidores directos para fundamentar un plan de atracción y retención de talento.

- Peers elegidos: **McDonald's, Domino's, Starbucks y Subway.** 
  * Cadenas líderes del sector *Quick Service Restaurants* (QSR) que compiten directamente con KFC por:
      * **Perfiles profesionales:** Cajeros, cocineros, *shift leaders*, *store managers* y repartidores.
      * **Dinámicas laborales homogéneas:** Estructuras de salarios de entrada, turnos rotativos, alta intensidad de servicio, retos de conciliación familiar y expectativas de promoción interna.


| Sección | Contenido |
|:---:|---|
| 0 | Carga y preparación de datos |
| 1 | EDA |
| 2 | Sentiment Analysis con DistilBERT  |
| 3 | Topic Modeling con BERTopic|
| 4 | Comparación con Peers|
| 5 | Análisis por Empleado Actuales vs. Antiguos |
| 6 | Matriz de Priorización de RRHH |
| 7 | Conclusiones, recomendaciones para RRHH y limitaciones del análisis |

## 0. Carga y preparación de datos

* Target: KFC
* Peers: McDonald's, Domino's, Starbucks y Subway

---
### Limpieza y Variables Derivadas

 Crear variables: 
- 'tipo_empleado'("Current Employe = Actual", "Former Employe = Antiguo", "Otros = Desconocido") 
- 'anios_antiguedad'(# años) basado en la columna "current"
- 'recomienda'('v=Sí', 'o=Neutral', 'x=No') basado en la columna 'recommend'.

 Limpieza de texto pros y cons

 ---
## 1. EDA

* Métricas por empresa
* Rating actuales vs antiguos
* Evolución temporal del rating
### Interpretación EDA
- Empleados actuales → presenta los ratings medios más altos.
- Rating temporal
    Starbucks-> el mejor rating,
    KFC -> un rating relativamente estable.


---
## 2. Sentiment Analysis con DistilBERT

- Control de calidad para verificar que el sentimiento predominante en pros es el positivo y en cons es en negativo.
- Utilizar  `distilbert-base-uncased-finetuned-sst-2-english` (POSITIVE / NEGATIVE, sin clase neutral) con `truncation=True`.
El control de calidad con DistilBERT confirma la fiabilidad del dataset de Glassdoor: 
- los Pros registran un ~88% de polaridad positiva 
- los Cons un ~84-85% negativa,
- con un comportamiento prácticamente idéntico entre KFC y la competencia (Domino's, McDonald's, Starbucks y Subway).

- ---
## 3. Topic Modeling con BERTopic
- Aplicar BERTOPIC (Ejecución del modelo)
- Asignación de Etiquetas de Negocio (Diccionarios)
- Revisión de Comentarios por Tema (Validación)

---
### 4. COMPARACIÓN CON PEERS Y BALANCE NETO
- Tabla Comparativa de Balance Neto (% PROS - % CONS) 
- Gráfico de Gap Competitivo (PROS y CONS por separado)
- Gráfico de Gap de Balance Neto

Desglose de Pros y Cons por Separado:
Permite auditar si los gaps competitivos se explican por el volumen de elogios o por la concentración de quejas.
* En PROS (Fortalezas): Confirma que la desventaja en *Beneficios y Flexibilidad (-3,83 pp)* no ocurre porque sea un tema negativo, sino porque los competidores (Starbucks/McDonald's) comunican con mayor éxito sus ventajas.
* En CONS (Quejas): Demuestra una paridad casi absoluta en *Salario, Horarios y Gestión (+0,22 pp)* entre KFC y sus competidores, confirmando que la insatisfacción con el sueldo de entrada y la rotación de turnos es un problema estructural de toda la industria QSR.

**Gap de Balance Neto:**
Este gráfico sintetiza la posición competitiva global de KFC en una sola métrica (% PROS − % CONS vs. Sector).
* Fortalezas: KFC lidera frente a sus competidores en Compañeros y Aprendizaje (+1,61 pp) y Producto y Descuentos (+1,22 pp), posicionando el buen clima laboral como su principal activo de marca empleadora.
* Áreas de Vulnerabilidad: Presenta su mayor rezago relativo en Beneficios y Flexibilidad (-3,83 pp) y una ligera desventaja en Salario, Horarios y Gestión (-0,22 pp). 
* Aunque Beneficios y Flexibilidad es un aspecto positive valorado internamente, la competencia lo implementa major.

---
## 5. Empleados actuales vs. antiguos

- Tablas Cruzadas de Quejas por Estado
- Gráfico Comparativo de Motivos de Salida
- Conclusiones de Retención (Markdown)
La nota media cae de **3.51** en empleados actuales a **3.18** en ex-empleados
  
**Salario, Horarios y Gestión** concentra el **85.93%** de las quejas en la plantilla activa y se eleva al **89.90%** en los trabajadores salientes.
### 6. MATRIZ DE PRIORIZACIÓN DE RRHH
- Gráfico Scatter de Matriz de Priorización (con adjustText)

* Salario, Horarios y Gestión representa el 88.2% del volumen total de insatisfacción y supera la media del sector en quejas (+0.2 pp).
* Problemas con la Empresa (4.6% del volumen) aunque el volumen es bajo, es la categoría con el gap desfavorable más abultado en quejas
- Fortalezas Operativas: El reparto y la carga física presentan menor incidencia negativa que en la competencia, actuando como elementos de estabilidad operativa.

### Analizar  si es posible separar el topic  "Salario, Horarios y Gestión" para entender cual es el que mas afecta.

---
## 7. Conclusiones y recomendaciones para RRHH

* **Puntos Fuertes (Ventajas Competitivas):**
  * **Buen clima laboral:** El ambiente entre compañeros y el aprendizaje en tienda destacan por encima de la competencia (**+1,61 pp**).
  * **Beneficios en producto:** La comida de personal y los descuentos corporativos son muy valorados (**+1,22 pp** vs. peers).
* **Áreas de Mejora (Riesgos Internos):**
  * **Salario, Horarios y Gestión:** Representa el **88,2% del total de quejas** en KFC y es el motivo de casi **9 de cada 10 salidas de empleados**.
  * **Flexibilidad de turnos:** Aunque es un punto apreciado internamente, la competencia ofrece mejor percepción de horarios (**-3,83 pp** por debajo del sector).
  * **Previsibilidad de Horarios:** Implementar cuadrantes de turnos rotativos con semanas de antelación para reducir la fatiga operativa.
