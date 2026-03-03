# PROYECTO RIDEFARE
## 1. Objetivo
Realizar un análisis exploratorio de datos (EDA) integrado sobre el dataset de viajes (rides) 
y el dataset meteorológico (weather) para comprender la estructura, calidad y contenido de ambas
fuentes, identificar problemas de integridad (valores nulos, duplicados, outliers), y caracterizar
la distribución y patrones de las variables numéricas y categóricas. A partir de este EDA, explorar
y cuantificar posibles relaciones entre características del viaje, condiciones climáticas y precio,
generar visualizaciones que evidencien tendencias y anomalías, y formular hipótesis de negocio sobre
los factores que influyen en el precio y la demanda del servicio, dejando la base lista para futuros
modelos predictivos y análisis avanzados.

## 2. Actividades principales 
 ## **2.1 Exploración inicial del dataset**

- **Dataset de viajes (rides)** Contiene aproximadamente 693.071 registros y 10 columnas, con 
información como distancia del viaje, tipo de servicio (cab_type), timestamp, origen, destino, 
precio, multiplicador de tarifa dinámica (surge_multiplier) e identificadores. 

- **Dataset meteorológico (weather)** Contiene alrededor de 6.276 registros y 8 columnas, con 
variables como temperatura (temp), ubicación (location), cobertura de nubes (clouds), presión 
atmosférica (pressure), lluvia (rain), humedad (humidity) y viento (wind). Se revisaron las 
dimensiones de cada dataset, los nombres de columnas y los tipos de datos, verificando la presencia 
de variables numéricas y categóricas. Asimismo, se generaron estadísticas descriptivas (media, 
mediana, desviación estándar, mínimo, máximo y percentiles) para las variables numéricas, lo que 
permitió detectar rangos de valores y posibles casos atípicos desde una primera aproximación.

## **2.2 Evaluación de la calidad de datos**

- **Valores nulos:** En el dataset de rides se identificó que la columna price presenta 55.095 valores 
nulos, lo que representa aproximadamente el 7,95 % del total de registros. – En el dataset de 
weather se encontró que la columna rain tiene 5.382 valores nulos, equivalente a un 85,76 % de 
los registros. Esto indica que la variable de precipitación está fuertemente incompleta en la fuente 
meteorológica, mientras que el precio presenta vacíos relevantes en la base de viajes.

- **Valores duplicados:**Se revisaron posibles duplicados (No se existen duplicados)considerando combinaciones de 
columnas clave (por ejemplo, ubicación y timestamp o identificadores de viaje). Esta revisión 
permite garantizar que las observaciones analizadas correspondan a eventos únicos y que no se 
dupliquen artificialmente ciertas transacciones. 

- **Conversión de tipos de datos:** La columna time_stamp fue convertida a formato datetime 
para facilitar el análisis temporal y posterior creación de variables derivadas (como franjas horarias 
o agrupaciones por día/hora). Se verificó, además, la consistencia entre las distintas columnas 
numéricas, ajustando tipos cuando fue necesario.

## **3. Análisis**
Una parte central del trabajo consistió en analizar la distribución de las variables relevantes, tanto 
numéricas como categóricas. Para el dataset de rides se estudiaron principalmente: 
- La distribución de la distancia de los viajes. 
- La distribución de cab_type y del tipo de servicio específico (name). 
- La distribución del precio, identificando diferencias entre categorías de servicio. Se utilizaron 
diversas visualizaciones, tales como:

### **a. Mapa de calor de correlaciones:** 
Permitió visualizar las relaciones lineales entre variables como distancia, precio, multiplicador de surge y características climáticas.

<img width="796" height="684" alt="6edb0a9b-ade2-47cc-9f6a-49eebd491c77" src="https://github.com/user-attachments/assets/7d69a4ef-c5a3-430c-a0e1-96b3dd0becd2" />

### **b. Histograma de distancias:**
Se evidenció que la mayoría de los viajes se concentran en distancias cortas, con una cola hacia valores mayores que representan trayectos más largos.

<img width="1389" height="490" alt="25efb2ef-27b4-443c-a30a-ec35f70433ee" src="https://github.com/user-attachments/assets/0e3e0422-7390-4fbb-8072-c64b65282322" />

### **c. Boxplot de precios::**
Permitió comparar la distribución de precios entre 
las distintas categorías, visualizando diferencias en medianas, dispersión y presencia de 
valores atípicos. Estas visualizaciones facilitaron la comprensión de cómo varían los precios 
según el tipo de viaje y la distancia, y cómo se comportan las variables numéricas clave dentro 
del conjunto de datos.

<img width="587" height="489" alt="a72b72a2-d1f2-427a-96a6-5ab16dad6d69" src="https://github.com/user-attachments/assets/a89914cc-243d-4a5f-9590-c8dd47559f73" />


## **4. Insights**
### **🌟4.1. La mayoría de viajes son cortos**

El histograma de distancias muestra que la mayor parte de los viajes se 
concentran en distancias cortas. 

<img width="1189" height="590" alt="085b8b33-a667-47b9-abb0-9a17d41d956d" src="https://github.com/user-attachments/assets/37b8c34e-f60d-440f-8f66-390406fbde12" />

