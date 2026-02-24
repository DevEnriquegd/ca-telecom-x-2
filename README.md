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
| Librería | Propósito |
| :--- | :--- |
| **pandas / numpy** | Manipulación y Feature Engineering. |
| **scikit-learn** | Pipeline de ML, métricas y validación cruzada. |
| **XGBoost** | Modelo de boosting de gradiente para comparación de rendimiento. |
| **imblearn** | Balanceo de clases (SMOTE, Undersampling). |
| **pickle** | Serialización del modelo "Champion". |

---

## 📊 4. Evaluación de Modelos y Resultados Finales
Se priorizó el **Recall** (Sensibilidad) para minimizar los Falsos Negativos, dado que el costo de perder un cliente es superior al de una campaña de retención.

### Comparativa de Validación Cruzada (K-Folds)
| Modelo | Recall Promedio | Estabilidad (STD) | F1-Score |
| :--- | :---: | :---: | :---: |
| **Random Forest + Under** | **79.28%** | **±0.019** | **0.63** |
| SVM + Undersampling | 79.20% | ±0.007 | 0.62 |
| XGBoost + Undersampling | 75.61% | ±0.024 | 0.61 |
| KNN + SMOTE | 72.17% | ±0.026 | 0.55 |

**🏆 Champion Model:** `Random Forest + Undersampling`. 
Este modelo logra capturar aproximadamente el **80% de las cancelaciones reales**, manteniendo un equilibrio óptimo entre precisión y sensibilidad.

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
# El archivo exportado contiene un diccionario con el modelo y los nombres de las features
with open('champion.pkl', 'rb') as f:
    data = pickle.load(f)
    model = data['model']
```
