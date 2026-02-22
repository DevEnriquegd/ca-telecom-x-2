# 🤖 Desafío: Predicción de Cancelación (Churn) — Telecom X Parte 2

![Estado del Proyecto](https://img.shields.io/badge/Estado-Finalizado-success)
![Tecnologías](https://img.shields.io/badge/Tecnologías-Python%20%7C%20Scikit--Learn-orange)
![Modelo](https://img.shields.io/badge/Modelo-Random%20Forest-blue)

## 🎯 1. Objetivo del Proyecto
Tras el análisis exploratorio de la Parte 1, Telecom X evoluciona hacia una estrategia predictiva. El objetivo es desarrollar un **modelo de clasificación binaria** capaz de identificar clientes con alta probabilidad de cancelar sus servicios (*churn*), permitiendo a la empresa actuar de forma preventiva.

### Objetivos específicos:
* **Tratamiento de Datos:** Codificación y normalización de variables.
* **Ingeniería de Características:** Análisis de correlación y selección de variables.
* **Modelado:** Entrenamiento y comparación de modelos (KNN, Trees, Ensemble).
* **Optimización:** Aplicación de técnicas de balanceo (SMOTE / Undersampling).

---

## 🧠 2. Enfoque Metodológico
Se implementó un pipeline de Machine Learning estructurado:

* **Preprocesamiento:** Eliminación de IDs, codificación de booleanas y `OneHotEncoding` para variables multiclase.
* **División de Datos:** `train_test_split` estratificado (73% Activos / 27% Churn).
* **Tratamiento del Desbalance:** Se experimentó con **SMOTE** y **RandomUndersampling** para corregir el sesgo hacia la clase mayoritaria.

---

## 🛠️ 3. Tecnologías Utilizadas
| Librería | Propósito |
| :--- | :--- |
| **pandas / numpy** | Manipulación y transformación de datos. |
| **matplotlib / seaborn** | Visualización estadística y de importancia. |
| **scikit-learn** | Modelado, métricas y validación cruzada. |
| **imblearn** | Balanceo de clases (SMOTE, Undersampling). |
| **pickle** | Exportación del modelo Champion. |

---

## 📊 4. Evaluación de Modelos
| Modelo | Recall (Churn) | Precision (Churn) | ROC-AUC |
| :--- | :---: | :---: | :---: |
| KNN | 50.4% | 52.1% | 0.764 |
| Decision Tree | 62.0% | 58.9% | 0.825 |
| Random Forest | 51.3% | 64.2% | 0.837 |
| KNN + Undersampling | 77.1% | 46.3% | 0.784 |
| **RandomForest + Undersampling** | **78.2%** | **51.2%** | **0.836** |

**🏆 Modelo Seleccionado:** `RandomForest + Undersampling`. 
Se priorizó el **Recall** para minimizar los Falsos Negativos, asegurando que el 78% de los clientes en riesgo sean detectados por el equipo de retención.

---

## 🔎 5. Variables Más Influyentes
El modelo identifica los siguientes factores como los mayores predictores de abandono:
1.  **Antigüedad (Tenure):** El riesgo es crítico en los primeros 6-12 meses.
2.  **Cargos (Total/Mensual):** Sensibilidad económica alta en clientes nuevos.
3.  **Internet (Fibra Óptica):** Mayor tasa de deserción comparado con DSL.
4.  **Contrato Mensual:** Falta de barreras de salida contractuales.

---

## 🚀 6. Impacto Estratégico y Recomendaciones
* **Onboarding:** Seguimiento intensivo en el primer semestre de vida del cliente.
* **Migración Contractual:** Incentivos para pasar de contratos mensuales a anuales.
* **Bundling:** Promover servicios de valor (Tech Support, Security) para aumentar la lealtad.
* **Pagos:** Fomentar el débito automático para reducir la fricción mensual del pago manual.

---

## ⚙️ 7. Instalación y Uso
1.  Instalar dependencias: `pip install -r requirements.txt`
2.  Ejecutar el notebook: `telecom_x_parte2.ipynb`
3.  Cargar el modelo exportado:
```python
import pickle
with open('champion_model_rf.pkl', 'rb') as f:
    model = pickle.load(f)
```

## 🤝 8. Autoría
Proyecto desarrollado por Enrique como Analista Junior de Machine Learning para el desafío Telecom X.
