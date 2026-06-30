# Talleres de Aprendizaje No Supervisado: Clustering, Reducción de Dimensionalidad y Detección de Anomalías

Este repositorio contiene dos talleres prácticos dedicados al **Aprendizaje No Supervisado**, estructurados para comparar el comportamiento de los algoritmos según la naturaleza de los datos: variables puramente categóricas frente a variables puramente numéricas.

---

## 📋 Estructura del Proyecto

El proyecto se compone de los siguientes cuadernos de Jupyter y sus correspondientes conjuntos de datos:

1. **`workshop_clustering_Mushrooms.ipynb`**: Taller centrado en datos categóricos (Dataset de Setas).
2. **`workshop-clustering-creditcard.ipynb`**: Taller centrado en datos numéricos y segmentación de negocio (Dataset de Tarjetas de Crédito).
3. **`mushrooms.csv`**: Datos con características morfológicas y ecológicas de diferentes especies de setas.
4. **`credit_card.csv`**: Datos de comportamiento financiero de ~9,000 usuarios de tarjetas de crédito.

---

## 🍄 Parte 1: Dataset de Setas (Variables Categóricas)
**Cuaderno:** `workshop_clustering_Mushrooms.ipynb`

### Descripción
Este taller aborda un problema clásico utilizando el Mushroom Dataset. Contiene información sobre características visuales y olfativas de setas, clasificadas como comestibles (`e`) o venenosas (`p`). 

> ⚠️ **Enfoque No Supervisado:** Aunque el dataset incluye la etiqueta real (`class`), esta se oculta durante todo el proceso y **solo se utiliza al final para validar** los grupos que los algoritmos han descubierto de forma autónoma.

### Flujo de Trabajo
* **Preprocesamiento:** Tratamiento de nulos ocultos (como el carácter `?`), eliminación de características constantes y codificación de variables categóricas.
* **Reducción de Dimensionalidad:** Aplicación de **PCA** (lineal) y **t-SNE** (no lineal) para proyectar y visualizar un espacio de más de 100 dimensiones tras la codificación.
* **Clustering:** Implementación y optimización de **K-Means**, **Clustering Jerárquico Aglomerativo**, **Modelos de Mezcla Gaussiana (GMM)** y **DBSCAN**.
* **Evaluación:** Uso de métricas internas (Método del Codo, *Silhouette*, *Davies-Bouldin*, *Calinski-Harabasz*) y métricas externas de validación cruzada con la etiqueta real (**Adjusted Rand Index (ARI)** y **NMI**).
* **Detección de Anomalías:** Uso de **Isolation Forest** para localizar las setas con rasgos más atípicos.

---

## 💳 Parte 2: Segmentación de Clientes (Variables Numéricas)
**Cuaderno:** `workshop-clustering-creditcard.ipynb`

### Descripción
Este taller plantea un escenario real de analítica de negocio utilizando datos financieros de consumo de unos 9,000 titulares de tarjetas de crédito durante 6 meses (saldo, frecuencia de compras, adelantos de efectivo, límites de crédito, etc.).

> 🎯 **Aprendizaje No Supervisado Real:** A diferencia del taller de las setas, aquí **no existe ninguna etiqueta de referencia**. El éxito del modelo se basa en métricas internas de cohesión y, fundamentalmente, en la **interpretabilidad y valor de negocio** de los segmentos obtenidos.

### Flujo de Trabajo
* **Preprocesamiento Crítico:** Imputación de valores nulos y **escalado/estandarización** de los datos (fundamental debido a las drásticas diferencias de magnitud entre variables como `CREDIT_LIMIT` y `PURCHASES_FREQUENCY`).
* **Análisis Exploratorio:** Identificación de sesgos severos en las distribuciones financieras (gráficos de distribución).
* **Reducción de Dimensionalidad:** PCA para analizar la varianza explicada y t-SNE para la visualización final de los clústeres.
* **Clustering Avanzado:** K-Means (optimizado mediante curvas de Inercia y *Silhouette*), Dendrogramas jerárquicos y **DBSCAN** aplicado principalmente como detector de atípicos.
* **Interpretación de Negocio:** Generación de un *Heatmap de Perfiles de Cliente* (comparando las medias estandarizadas de cada grupo) para transformar los clústeres matemáticos en **segmentos de marketing accionables**.

---

## 🛠️ Tecnologías y Librerías Utilizadas

Los cuadernos están desarrollados en **Python 3** utilizando el stack científico estándar:
* **Manipulación de datos:** `pandas`, `numpy`
* **Visualización:** `matplotlib`, `seaborn`
* **Machine Learning No Supervisado:** `scikit-learn`

---

## 📈 Conclusiones Clave de los Talleres

* **La importancia del Preprocesamiento:** Los datos numéricos requieren escalado obligatorio para evitar que las variables con magnitudes grandes dominen los cálculos de distancia, mientras que los categóricos exigen estrategias de codificación adecuadas.
* **DBSCAN y la densidad:** DBSCAN demostró que los datos financieros forman una nube continua en lugar de grupos densos separados, funcionando mejor como detector de *outliers*. En las setas, evidenció que la métrica de distancia seleccionada redefine por completo los límites del grupo.
* **Interpretabilidad vs. Validación Extrínseca:** Se trabaja el contraste entre evaluar un modelo con métricas de alineación externa (como el ARI en las setas) y evaluarlo mediante su utilidad práctica utilizando caracterización de perfiles (en las tarjetas de crédito).

Autores: Manuel Macarro de la Osa y Miguel Angel Moreno Delgado

