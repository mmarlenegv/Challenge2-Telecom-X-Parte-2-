# 📡 Proyecto Telecom X - Parte 2: Predicción de Evasión de Clientes (Churn)

![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-2C2D72?style=for-the-badge&logo=pandas&logoColor=white)
![Scikit-Learn](https://img.shields.io/badge/Scikit_Learn-F7931E?style=for-the-badge&logo=scikit-learn&logoColor=white)

## 🎯 1. Propósito del Análisis
Este proyecto representa la segunda fase del desafío **Telecom X**. Tras haber realizado la limpieza inicial de los datos, el objetivo principal de esta etapa es **predecir el Churn (cancelación de clientes)** utilizando técnicas de Machine Learning. 

A través del preprocesamiento avanzado, la codificación de variables y el balanceo de clases, se busca construir un modelo capaz de identificar qué clientes tienen un alto riesgo de abandonar la compañía en base a sus características demográficas y los servicios contratados, permitiendo así tomar decisiones estratégicas de retención.

---

## 📂 2. Estructura del Proyecto

El repositorio está organizado de la siguiente manera para facilitar su reproducibilidad:

```text
📁 Telecom-X-Parte2/
│
├── 📄 Notebook_TelecomX_Parte2.ipynb  # Cuaderno principal con el código ETL, EDA y Modelado.
├── 📁 data/
│   └── 📊 datos_tratados.csv          # Dataset limpio base utilizado en el análisis.
├── 📁 visualizaciones/                # Carpeta destinada a guardar los gráficos generados (.png).
└── 📄 README.md                       # Documentación y justificación técnica del proyecto.
```
---

## ⚙️ 3. Preparación de los Datos
Para que los algoritmos de Machine Learning pudieran interpretar la información, el dataset (datos_tratados.csv) pasó por una transformación rigurosa:

Clasificación de Variables
Variables Numéricas: Tenure (antigüedad), ChargesDaily, ChargesMonthly, ChargesTotal.

Variables Categóricas: Gender, Partner, Dependents, InternetService, Contract, PaymentMethod, y múltiples variables de servicios adicionales (ej. OnlineSecurity, TechSupport).

Etapas de Normalización y Codificación
Unificación de Categorías: Se estandarizaron las respuestas redundantes. Valores como "No internet service" o "No phone service" se reemplazaron globalmente por "No" para simplificar la información sin perder contexto.

Codificación Binaria (Mapeo): Variables con respuestas de Sí/No (incluyendo la variable objetivo Churn) y Gender (Male/Female) fueron transformadas a valores numéricos 1 y 0 utilizando diccionarios de mapeo manual (.map()).

One-Hot Encoding (Variables Dummy): Las variables categóricas complejas con más de dos opciones (como Contract o PaymentMethod) fueron transformadas en múltiples columnas binarias utilizando la función pd.get_dummies() de Pandas, evitando así jerarquías falsas en los datos.

---

## 📊 4. Análisis Exploratorio (EDA) e Insights
Durante la exploración visual de los datos, se identificaron factores críticos que impulsan la evasión:

El impacto del tipo de contrato: Los clientes con contratos de mes a mes (Month-to-month) tienen una tasa de cancelación drásticamente superior en comparación con los contratos de uno o dos años.

Ausencia de servicios de soporte: La falta de servicios adicionales como TechSupport (Soporte Técnico) u OnlineSecurity (Seguridad en línea) está fuertemente correlacionada con los clientes que deciden irse.

(💡 Nota: Puedes revisar los gráficos de correlación y distribución en la carpeta /visualizaciones de este repositorio).

---

## 🧠 5. Modelización y Decisiones Técnicas
El enfoque predictivo requirió tomar decisiones estadísticas clave para asegurar la fiabilidad del modelo:

Separación de los Datos
Se utilizó train_test_split para dividir el dataset (excluyendo la columna ID, que no aporta valor predictivo):

Conjunto de Entrenamiento (Train): 70% de los datos.

Conjunto de Prueba (Test): 30% de los datos (test_size=0.3), utilizando una semilla aleatoria (random_state=101) para garantizar resultados reproducibles.

Justificaciones Técnicas en el Modelado
Balanceo de Clases (SMOTE): El EDA reveló que había muchos más clientes que se quedaban frente a los que cancelaban (desbalance de clases). Para evitar que el modelo se volviera "perezoso" y predijera siempre la clase mayoritaria, se aplicó SMOTE (Synthetic Minority Over-sampling Technique) exclusivamente en el set de entrenamiento. Esto generó datos sintéticos para equilibrar ambas clases.

Selección del Modelo (Regresión Logística): Se optó por una LogisticRegression debido a que el problema es de clasificación binaria (Churn: Sí o No). Es un modelo altamente interpretable que permite entender el peso real de cada variable en el resultado final, logrando una precisión (Accuracy) sólida en los datos de prueba.

----

## 💻 6. Instrucciones de Ejecución

Este proyecto no requiere el uso de consola o terminal de comandos para ser explorado. Tienes tres opciones sencillas para revisarlo:

**Opción 1: Visualización rápida en GitHub**
Haz clic en el archivo `Notebook_TelecomX_Parte2.ipynb` dentro de este repositorio. GitHub renderizará automáticamente todo el código, los gráficos y los resultados para que puedas leer el informe directamente en tu navegador.

**Opción 2: Ejecución en Google Colab (Recomendado)**
1. Descarga el archivo `datos_tratados.csv` de la carpeta `data/` de este repositorio.
2. Descarga el archivo `.ipynb`.
3. Sube el archivo `.ipynb` a [Google Colab](https://colab.research.google.com/).
4. En el menú izquierdo de Colab, ve a la sección de "Archivos" y sube el `datos_tratados.csv`.
5. Ejecuta las celdas secuencialmente. *(Nota: Colab ya trae preinstaladas casi todas las librerías, solo asegúrate de ejecutar `!pip install imbalanced-learn` si el entorno te lo pide para usar SMOTE).*

**Opción 3: Descarga manual para Jupyter Notebook local**
1. Haz clic en el botón verde **"<> Code"** en la parte superior derecha de este repositorio.
2. Selecciona **"Download ZIP"** y extrae los archivos en tu computadora.
3. Abre el archivo `.ipynb` con tu entorno de Jupyter Notebook.
4. Asegúrate de tener instaladas las dependencias (`pandas`, `matplotlib`, `seaborn`, `scikit-learn`, `imbalanced-learn`).

---

Desarrollado con 💙 y datos por *[Marlene Galvez/mmarlenegv]*