**Interpretación:**
- El servicio se usa principalmente para movilidad urbana.
- Los viajes largos son menos frecuentes y suelen asociarse a servicios premium. 
- Esto explica por qué la mayoría de precios se concentran en rangos bajos medios.
  


### **🌟4.2. Lyft es más costoso y más variable que Uber**

**Diferencias entre servicios:**
- **Lyft** tiene precios ligeramente más altos en promedio ($17.35 vs $16.68 de Uber)
- **Uber** muestra mayor concentración de precios (mediana $13.00 vs $16.50 de Lyft)
- **Dispersión**: Lyft tiene mayor variabilidad ($10.02 vs $7.94 de desviación estándar)

<img width="1189" height="675" alt="5d065123-cf2e-423b-87f6-f0a66e4c9fcf" src="https://github.com/user-attachments/assets/b08a964a-0686-44d5-8ce8-25105bb0a1cb" />

**Comparación de precios**
 |Lyft: Media=$17.35 | Mediana=$16.50 | Q1=$9.00 | Q3=$22.50 | 
 |---|---|---|---|
  | Uber: Media=$15.72 | Mediana=$13.00 | Q1=$9.50 | Q3=$19.50 |
  
  **Análisis de cuartiles:**
- **Q1-Q3 de Lyft**: $9.00 - $22.50 (rango intercuartílico más amplio)
- **Q1-Q3 de Uber**: $9.50 - $19.50 (rango más compacto)
- Ambos servicios tienen Q1 similar (~$9), pero Lyft alcanza Q3 más alto
 **Outliers:**
- Ambos servicios presentan numerosos outliers hacia valores altos (>$42)
- Lyft muestra mayor cantidad de valores extremos, consistente con su mayor variabilidad
- Estos outliers corresponden a viajes largos o servicios premium detectados en análisis previos



### 🌟4.3. UberX y Lyft son los servicios más usados

Los servicios estándar (UberX, Lyft) dominan el mercado, mientras que los servicios premium tienen menor volumen, pero precios más altos.

<img width="1389" height="690" alt="602fd955-52f2-48b5-ad91-dd38b00c125f" src="https://github.com/user-attachments/assets/ad853b65-ba5f-47cb-90df-d216aa7e1970" />

La competencia real está en las categorías económicas. 



### 🌟4.4. Existe una relación positiva entre distancia y precio


  <img width="790" height="490" alt="dcebe8a5-b424-4ade-990a-763a93d26fc6" src="https://github.com/user-attachments/assets/2650f987-a176-4102-8747-c16a053fbb22" />

El scatterplot confirma que una **relación positiva clara**: a mayor distancia, mayor precio del viaje
La pendiente visual confirma que la distancia es uno de los factores más importantes en la determinación del precio.
Esta evidencia respalda la lógica de un modelo de precios basado en distancia + tarifa base.

  ### 🌟4.5. Variación del precio según la hora del día
  
<img width="790" height="390" alt="98f6324f-d5ba-40d2-a635-fea09ec5824c" src="https://github.com/user-attachments/assets/85788aa7-dc75-4c29-99b0-b25f63f1148f" />

- Se identifican horas con precios promedio más altos, usualmente coincidiendo con **horas pico** (mañana y tarde-noche).
- En horas de menor demanda (madrugada) los precios tienden a ser más bajos y estables.
- Este patrón respalda la hipótesis de que la demanda y la congestión influyen en el precio final del viaje.
- Esta información es útil para planificar oferta de vehículos y diseñar promociones en horarios de baja demanda.

### 🌟4.6. La lluvia aumenta ligeramente los precios


<img width="1389" height="490" alt="fa10e8e7-6da3-4202-97bf-7cd6dd43660b" src="https://github.com/user-attachments/assets/19eb3498-4373-4eef-9440-3984d7c8a487" />


Cuando hay lluvia CON baja visibilidad (mucha nubosidad), el precio aumenta hasta un 8-10% más que en condiciones normales. La visibilidad SOLA 
(sin lluvia) NO afecta el precio, pero COMBINADA con lluvia sí.

## **5. Conclusiones Finales**

- La distancia del viaje es la variable que más influye en el precio, con una relación positiva clara.
- Lyft tiende a mostrar precios más altos y más variables que Uber, aunque ambos compiten en el segmento económico de entrada.
- La mayoría de los viajes son de corta distancia, lo que confirma que el servicio se usa principalmente para desplazamientos urbanos.
- Las condiciones climáticas (especialmente la lluvia) están asociadas a ligeros incrementos en el precio promedio, posiblemente por
  demanda y tarifas dinámicas.
- Existen diferencias de precio según la hora del día, con horas pico más costosas que las horas de baja demanda.

Estas conclusiones permiten comprender mejor el comportamiento de precios en servicios de movilidad tipo Uber/Lyft y sirven como base para futuros modelos predictivos y decisiones de negocio.


## **6. Recomendaciones**
- Crear un modelo de predicción de precios utilizando distancia + cab_type + 
clima. 
- Estudiar elasticidad de demanda por tipo de servicio. 
- Incorporar análisis geográfico usando mapas (heatmaps de origen/destino). 
- Combinar precio con el tiempo de espera para entender experiencia del 
usuario.
