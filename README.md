# 🤖 Desafío: Predicción de Cancelación (Churn) — Telecom X (Machine Learning)

![Estado del Proyecto](https://img.shields.io/badge/Estado-Finalizado-success)
![Tecnologías](https://img.shields.io/badge/Tecnologías-Python%20%7C%20Scikit--Learn%20%7C%20XGBoost-orange)
![Modelo](https://img.shields.io/badge/Modelo-Random%20Forest%20--%20Champion-blue)

## 🎯 1. Objetivo del Proyecto
Tras el análisis exploratorio de la Parte 1, Telecom X evoluciona hacia una estrategia predictiva. El objetivo es desarrollar un **pipeline de Machine Learning** robusto capaz de predecir el *churn* de clientes, permitiendo transitar de una cultura reactiva a una proactiva.

### Objetivos específicos:
* **Tratamiento de Datos:** Pipeline de limpieza, codificación y normalización.
* **Manejo de Desbalance:** Comparativa entre técnicas de **Oversampling (SMOTE)** y **Undersampling**.
* **Modelado Avanzado:** Evaluación de múltiples arquitecturas (KNN, Decision Tree, Random Forest, SVM y XGBoost).
* **Validación Estadística:** Implementación de **Stratified K-Fold Cross-Validation** para asegurar la estabilidad del modelo.

---

## 🧠 2. Enfoque Metodológico
Se implementó un pipeline estructurado bajo el criterio de **maximización del Recall**:

* **Preprocesamiento:** `OneHotEncoding` para variables categóricas y estandarización para modelos basados en distancia (KNN/SVM).
* **Estrategia de Balanceo:** Se determinó que el **Undersampling** produce fronteras de decisión más nítidas y estables para este dataset en comparación con SMOTE.
* **Validación:** Uso de 5 pliegues (*folds*) para garantizar que las métricas sean representativas de todo el dataset y no de una partición afortunada.

---

## 🛠️ 3. Tecnologías Utilizadas

| Categoría | Herramientas / Librerías | Propósito Específico |
| :--- | :--- | :--- |
| **Lenguaje** | `Python 3.x` | Base del desarrollo del proyecto. |
| **Análisis de Datos** | `pandas`, `numpy` | Manipulación de DataFrames y operaciones vectoriales. |
| **Visualización** | `matplotlib`, `seaborn` | Gráficos estadísticos y visualización de importancia de variables. |
| **Preprocesamiento** | `OneHotEncoder`, `ColumnTransformer` | Codificación de variables categóricas y transformación modular. |
| **Modelado (Core)** | `Scikit-learn`, `XGBoost`, `SVM` | Entrenamiento de modelos de clasificación y ensambles. |
| **Pipeline y Flujo** | `sklearn.pipeline.Pipeline` | Automatización de la cadena de transformación y predicción. |
| **Validación Avanzada** | `StratifiedKFold`, `cross_val_score` | Validación cruzada robusta para asegurar la estabilidad. |
| **Balanceo de Clases** | `SMOTE`, `RandomUnderSampler` | Mitigación del sesgo de clases mediante sobre/submuestreo. |
| **Persistencia** | `pickle` | Exportación y serialización del modelo "Champion". |

---

## 📊 4. Evaluación de Experimentos y Resultados

Para seleccionar la mejor estrategia, se realizó una comparativa inicial evaluando el rendimiento puntual de los modelos combinados con técnicas de balanceo (SMOTE y Undersampling).

### A. Resultados de la Fase de Experimentación (Hold-out)
En esta fase se midió el impacto directo del balanceo en la matriz de confusión y métricas clave:

| Modelo + Estrategia | TP | TN | FN | FP | Recall | Precision | ROC-AUC |
| :--- | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| **RandomForest + SMOTE** | 457 | 1098 | 104 | 454 | **81.46%** | 50.16% | 0.834 |
| **RandomForest + Under** | 454 | 1101 | 107 | 451 | **80.93%** | 50.17% | 0.836 |
| XGBoost + Under | 451 | 1105 | 110 | 447 | 80.39% | 50.22% | 0.831 |
| SVM + Under | 438 | 1116 | 123 | 436 | 78.07% | 50.11% | 0.819 |
| XGBoost + SMOTE | 437 | 1123 | 124 | 429 | 77.90% | 50.46% | 0.831 |
| SVM + SMOTE | 428 | 1126 | 133 | 426 | 76.29% | 50.12% | 0.822 |
| KNN + Under | 332 | 1259 | 229 | 293 | 59.18% | 53.12% | 0.783 |
| KNN + SMOTE | 142 | 1430 | 419 | 122 | 25.31% | 53.79% | 0.754 |


### B. Validación Cruzada (La Prueba de Consistencia)
Debido a la cercanía en los resultados entre SMOTE y Undersampling para Random Forest, se aplicó **Stratified K-Fold** para determinar cuál técnica era más estable ante diferentes particiones de datos:

| Modelo (K-Folds) | Recall Promedio | Estabilidad (STD) | F1-Score | Estado |
| :--- | :--- | :--- | :--- | :--- |
| **Random Forest + Under** | **79.28%** | **±0.019** | **0.63** | **CHAMPION** |
| SVM + Under | 79.20% | ±0.007 | 0.62 | Finalista |
| KNN + SMOTE | 72.17% | ±0.026 | 0.55 | Descartado |

**Análisis de Selección:** Aunque SMOTE alcanzó un pico de Recall del 81.46% en la prueba inicial, el **Undersampling** demostró una mayor robustez y un mejor F1-Score general en la validación cruzada, lo que lo convierte en la opción más fiable para producción.

---

## 🔎 5. Factores Clave de Cancelación (Insights)
Basado en el atributo `feature_importances_` del modelo ganador:
1.  **Antigüedad (Tenure - 17.9%):** El mayor riesgo se concentra en los meses iniciales de contrato.
2.  **Métricas Financieras (Total/Monthly Charges - 27.3%):** Existe una alta sensibilidad al precio en los primeros ciclos de facturación.
3.  **Tipo de Contrato (2 Year - 7.9%):** Los contratos a largo plazo reducen drásticamente la probabilidad de fuga.
4.  **Servicios de Fibra Óptica:** Identificado como un segmento con mayor tasa de deserción, sugiriendo revisión de calidad o precio.

---

## 🚀 6. Recomendaciones Estratégicas
* **Fidelización Temprana:** Implementar programas de acompañamiento (*onboarding*) en los primeros 6 meses.
* **Migración de Pagos:** Fomentar el uso de pagos automáticos para reducir la fricción del "punto de decisión" mensual asociado al *Electronic Check*.
* **Estrategia de Bundling:** Promover servicios de valor agregado (`Online Security`, `Tech Support`) para aumentar el costo de cambio percibido.

---

## ⚙️ 7. Instalación y Uso
1.  Instalar dependencias: `pip install -r requirements.txt`
2.  Ejecutar el notebook: `telecom_x_parte2.ipynb`
3.  Cargar el modelo exportado:

```python
import pickle

# Cargar el diccionario que contiene el modelo y metadatos
with open('champion.pkl', 'rb') as f:
    data = pickle.load(f)

# Acceder a los componentes
model = data['model']
features = data['features']
```

## 🤝 8. Autoría
Proyecto desarrollado por Enrique como Analista Junior de Machine Learning para el desafío Telecom X.
