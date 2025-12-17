# Reporte de Resultados - Clasificación de Animals5

## 1. Introducción

Este proyecto tiene como objetivo clasificar imágenes de animales en 5 categorías utilizando técnicas de Deep Learning. El dataset **Animals5** contiene imágenes de: caballo (cavallo), elefante, gallina, vaca (mucca) y oveja (pecora).

Se probaron diferentes enfoques, desde redes neuronales creadas desde cero hasta el uso de modelos pre-entrenados (Transfer Learning), para comparar su rendimiento y determinar cuál es la mejor estrategia.

## 2. Metodología

### Preparación de Datos
El dataset fue dividido de forma balanceada:
- **Entrenamiento**: 723 imágenes por clase (50%)
- **Validación**: 361 imágenes por clase (25%)
- **Prueba**: 362 imágenes por clase (25%)
- **Total por clase**: 1,446 imágenes

### Modelos Implementados

| # | Modelo | Descripción |
|---|--------|-------------|
| 1 | CNN Básica | Red neuronal simple con 3 capas convolucionales |
| 2 | CNN Compleja | Agregamos BatchNormalization y Dropout para evitar sobreajuste |
| 3 | Data Augmentation | Rotación y zoom aleatorio para aumentar variedad de datos |
| 4a | MobileNetV2 | Modelo pre-entrenado liviano, con ajuste fino |
| 4b | ResNet50 | Modelo pre-entrenado más profundo, con ajuste fino |

## 3. Resultados

### Tabla Comparativa de Precisión (Accuracy) en Test

| Modelo | Estrategia | Accuracy (Test) | Observaciones |
|--------|------------|-----------------|---------------|
| **CNN Básica** | Desde cero | **57.90%** | Mejor modelo personalizado |
| **CNN Compleja** | BN + Dropout | 41.77% | Regularización excesiva |
| **CNN Aumentada** | Data Augmentation | 30.17% | Datos insuficientes para beneficiarse |
| **MobileNetV2** | Feature Extraction | 94.25% | Excelente con base congelada |
| **MobileNetV2** | Fine Tuning | 17.46% | Degradación por sobreajuste |
| **ResNet50** | Feature Extraction | 95.91% | Mejor Feature Extraction |
| **ResNet50** | Fine Tuning | **96.69%** | ⭐ **Mejor modelo general** |

### Resumen por Clase (Mejor Modelo: ResNet50 Fine-Tuned)

| Clase | Precisión | Recall | F1-Score |
|-------|-----------|--------|----------|
| Caballo | 97% | 96% | 96% |
| Elefante | 98% | 98% | 98% |
| Gallina | 99% | 98% | 99% |
| Vaca | 94% | 94% | 94% |
| Oveja | 95% | 97% | 96% |
| **Promedio** | **97%** | **97%** | **97%** |

## 4. Análisis de Resultados

### CNNs Personalizadas
- La **CNN Básica** logró el mejor resultado entre los modelos desde cero (57.90%).
- La adición de BatchNormalization y Dropout en **CNN Compleja** empeoró el rendimiento, posiblemente debido a que la regularización fue demasiado agresiva para el tamaño del dataset.
- **Data Augmentation** no mejoró los resultados; el modelo requiere más épocas de entrenamiento o una arquitectura más robusta.

### Transfer Learning
- **MobileNetV2 Feature Extraction** alcanzó 94.25%, demostrando que los modelos pre-entrenados capturan características útiles.
- El Fine Tuning de MobileNetV2 causó una degradación severa (17.46%), lo cual indica sobreajuste o problemas con la tasa de aprendizaje.
- **ResNet50** fue el mejor modelo en todas las métricas:
  - Feature Extraction: 95.91%
  - Fine Tuning: **96.69%** (mejor resultado)

## 5. Conclusiones

1. **Transfer Learning supera ampliamente a las CNNs desde cero** para este dataset de tamaño mediano.
2. **ResNet50 con Fine Tuning** es el modelo recomendado, logrando 96.69% de precisión.
3. Para datasets pequeños/medianos, **Feature Extraction** es una estrategia segura y efectiva.
4. El Fine Tuning debe realizarse con cuidado (tasa de aprendizaje muy baja) para evitar sobreajuste.
5. Las CNNs personalizadas pueden mejorar con más épocas de entrenamiento y ajuste de hiperparámetros.

---
*Proyecto realizado como parte del curso de Sistemas Inteligentes - 8vo Semestre*
