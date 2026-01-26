## INTELIGENCIA ARTIFICIAL

**¿De qué trata?**
- Sistemas computacionales que imitan capacidades humanas
- Aprendizaje, razonamiento, percepción, toma de decisiones
- Procesamiento de lenguaje natural, visión por computadora
- Automatización de tareas cognitivas
- Modelos que mejoran con experiencia (datos)

**¿Por qué se utiliza?**
- Automatizar tareas repetitivas y complejas
- Analizar grandes volúmenes de datos (Big Data)
- Descubrir patrones invisibles para humanos
- Predicciones precisas (forecasting)
- Personalización de experiencias (recomendaciones)
- Reducir errores humanos
- Disponibilidad 24/7 (chatbots, asistentes)

**Ventajas/Beneficios:**
- **Escalabilidad:** Procesa millones de datos simultáneamente
- **Velocidad:** Análisis en tiempo real
- **Precisión:** Supera humanos en tareas específicas (reconocimiento imágenes)
- **Automatización:** Libera tiempo humano para tareas creativas
- **Disponibilidad continua:** Sin descansos ni horarios
- **Adaptabilidad:** Aprende de nuevos datos
- **Detección de anomalías:** Fraude, fallos, enfermedades

**Desventajas:**
- **Costo inicial alto:** Hardware (GPUs), datos, talento
- **Requiere grandes datasets:** Sin datos suficientes, falla
- **Caja negra:** Difícil explicar decisiones (especialmente deep learning)
- **Sesgos:** Aprende sesgos de datos de entrenamiento
- **Falta de sentido común:** Solo funciona en dominio entrenado
- **Desempleo:** Automatización reemplaza trabajos
- **Privacidad:** Requiere datos sensibles
- **Dependencia:** Sobreconfianza en sistemas automatizados

---

**Tipos de Inteligencia Artificial:**

### **1. Por Capacidad**

**ANI (Artificial Narrow Intelligence) - IA Débil**
```
Características:
- Especializada en tarea específica
- Supera humanos en dominio limitado
- No transfiere conocimiento a otros dominios

Ejemplos:
- Siri, Alexa (asistentes de voz)
- AlphaGo (juega Go, no puede jugar ajedrez)
- Reconocimiento facial
- Sistemas de recomendación (Netflix, Spotify)
- Diagnóstico médico (detecta cáncer en radiografías)

Estado: Actual (2026) - Toda IA existente
```

**AGI (Artificial General Intelligence) - IA Fuerte**
```
Características:
- Inteligencia a nivel humano
- Aprende cualquier tarea intelectual
- Razonamiento abstracto
- Transferencia de conocimiento entre dominios

Ejemplos: Ninguno (aún no existe)
Proyecciones: 2040-2060 (especulativo)
```

**ASI (Artificial Super Intelligence)**
```
Características:
- Supera inteligencia humana en todos los aspectos
- Creatividad, sabiduría, habilidades sociales
- Autoconciencia

Ejemplos: Ninguno (teórico)
Riesgos: Singularidad tecnológica
```

---

### **2. Por Funcionalidad**

**Máquinas Reactivas**
```
- No tienen memoria
- Reaccionan a situación actual
- No aprenden de experiencia pasada

Ejemplo: Deep Blue (ajedrez IBM, 1997)
```

**Memoria Limitada**
```
- Aprenden de datos históricos
- Memoria temporal
- Mayoría de IA actual

Ejemplo: Autos autónomos (Tesla)
- Detectan objetos (cámaras, sensores)
- Aprenden de millones de millas
- Predicen comportamiento de peatones
```

**Teoría de la Mente** (en desarrollo)
```
- Entienden emociones humanas
- Interacción social avanzada

Ejemplo: Robots sociales experimentales
```

**Autoconciencia** (teórico)
```
- Consciencia propia
- Emociones y autoconcepto

Estado: No existe
```

---

**Componentes de la IA:**

```
┌──────────────────────────────────────────────────────────┐
│                 INTELIGENCIA ARTIFICIAL                   │
├──────────────────────────────────────────────────────────┤
│                                                           │
│  ┌────────────────────────────────────────────────┐      │
│  │         MACHINE LEARNING (ML)                  │      │
│  │  ┌──────────────────────────────────────┐      │      │
│  │  │    DEEP LEARNING (DL)                │      │      │
│  │  │  - Neural Networks                   │      │      │
│  │  │  - CNN, RNN, Transformers            │      │      │
│  │  └──────────────────────────────────────┘      │      │
│  │                                                 │      │
│  │  - Supervised Learning                          │      │
│  │  - Unsupervised Learning                        │      │
│  │  - Reinforcement Learning                       │      │
│  └────────────────────────────────────────────────┘      │
│                                                           │
│  ┌────────────────────────────────────────────────┐      │
│  │  RAMAS ESPECIALIZADAS                          │      │
│  │  - NLP (Natural Language Processing)           │      │
│  │  - Computer Vision                             │      │
│  │  - Robotics                                    │      │
│  │  - Expert Systems                              │      │
│  └────────────────────────────────────────────────┘      │
└──────────────────────────────────────────────────────────┘
```

---

**Ciclo de Vida de Proyecto de IA:**

```
1. DEFINICIÓN DEL PROBLEMA
   - Objetivo: ¿Qué queremos predecir/clasificar?
   - Métricas de éxito: Accuracy, F1-score, etc.
   - Ejemplo: Predecir churn de clientes (sí/no)

2. RECOLECCIÓN DE DATOS
   - Fuentes: Bases de datos, APIs, web scraping, sensores
   - Cantidad: Mínimo miles de ejemplos
   - Ejemplo: Historial de clientes (edad, compras, interacciones)

3. EXPLORACIÓN Y PREPARACIÓN DE DATOS (EDA)
   - Análisis estadístico
   - Visualizaciones (matplotlib, seaborn)
   - Identificar valores faltantes, outliers
   - Feature engineering (crear nuevas variables)
   
   Ejemplo:
   - Datos faltantes: 20% sin edad → imputar con mediana
   - Outliers: Clientes con 10,000 compras → analizar
   - Nueva feature: "días_desde_ultima_compra"

4. LIMPIEZA Y TRANSFORMACIÓN
   - Manejo de valores nulos (imputación, eliminación)
   - Encoding de variables categóricas (one-hot, label encoding)
   - Normalización/Estandarización
   - Balanceo de clases (SMOTE si desbalanceado)
   
   Ejemplo:
   - Género (M/F) → One-hot encoding → [1,0] / [0,1]
   - Edad: 18-80 → Normalizar → 0-1
   - 90% no-churn, 10% churn → SMOTE para balancear

5. DIVISIÓN DE DATOS
   - Train: 70-80%
   - Validation: 10-15%
   - Test: 10-15%
   - Estratificación si desbalanceado

6. SELECCIÓN DE MODELO
   - Clasificación: Logistic Regression, Random Forest, XGBoost, Neural Network
   - Regresión: Linear Regression, SVR, Gradient Boosting
   - Clustering: K-means, DBSCAN
   - Empezar simple, aumentar complejidad

7. ENTRENAMIENTO
   - Ajustar parámetros (hyperparameters)
   - Cross-validation (k-fold)
   - Monitorear overfitting/underfitting
   
   Ejemplo:
   - Random Forest: n_estimators=100, max_depth=10
   - Train accuracy: 95%, Val accuracy: 85% → OK
   - Train accuracy: 99%, Val accuracy: 60% → Overfitting

8. EVALUACIÓN
   - Métricas apropiadas al problema
   - Confusion Matrix
   - Precision, Recall, F1-Score
   - ROC-AUC Curve
   - Comparar múltiples modelos

9. OPTIMIZACIÓN (Hyperparameter Tuning)
   - Grid Search
   - Random Search
   - Bayesian Optimization
   - AutoML (H2O, Auto-sklearn)

10. DEPLOYMENT
    - Serializar modelo (pickle, joblib, ONNX)
    - API REST (Flask, FastAPI)
    - Containerización (Docker)
    - Plataformas: AWS SageMaker, Azure ML, GCP AI Platform
    - Monitoreo en producción

11. MONITOREO Y MANTENIMIENTO
    - Detectar data drift (distribución de datos cambia)
    - Model drift (performance degrada)
    - Reentrenamiento periódico
    - A/B testing de versiones

12. RETROALIMENTACIÓN
    - Recopilar feedback de usuarios
    - Actualizar con nuevos datos
    - Mejorar features
    - Iterar
```

---

**Frameworks y Herramientas:**

**Machine Learning:**
```python
# Scikit-learn (ML tradicional)
from sklearn.ensemble import RandomForestClassifier
from sklearn.model_selection import train_test_split
from sklearn.metrics import accuracy_score

# XGBoost (Gradient Boosting)
import xgboost as xgb

# LightGBM (Microsoft)
import lightgbm as lgb

# CatBoost (Yandex - maneja categóricas)
import catboost as cb
```

**Deep Learning:**
```python
# TensorFlow + Keras
import tensorflow as tf
from tensorflow import keras

# PyTorch
import torch
import torch.nn as nn

# JAX (Google - investigación)
import jax
```

**NLP:**
```python
# Hugging Face Transformers (BERT, GPT)
from transformers import pipeline

# spaCy (NLP industrial)
import spacy

# NLTK (procesamiento de texto)
import nltk
```

**Computer Vision:**
```python
# OpenCV
import cv2

# Pillow (PIL)
from PIL import Image

# Albumentations (augmentation)
import albumentations as A
```

**Datos y Visualización:**
```python
# Pandas (manipulación de datos)
import pandas as pd

# NumPy (arrays numéricos)
import numpy as np

# Matplotlib (gráficos)
import matplotlib.pyplot as plt

# Seaborn (visualización estadística)
import seaborn as sns

# Plotly (interactivo)
import plotly.express as px
```

**Ambientes de Desarrollo:**
```
- Jupyter Notebook / JupyterLab
- Google Colab (gratis, GPUs)
- Kaggle Notebooks
- VS Code + Python extension
- PyCharm (IDE)
```

**Datasets Públicos:**
```
Imágenes:
- MNIST (dígitos escritos a mano)
- CIFAR-10 (10 categorías, 60k imágenes)
- ImageNet (1.4M imágenes, 1000 clases)
- COCO (detección de objetos)

Texto:
- IMDB (reviews de películas)
- 20 Newsgroups (categorización de texto)
- SQuAD (preguntas/respuestas)

Tabulares:
- Titanic (supervivencia)
- House Prices (predicción de precios)
- Credit Card Fraud (detección de fraude)

Fuentes:
- Kaggle Datasets
- UCI ML Repository
- Hugging Face Datasets
- TensorFlow Datasets
```

---

**Aplicaciones de IA:**

**1. Reconocimiento de Imágenes**
```
Usos:
- Desbloqueo facial (Face ID)
- Diagnóstico médico (detectar tumores)
- Control de calidad en manufactura
- Búsqueda de imágenes (Google Lens)
- Moderación de contenido (Facebook)

Tecnología: CNN (Convolutional Neural Networks)
Modelos: ResNet, VGG, Inception, EfficientNet
```

**2. Procesamiento de Lenguaje Natural**
```
Usos:
- Chatbots (atención al cliente)
- Traducción automática (Google Translate)
- Análisis de sentimientos (reviews)
- Generación de texto (ChatGPT)
- Resumen automático de documentos

Tecnología: Transformers, BERT, GPT
Modelos: GPT-4, BERT, T5, LLaMA
```

**3. Sistemas de Recomendación**
```
Usos:
- Netflix (películas/series)
- Spotify (música)
- Amazon (productos)
- YouTube (videos)

Tecnología: Collaborative Filtering, Content-based
Algoritmos: Matrix Factorization, Deep Learning
```

**4. Detección de Fraude**
```
Usos:
- Transacciones bancarias
- Seguros (claims fraudulentos)
- E-commerce (cuentas falsas)

Tecnología: Anomaly Detection
Algoritmos: Isolation Forest, Autoencoders
```

**5. Vehículos Autónomos**
```
Componentes:
- Computer Vision (detectar objetos)
- Sensor Fusion (cámaras, LiDAR, radar)
- Reinforcement Learning (toma de decisiones)
- Path Planning (navegación)

Empresas: Tesla, Waymo, Cruise
```

**Habilitación Básica:**
```bash
# 1. Instalar Python 3.8+
# 2. Crear entorno virtual
python -m venv venv
venv\Scripts\activate  # Windows

# 3. Instalar librerías base
pip install numpy pandas matplotlib seaborn scikit-learn

# 4. Instalar Jupyter
pip install jupyter
jupyter notebook

# 5. Para Deep Learning
pip install tensorflow  # o pip install torch torchvision

# 6. Para NLP
pip install transformers spacy

# 7. Primer script
# train_model.py
```

**Recursos de Aprendizaje:**
```
Cursos:
- Andrew Ng - Machine Learning (Coursera)
- Fast.ai - Practical Deep Learning
- Google ML Crash Course

Plataformas de Práctica:
- Kaggle Competitions
- Google Colab (gratis)
- Hugging Face Spaces

Documentación:
- Scikit-learn docs
- TensorFlow tutorials
- PyTorch tutorials
```

---

### Fundamentos y principios de la IA y sus ramas

**¿De qué trata?**
- Conceptos fundamentales de aprendizaje automático
- Ramas principales de IA y sus aplicaciones
- Principios matemáticos y estadísticos
- Arquitecturas y algoritmos clave

**¿Por qué se utiliza?**
- Entender cómo funcionan los modelos de IA
- Seleccionar algoritmo apropiado para problema específico
- Base para desarrollo e investigación en IA
- Comprender limitaciones y capacidades

---

## **MACHINE LEARNING (ML)**

**¿De qué trata?**
- Subconjunto de IA que aprende de datos
- Encuentra patrones sin ser explícitamente programado
- Mejora rendimiento con experiencia
- Base matemática: estadística, álgebra lineal, cálculo

**Paradigmas de Aprendizaje:**

### **1. Aprendizaje Supervisado (Supervised Learning)**

**Concepto:**
```
- Datos etiquetados: (X, y)
- X = features (características)
- y = label (etiqueta/target)
- Modelo aprende función: f(X) ≈ y

Analogía: Profesor (etiquetas) enseña a estudiante (modelo)
```

**Tipos:**

**a) Clasificación** (output discreto)
```
Objetivo: Predecir categoría/clase

Binaria:
- Spam o No Spam
- Fraude o Legítimo
- Sí o No

Multiclase:
- Dígito (0-9)
- Especie de flor (Iris: setosa, versicolor, virginica)
- Categoría de producto

Multilabel:
- Una imagen puede tener múltiples tags (perro + playa + atardecer)
```

**b) Regresión** (output continuo)
```
Objetivo: Predecir valor numérico

Ejemplos:
- Precio de casa ($100,000 - $1,000,000)
- Temperatura (°C)
- Ventas futuras
- Edad de persona
```

---

### **2. Aprendizaje No Supervisado (Unsupervised Learning)**

**Concepto:**
```
- Datos sin etiquetas: solo X
- Encontrar estructura oculta en datos
- Agrupar, reducir dimensionalidad, detectar anomalías

Analogía: Explorador descubre patrones por cuenta propia
```

**Tipos:**

**a) Clustering** (Agrupamiento)
```
Objetivo: Agrupar datos similares

Ejemplos:
- Segmentación de clientes (alto valor, medio, bajo)
- Agrupar documentos similares
- Genes con expresión similar
```

**b) Reducción de Dimensionalidad**
```
Objetivo: Reducir número de features manteniendo información

Usos:
- Visualización (3D → 2D)
- Compresión
- Eliminar ruido
- Acelerar entrenamiento
```

**c) Detección de Anomalías**
```
Objetivo: Encontrar datos atípicos

Ejemplos:
- Fraude
- Fallo de máquinas
- Intrusión en redes
```

---

### **3. Aprendizaje por Refuerzo (Reinforcement Learning)**

**Concepto:**
```
- Agente interactúa con ambiente
- Recibe recompensas/penalizaciones
- Aprende política óptima (qué acción tomar)

Componentes:
- Estado (state): situación actual
- Acción (action): decisión del agente
- Recompensa (reward): feedback
- Política (policy): estrategia de decisión

Analogía: Perro aprende trucos con premios
```

**Ejemplos:**
```
- AlphaGo (juega Go)
- Robots caminando
- Trading algorítmico
- Optimización de centros de datos (Google DeepMind reduce consumo energético 40%)
- Juegos (Dota 2, StarCraft)
```

---

## **RAMAS DE LA IA**

### **1. DEEP LEARNING (Aprendizaje Profundo)**

**¿De qué trata?**
- Redes neuronales con múltiples capas (profundas)
- Aprende representaciones jerárquicas
- Inspirado en neurona biológica
- Requiere muchos datos y poder computacional (GPUs)

**Arquitectura de Red Neuronal:**

```
Input Layer     Hidden Layers        Output Layer
     
 X1 ○────────┬──○────┬──○────┬───────○ Y1
            │       │       │
 X2 ○────────┼──○────┼──○────┼───────○ Y2
            │       │       │
 X3 ○────────┼──○────┼──○────┼───────○ Y3
            │       │       │
 X4 ○────────┴──○────┴──○────┘

Neurona:
  Inputs → Weighted Sum → Activation Function → Output
  
  z = w1*x1 + w2*x2 + ... + bias
  output = activation(z)
  
Funciones de Activación:
- ReLU: max(0, z)
- Sigmoid: 1 / (1 + e^(-z))
- Tanh: tanh(z)
- Softmax: para clasificación multiclase
```

**Tipos de Redes Neuronales:**

**a) Feedforward Neural Network (FNN)**
```python
import tensorflow as tf

model = tf.keras.Sequential([
    tf.keras.layers.Dense(128, activation='relu', input_shape=(784,)),
    tf.keras.layers.Dropout(0.2),
    tf.keras.layers.Dense(64, activation='relu'),
    tf.keras.layers.Dense(10, activation='softmax')
])

model.compile(
    optimizer='adam',
    loss='sparse_categorical_crossentropy',
    metrics=['accuracy']
)

# Entrenar
model.fit(X_train, y_train, epochs=10, batch_size=32, validation_split=0.2)

# Predecir
predictions = model.predict(X_test)
```

**b) Convolutional Neural Network (CNN)**
```
Uso: Computer Vision (imágenes)

Capas:
1. Convolución: Detecta features (bordes, texturas)
2. Pooling: Reduce dimensionalidad
3. Flatten: Convierte a vector
4. Dense: Clasificación

Arquitectura:
Input Image (28x28x1)
    ↓
Conv2D (32 filters, 3x3) + ReLU
    ↓
MaxPooling (2x2)
    ↓
Conv2D (64 filters, 3x3) + ReLU
    ↓
MaxPooling (2x2)
    ↓
Flatten
    ↓
Dense (128) + ReLU
    ↓
Dense (10) + Softmax
    ↓
Output (clase 0-9)

Ejemplo: Clasificar MNIST
```

```python
# CNN para clasificar imágenes
model = tf.keras.Sequential([
    tf.keras.layers.Conv2D(32, (3,3), activation='relu', input_shape=(28,28,1)),
    tf.keras.layers.MaxPooling2D((2,2)),
    tf.keras.layers.Conv2D(64, (3,3), activation='relu'),
    tf.keras.layers.MaxPooling2D((2,2)),
    tf.keras.layers.Flatten(),
    tf.keras.layers.Dense(128, activation='relu'),
    tf.keras.layers.Dense(10, activation='softmax')
])
```

**c) Recurrent Neural Network (RNN)**
```
Uso: Secuencias (texto, time series, audio)

Características:
- Memoria de estados anteriores
- Procesa secuencias de longitud variable

Variantes:
- LSTM (Long Short-Term Memory): Evita vanishing gradient
- GRU (Gated Recurrent Unit): Más simple que LSTM

Aplicaciones:
- Traducción automática
- Generación de texto
- Reconocimiento de voz
- Predicción de series temporales
```

```python
# LSTM para predicción de series temporales
model = tf.keras.Sequential([
    tf.keras.layers.LSTM(50, return_sequences=True, input_shape=(timesteps, features)),
    tf.keras.layers.LSTM(50),
    tf.keras.layers.Dense(25),
    tf.keras.layers.Dense(1)
])
```

**d) Transformer**
```
Uso: NLP (actualmente dominante)

Ventajas sobre RNN:
- Paralelizable (más rápido)
- Maneja dependencias de largo plazo
- Attention mechanism

Arquitectura:
- Self-Attention: Qué palabras son relevantes
- Positional Encoding: Orden de palabras
- Multi-Head Attention: Múltiples perspectivas

Modelos famosos:
- BERT (Google): Bidireccional, clasificación, Q&A
- GPT (OpenAI): Generativo, autoregresivo
- T5: Text-to-Text
- LLaMA: Open source (Meta)
```

**e) Generative Adversarial Network (GAN)**
```
Uso: Generar datos sintéticos (imágenes, audio)

Arquitectura:
  Generator                 Discriminator
      ↓                          ↓
  Ruido → Imagen Falsa      Real o Falso?
                ↓                 ↓
          Comparar y Entrenar Adversarialmente

Proceso:
1. Generator crea imagen falsa desde ruido
2. Discriminator clasifica (real/fake)
3. Generator mejora para engañar Discriminator
4. Discriminator mejora para detectar fakes
5. Equilibrio: Generator crea imágenes realistas

Aplicaciones:
- Deepfakes
- Style Transfer (artístico)
- Super-resolución (mejorar calidad)
- Generación de rostros (ThisPersonDoesNotExist.com)
```

**f) Autoencoder**
```
Uso: Compresión, reducción dimensionalidad, denoising

Arquitectura:
Input → Encoder → Latent Space (bottleneck) → Decoder → Output

Objetivo: Output ≈ Input

Variantes:
- Denoising Autoencoder: Input ruidoso → Output limpio
- Variational Autoencoder (VAE): Generativo, latent space estructurado

Aplicaciones:
- Compresión de imágenes
- Detección de anomalías
- Generación de datos
```

---

### **2. NATURAL LANGUAGE PROCESSING (NLP)**

**¿De qué trata?**
- Procesamiento y entendimiento de lenguaje humano
- Texto, voz, traducción, generación

**Tareas de NLP:**

**a) Clasificación de Texto**
```
- Análisis de sentimientos (positivo/negativo/neutral)
- Spam detection
- Categorización de noticias
- Detección de hate speech
```

**b) Named Entity Recognition (NER)**
```
Extractar entidades de texto:
"Elon Musk fundó Tesla en California"
- Persona: Elon Musk
- Organización: Tesla
- Lugar: California
```

**c) Traducción Automática**
```
Inglés → Español
"Hello world" → "Hola mundo"

Modelos: Google Translate (Transformer), DeepL
```

**d) Question Answering**
```
Contexto: "París es la capital de Francia..."
Pregunta: ¿Cuál es la capital de Francia?
Respuesta: París

Modelos: BERT, GPT, T5
```

**e) Text Generation**
```
Prompt: "La inteligencia artificial es"
Output: "...una rama de la informática que busca crear sistemas capaces de realizar tareas que normalmente requieren inteligencia humana..."

Modelos: GPT-4, Claude, LLaMA
```

**f) Resumen Automático**
```
Input: Artículo de 1000 palabras
Output: Resumen de 100 palabras

Tipos:
- Extractivo: Selecciona frases existentes
- Abstractivo: Genera nuevas frases
```

**Ejemplo: Análisis de Sentimientos**

```python
from transformers import pipeline

# Usar modelo pre-entrenado
sentiment_analyzer = pipeline("sentiment-analysis")

texts = [
    "Me encanta este producto, es increíble!",
    "Pésimo servicio, nunca vuelvo",
    "Es aceptable, nada especial"
]

results = sentiment_analyzer(texts)
print(results)
# [
#   {'label': 'POSITIVE', 'score': 0.9998},
#   {'label': 'NEGATIVE', 'score': 0.9995},
#   {'label': 'NEUTRAL', 'score': 0.8542}
# ]
```

**Preprocesamiento de Texto:**

```python
import nltk
from nltk.tokenize import word_tokenize
from nltk.corpus import stopwords
from nltk.stem import PorterStemmer, WordNetLemmatizer

texto = "Los gatos están corriendo por el jardín"

# 1. Tokenización
tokens = word_tokenize(texto.lower())
# ['los', 'gatos', 'están', 'corriendo', 'por', 'el', 'jardín']

# 2. Eliminar stopwords
stop_words = set(stopwords.words('spanish'))
filtered = [w for w in tokens if w not in stop_words]
# ['gatos', 'corriendo', 'jardín']

# 3. Stemming (raíz de palabra)
stemmer = PorterStemmer()
stemmed = [stemmer.stem(w) for w in filtered]
# ['gat', 'corr', 'jardín']

# 4. Lemmatization (forma base)
lemmatizer = WordNetLemmatizer()
lemmatized = [lemmatizer.lemmatize(w) for w in filtered]
# ['gato', 'correr', 'jardín']

# 5. Vectorización (texto → números)
from sklearn.feature_extraction.text import TfidfVectorizer

corpus = [
    "el gato come pescado",
    "el perro come carne",
    "el gato juega con el perro"
]

vectorizer = TfidfVectorizer()
X = vectorizer.fit_transform(corpus)
# Matriz TF-IDF: (documentos x vocabulario)
```

---

### **3. COMPUTER VISION**

**¿De qué trata?**
- Procesamiento y entendimiento de imágenes/videos
- Extrae información significativa de datos visuales

**Tareas de Computer Vision:**

**a) Clasificación de Imágenes**
```
Input: Imagen
Output: Clase (perro, gato, auto, etc.)

Arquitecturas: ResNet, VGG, EfficientNet, Vision Transformer
```

**b) Detección de Objetos**
```
Input: Imagen
Output: Bounding boxes + clases

Modelos:
- YOLO (You Only Look Once): Rápido, real-time
- Faster R-CNN: Más preciso, más lento
- SSD (Single Shot Detector)

Aplicación: Autos autónomos detectan peatones, señales, otros autos
```

**c) Segmentación**
```
Semántica: Clasificar cada pixel
- Cielo, carretera, edificio, persona

Instancia: Diferenciar instancias individuales
- Persona 1, Persona 2, Persona 3

Modelos: U-Net, Mask R-CNN
```

**d) Reconocimiento Facial**
```
Pasos:
1. Detección de rostro (Haar Cascades, MTCNN)
2. Alineación (normalizar orientación)
3. Embedding (convertir a vector)
4. Comparación (distancia coseno)

Modelos: FaceNet, ArcFace, DeepFace
Aplicación: Face ID, vigilancia, álbumes de fotos
```

**e) Pose Estimation**
```
Detectar puntos clave del cuerpo humano:
- Cabeza, hombros, codos, manos, rodillas, pies

Modelos: OpenPose, PoseNet
Aplicación: Fitness apps, animación, AR
```

**Ejemplo: Clasificación de Imágenes con Transfer Learning**

```python
import tensorflow as tf
from tensorflow.keras.applications import MobileNetV2
from tensorflow.keras.preprocessing.image import ImageDataGenerator

# 1. Cargar modelo pre-entrenado (ImageNet)
base_model = MobileNetV2(
    input_shape=(224, 224, 3),
    include_top=False,
    weights='imagenet'
)
base_model.trainable = False  # Congelar pesos

# 2. Añadir capas custom
model = tf.keras.Sequential([
    base_model,
    tf.keras.layers.GlobalAveragePooling2D(),
    tf.keras.layers.Dense(128, activation='relu'),
    tf.keras.layers.Dropout(0.5),
    tf.keras.layers.Dense(5, activation='softmax')  # 5 clases custom
])

# 3. Compilar
model.compile(
    optimizer=tf.keras.optimizers.Adam(learning_rate=0.0001),
    loss='categorical_crossentropy',
    metrics=['accuracy']
)

# 4. Data Augmentation
train_datagen = ImageDataGenerator(
    rescale=1./255,
    rotation_range=20,
    width_shift_range=0.2,
    height_shift_range=0.2,
    horizontal_flip=True,
    validation_split=0.2
)

train_generator = train_datagen.flow_from_directory(
    'data/train',
    target_size=(224, 224),
    batch_size=32,
    class_mode='categorical',
    subset='training'
)

val_generator = train_datagen.flow_from_directory(
    'data/train',
    target_size=(224, 224),
    batch_size=32,
    class_mode='categorical',
    subset='validation'
)

# 5. Entrenar
history = model.fit(
    train_generator,
    epochs=10,
    validation_data=val_generator
)

# 6. Predecir
import numpy as np
from tensorflow.keras.preprocessing import image

img_path = 'test_image.jpg'
img = image.load_img(img_path, target_size=(224, 224))
img_array = image.img_to_array(img)
img_array = np.expand_dims(img_array, axis=0) / 255.0

prediction = model.predict(img_array)
class_idx = np.argmax(prediction)
print(f"Clase predicha: {class_idx}, Confianza: {prediction[0][class_idx]:.2f}")
```

---

### **4. ROBOTICS**

**¿De qué trata?**
- IA aplicada a robots físicos
- Percepción, planificación, control

**Componentes:**
```
Sensores → Percepción → Planificación → Acción → Actuadores

Sensores:
- Cámaras (visión)
- LiDAR (distancia)
- IMU (orientación)
- Sensores táctiles

Actuadores:
- Motores
- Brazos robóticos
- Grippers (pinzas)
```

**Aplicaciones:**
```
- Manufactura (ensamblaje)
- Logística (Amazon warehouses)
- Cirugía asistida (Da Vinci)
- Exploración espacial (Mars rovers)
- Agricultura (cosecha automatizada)
```

---

### **5. EXPERT SYSTEMS (Sistemas Expertos)**

**¿De qué trata?**
- Sistemas basados en reglas (if-then)
- Imitan toma de decisiones de experto humano
- Lógica simbólica

**Componentes:**
```
1. Base de Conocimiento: Reglas (if-then)
2. Motor de Inferencia: Aplica reglas
3. Interfaz de Usuario: Preguntas/respuestas

Ejemplo: Diagnóstico médico
IF fiebre = alta AND tos = sí AND dificultad_respirar = sí
THEN posible_diagnostico = neumonía
RECOMENDACIÓN = consultar médico urgente
```

**Aplicaciones:**
```
- MYCIN (diagnóstico infecciones)
- DENDRAL (química)
- XCON (configuración de computadoras)
- Sistemas de crédito bancario
```

**Limitaciones:**
```
- Mantenimiento difícil (agregar reglas)
- No aprenden de datos
- Brittle (fallan en casos no previstos)
- Reemplazados mayormente por ML
```

---

**Habilitación:**
1. Aprender matemáticas: álgebra lineal, cálculo, estadística
2. Python + librerías (NumPy, Pandas, scikit-learn)
3. Cursos: Andrew Ng ML, Fast.ai
4. Practicar en Kaggle
5. Proyectos personales
6. Leer papers (arXiv.org)
7. Especializar en rama (NLP, CV, RL)

---

### Algoritmos Supervisados y no Supervisados, Indicadores de ML, Servicios Cognitivos

---

## **ALGORITMOS SUPERVISADOS**

### **1. REGRESIÓN LINEAL (Linear Regression)**

**¿De qué trata?**
- Predice valor continuo
- Relación lineal entre X e y
- Ecuación: y = mx + b (una variable) o y = w₁x₁ + w₂x₂ + ... + b

**Cuándo usar:**
```
- Relación lineal entre variables
- Predicción de valores continuos
- Variables numéricas

Ejemplos:
- Predecir precio casa según tamaño
- Ventas según gasto en publicidad
- Temperatura según hora del día
```

**Implementación:**

```python
from sklearn.linear_model import LinearRegression
from sklearn.model_selection import train_test_split
from sklearn.metrics import mean_squared_error, r2_score
import numpy as np

# Datos de ejemplo: Predecir precio casa (miles $) según tamaño (m²)
X = np.array([[50], [60], [70], [80], [90], [100], [110], [120]])  # Tamaño
y = np.array([150, 180, 200, 220, 250, 280, 300, 330])  # Precio

# Dividir datos
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)

# Entrenar modelo
model = LinearRegression()
model.fit(X_train, y_train)

# Predecir
y_pred = model.predict(X_test)

# Evaluar
mse = mean_squared_error(y_test, y_pred)
r2 = r2_score(y_test, y_pred)

print(f"Ecuación: y = {model.coef_[0]:.2f}x + {model.intercept_:.2f}")
print(f"MSE: {mse:.2f}")
print(f"R²: {r2:.2f}")

# Predecir nueva casa de 95 m²
nueva_casa = np.array([[95]])
precio_predicho = model.predict(nueva_casa)
print(f"Casa de 95m²: ${precio_predicho[0]:.2f}k")
```

**Ventajas:**
- Simple de entender e implementar
- Interpretable (coeficientes)
- Rápido de entrenar
- Funciona bien con relaciones lineales

**Desventajas:**
- Asume linealidad
- Sensible a outliers
- No captura relaciones complejas

---

### **2. REGRESIÓN LOGÍSTICA (Logistic Regression)**

**¿De qué trata?**
- Clasificación (no regresión, nombre confuso)
- Salida: probabilidad (0-1)
- Función sigmoide transforma salida lineal

**Ecuación:**
```
z = w₁x₁ + w₂x₂ + ... + b
P(y=1) = sigmoid(z) = 1 / (1 + e^(-z))

Si P > 0.5 → Clase 1
Si P ≤ 0.5 → Clase 0
```

**Implementación:**

```python
from sklearn.linear_model import LogisticRegression
from sklearn.metrics import accuracy_score, confusion_matrix, classification_report

# Datos: Predecir si email es spam (1) o no (0)
# Features: número de palabras_spam, num_enlaces, tiene_adjuntos
X = np.array([
    [5, 3, 1],   # Spam
    [1, 0, 0],   # No spam
    [10, 5, 1],  # Spam
    [2, 1, 0],   # No spam
    [8, 4, 1],   # Spam
    [0, 0, 0],   # No spam
])
y = np.array([1, 0, 1, 0, 1, 0])

X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.3, random_state=42)

model = LogisticRegression()
model.fit(X_train, y_train)

y_pred = model.predict(X_test)
y_proba = model.predict_proba(X_test)  # Probabilidades

print(f"Accuracy: {accuracy_score(y_test, y_pred):.2f}")
print(f"\nProbabilidades:\n{y_proba}")
print(f"\nConfusion Matrix:\n{confusion_matrix(y_test, y_pred)}")
```

**Ventajas:**
- Salida probabilística (interpretable)
- Funciona bien para clasificación binaria
- Regularización disponible (L1, L2)

**Desventajas:**
- Asume linealidad en logit
- No captura relaciones complejas

---

### **3. DECISION TREES (Árboles de Decisión)**

**¿De qué trata?**
- Estructura de árbol con reglas if-then
- Split datos basado en features
- Clasificación o regresión

**Estructura:**
```
                    [Outlook]
                   /    |    \
              Sunny   Overcast  Rain
              /          |         \
         [Humidity]      Play    [Wind]
          /      \                /    \
       High      Normal       Strong   Weak
        /          \            /        \
      Don't       Play      Don't       Play
```

**Implementación:**

```python
from sklearn.tree import DecisionTreeClassifier, plot_tree
import matplotlib.pyplot as plt

# Datos: Predecir si jugar tenis según clima
# Features: [Outlook (0=Sunny,1=Overcast,2=Rain), Temp (°C), Humidity (%), Wind (0=Weak,1=Strong)]
X = np.array([
    [0, 85, 85, 0],  # Sunny, calor, humedad alta, viento débil → No
    [0, 80, 90, 1],  # No
    [1, 83, 78, 0],  # Overcast → Sí
    [2, 70, 96, 0],  # Rain, viento débil → Sí
    [2, 68, 80, 0],  # Sí
    [2, 65, 70, 1],  # Rain, viento fuerte → No
    [1, 64, 65, 1],  # Overcast → Sí
    [0, 72, 95, 0],  # Sunny → No
    [0, 69, 70, 0],  # Sunny → Sí
    [2, 75, 80, 0],  # Rain → Sí
])
y = np.array([0, 0, 1, 1, 1, 0, 1, 0, 1, 1])  # 0=No jugar, 1=Jugar

model = DecisionTreeClassifier(max_depth=3, random_state=42)
model.fit(X, y)

# Visualizar árbol
plt.figure(figsize=(20,10))
plot_tree(model, feature_names=['Outlook', 'Temp', 'Humidity', 'Wind'], 
          class_names=['No', 'Yes'], filled=True)
plt.show()

# Predecir
nuevo_dia = np.array([[1, 75, 80, 0]])  # Overcast, 75°, 80% humidity, viento débil
prediccion = model.predict(nuevo_dia)
print(f"Jugar tenis: {'Sí' if prediccion[0] == 1 else 'No'}")

# Feature importance
importances = model.feature_importances_
print("\nImportancia de features:")
for i, imp in enumerate(importances):
    print(f"  {['Outlook', 'Temp', 'Humidity', 'Wind'][i]}: {imp:.3f}")
```

**Ventajas:**
- Fácil de entender y visualizar
- No requiere normalización de datos
- Maneja features numéricos y categóricos
- Feature importance automática

**Desventajas:**
- Overfitting fácilmente (sin poda)
- Inestable (pequeños cambios → árbol diferente)
- Sesgo hacia features con más valores

---

### **4. RANDOM FOREST**

**¿De qué trata?**
- Ensemble de múltiples Decision Trees
- Cada árbol entrenado con subset aleatorio de datos
- Votación para clasificación, promedio para regresión

**Concepto:**
```
        [Random Forest]
             |
    ┌────────┼────────┐
    │        │        │
  Tree 1  Tree 2  Tree 3  ... Tree N
    ↓        ↓        ↓
  Vote     Vote     Vote
    └────────┼────────┘
          Majority
          Vote → Predicción
```

**Implementación:**

```python
from sklearn.ensemble import RandomForestClassifier
from sklearn.datasets import load_iris

# Cargar dataset Iris
iris = load_iris()
X, y = iris.data, iris.target

X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.3, random_state=42)

# Random Forest con 100 árboles
model = RandomForestClassifier(n_estimators=100, max_depth=5, random_state=42)
model.fit(X_train, y_train)

y_pred = model.predict(X_test)
accuracy = accuracy_score(y_test, y_pred)

print(f"Accuracy: {accuracy:.2f}")
print(f"\nFeature Importances:")
for name, imp in zip(iris.feature_names, model.feature_importances_):
    print(f"  {name}: {imp:.3f}")
```

**Ventajas:**
- Reduce overfitting vs árbol individual
- Robusto, alta precisión
- Maneja features categóricos y numéricos
- Feature importance

**Desventajas:**
- Menos interpretable que árbol individual
- Más lento que árbol único
- Requiere más memoria

---

### **5. SUPPORT VECTOR MACHINE (SVM)**

**¿De qué trata?**
- Encuentra hiperplano óptimo que separa clases
- Maximiza margen entre clases
- Kernel trick para datos no lineales

**Concepto:**
```
        Clase A          |          Clase B
          ●              |              ○
          ●              |              ○
          ●        Margen |  Margen     ○
    ─────●──────────────────────────○─────
          ●              |              ○
          ●       Hiperplano            ○
                         |
    Support Vectors: Puntos más cercanos al hiperplano
```

**Implementación:**

```python
from sklearn.svm import SVC
from sklearn.preprocessing import StandardScaler

# Datos linealmente separables
X = np.array([[1, 2], [2, 3], [3, 3], [6, 5], [7, 7], [8, 6]])
y = np.array([0, 0, 0, 1, 1, 1])

# Escalar (SVM sensible a escala)
scaler = StandardScaler()
X_scaled = scaler.fit_transform(X)

# SVM lineal
model = SVC(kernel='linear', C=1.0)
model.fit(X_scaled, y)

# Predecir
nuevo_punto = scaler.transform([[5, 4]])
prediccion = model.predict(nuevo_punto)
print(f"Clase: {prediccion[0]}")

# SVM con kernel RBF (para datos no lineales)
model_rbf = SVC(kernel='rbf', gamma='auto')
model_rbf.fit(X_scaled, y)
```

**Kernels:**
```
- Linear: Datos linealmente separables
- RBF (Radial Basis Function): Datos no lineales (default)
- Polynomial: Relaciones polinómicas
- Sigmoid: Similar a red neuronal
```

**Ventajas:**
- Efectivo en alta dimensionalidad
- Memoria eficiente (solo usa support vectors)
- Kernel trick para no linealidad

**Desventajas:**
- Lento con datasets grandes (>10k muestras)
- Sensible a escala de features
- Difícil de interpretar

---

### **6. K-NEAREST NEIGHBORS (KNN)**

**¿De qué trata?**
- Clasificación basada en vecinos más cercanos
- No entrenamiento real (lazy learning)
- Vota mayoría de K vecinos

**Concepto:**
```
        ?  ← Punto a clasificar
        |
    ┌───┼───┐
    │   │   │
    ●   ○   ●   K=3
    
Distancia a 3 vecinos más cercanos:
● (Clase A): 2 vecinos
○ (Clase B): 1 vecino

Predicción: Clase A (mayoría)
```

**Implementación:**

```python
from sklearn.neighbors import KNeighborsClassifier

X = np.array([[1,1], [2,2], [3,3], [6,6], [7,7], [8,8]])
y = np.array([0, 0, 0, 1, 1, 1])

# K=3 vecinos
model = KNeighborsClassifier(n_neighbors=3)
model.fit(X, y)

# Predecir
nuevo_punto = np.array([[4, 4]])
prediccion = model.predict(nuevo_punto)
distancias, indices = model.kneighbors(nuevo_punto)

print(f"Clase: {prediccion[0]}")
print(f"Vecinos más cercanos: {indices}")
print(f"Distancias: {distancias}")
```

**Elegir K:**
```
K pequeño (1-3):
  + Captura detalles finos
  - Sensible a ruido (overfitting)

K grande (>10):
  + Más robusto, suaviza decisión
  - Puede perder detalles (underfitting)

Regla: K = √n (n = número de muestras)
Usar cross-validation para optimizar K
```

**Ventajas:**
- Simple de entender
- No requiere entrenamiento
- Funciona bien con pocos datos

**Desventajas:**
- Lento en predicción (calcula distancias a todos)
- Sensible a escala de features
- Curse of dimensionality (alta dimensión)

---

### **7. GRADIENT BOOSTING (XGBoost, LightGBM, CatBoost)**

**¿De qué trata?**
- Ensemble de árboles secuenciales
- Cada árbol corrige errores del anterior
- Suma ponderada de predicciones

**Concepto:**
```
Iteración 1: Árbol simple → Error residual
Iteración 2: Árbol entrena en residuales → Mejora
Iteración 3: Árbol corrige nuevos residuales → Mejora
...
Iteración N: Combinación de todos los árboles

Predicción Final = Σ (learning_rate × árbol_i)
```

**Implementación:**

```python
import xgboost as xgb
from sklearn.datasets import load_breast_cancer

# Cargar datos (clasificación cáncer)
data = load_breast_cancer()
X, y = data.data, data.target

X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)

# XGBoost
model = xgb.XGBClassifier(
    n_estimators=100,      # Número de árboles
    learning_rate=0.1,     # Tasa de aprendizaje
    max_depth=5,           # Profundidad de árboles
    random_state=42
)

model.fit(X_train, y_train)

y_pred = model.predict(X_test)
y_proba = model.predict_proba(X_test)

accuracy = accuracy_score(y_test, y_pred)
print(f"Accuracy: {accuracy:.3f}")

# Feature importance
import matplotlib.pyplot as plt
xgb.plot_importance(model, max_num_features=10)
plt.show()
```

**Comparación de Librerías:**

| Librería    | Velocidad | Memoria | Categóricas | Uso Principal              |
|-------------|-----------|---------|-------------|----------------------------|
| **XGBoost** | Rápido    | Media   | Manual      | Kaggle, competencias       |
| **LightGBM**| Muy rápido| Baja    | Automático  | Datasets grandes           |
| **CatBoost**| Media     | Media   | Nativo      | Features categóricos       |

**Ventajas:**
- Alta precisión (gana Kaggle competitions)
- Maneja features categóricos y numéricos
- Regularización incorporada
- Feature importance

**Desventajas:**
- Propenso a overfitting (requiere tuning)
- Más lento que Random Forest
- Menos interpretable

---

### **8. NEURAL NETWORKS (Redes Neuronales)**

**¿De qué trata?**
- Capas de neuronas interconectadas
- Aprende representaciones complejas
- Backpropagation para ajustar pesos

(Ya cubierto en sección Deep Learning)

---

## **ALGORITMOS NO SUPERVISADOS**

### **1. K-MEANS CLUSTERING**

**¿De qué trata?**
- Agrupa datos en K clusters
- Minimiza distancia intra-cluster
- Asigna cada punto al centroide más cercano

**Algoritmo:**
```
1. Inicializar K centroides aleatoriamente
2. Asignar cada punto al centroide más cercano
3. Recalcular centroides (media de puntos asignados)
4. Repetir 2-3 hasta convergencia
```

**Implementación:**

```python
from sklearn.cluster import KMeans
import matplotlib.pyplot as plt

# Datos: Clientes (gasto anual, frecuencia compras)
X = np.array([
    [20, 5], [21, 6], [22, 5],    # Cluster 1: Bajo gasto
    [80, 18], [82, 19], [85, 20], # Cluster 2: Alto gasto
    [50, 12], [52, 11], [48, 13]  # Cluster 3: Medio gasto
])

# K-Means con 3 clusters
kmeans = KMeans(n_clusters=3, random_state=42)
kmeans.fit(X)

# Predicciones
labels = kmeans.labels_
centroids = kmeans.cluster_centers_

print(f"Labels: {labels}")
print(f"Centroides:\n{centroids}")

# Visualizar
plt.scatter(X[:, 0], X[:, 1], c=labels, cmap='viridis')
plt.scatter(centroids[:, 0], centroids[:, 1], marker='X', s=200, c='red')
plt.xlabel('Gasto Anual ($k)')
plt.ylabel('Frecuencia Compras')
plt.title('Segmentación de Clientes')
plt.show()

# Predecir nuevo cliente
nuevo_cliente = np.array([[60, 15]])
cluster = kmeans.predict(nuevo_cliente)
print(f"Nuevo cliente pertenece a cluster: {cluster[0]}")
```

**Elegir K (Método del Codo):**

```python
# Probar diferentes valores de K
inertias = []
K_range = range(1, 10)

for k in K_range:
    kmeans = KMeans(n_clusters=k, random_state=42)
    kmeans.fit(X)
    inertias.append(kmeans.inertia_)  # Suma de distancias al cuadrado

# Graficar
plt.plot(K_range, inertias, marker='o')
plt.xlabel('Número de Clusters (K)')
plt.ylabel('Inertia')
plt.title('Método del Codo')
plt.show()

# Buscar "codo" donde inertia deja de decrecer significativamente
```

**Ventajas:**
- Simple y rápido
- Escalable a grandes datasets
- Funciona bien con clusters esféricos

**Desventajas:**
- Requiere especificar K
- Sensible a inicialización (usar k-means++)
- Asume clusters esféricos y tamaño similar
- Sensible a outliers

---

### **2. HIERARCHICAL CLUSTERING**

**¿De qué trata?**
- Crea jerarquía de clusters (dendrograma)
- No requiere especificar K
- Aglomerativo (bottom-up) o Divisivo (top-down)

**Algoritmo Aglomerativo:**
```
1. Cada punto es un cluster
2. Combinar 2 clusters más cercanos
3. Repetir hasta 1 cluster (o K deseado)
```

**Implementación:**

```python
from sklearn.cluster import AgglomerativeClustering
from scipy.cluster.hierarchy import dendrogram, linkage

X = np.array([[1,2], [2,3], [3,3], [8,7], [9,8], [10,8]])

# Hierarchical Clustering
clustering = AgglomerativeClustering(n_clusters=2, linkage='ward')
labels = clustering.fit_predict(X)

print(f"Labels: {labels}")

# Dendrograma
plt.figure(figsize=(10, 5))
linked = linkage(X, method='ward')
dendrogram(linked)
plt.title('Dendrograma')
plt.xlabel('Índice de Muestra')
plt.ylabel('Distancia')
plt.show()
```

**Linkage Methods:**
```
- Ward: Minimiza varianza intra-cluster (común)
- Complete: Distancia máxima entre clusters
- Average: Distancia promedio
- Single: Distancia mínima
```

**Ventajas:**
- No requiere K predefinido
- Dendrograma visualiza jerarquía
- Flexibilidad en linkage

**Desventajas:**
- Lento O(n³) (no escalable)
- Decisiones no reversibles
- Sensible a ruido y outliers

---

### **3. DBSCAN (Density-Based Spatial Clustering)**

**¿De qué trata?**
- Clustering basado en densidad
- Detecta clusters de forma arbitraria
- Identifica outliers automáticamente

**Parámetros:**
```
- eps: Radio de vecindad
- min_samples: Mínimo de puntos para formar cluster

Tipos de puntos:
- Core: ≥ min_samples en eps
- Border: < min_samples pero en vecindad de core
- Noise: No core ni border (outlier)
```

**Implementación:**

```python
from sklearn.cluster import DBSCAN

# Datos con forma no esférica y outliers
X = np.array([
    [1,2], [2,2], [2,3], [8,7], [8,8], [25,25],  # Outlier
    [1,3], [3,2], [9,8], [8,9]
])

# DBSCAN
dbscan = DBSCAN(eps=2, min_samples=2)
labels = dbscan.fit_predict(X)

print(f"Labels: {labels}")  # -1 indica outlier

# Visualizar
plt.scatter(X[:, 0], X[:, 1], c=labels, cmap='viridis')
plt.title('DBSCAN Clustering')
plt.show()

# Contar clusters (excluyendo -1)
n_clusters = len(set(labels)) - (1 if -1 in labels else 0)
n_noise = list(labels).count(-1)
print(f"Clusters: {n_clusters}, Outliers: {n_noise}")
```

**Ventajas:**
- No requiere K
- Detecta clusters de forma arbitraria
- Identifica outliers
- Robusto a ruido

**Desventajas:**
- Sensible a eps y min_samples
- No funciona bien con densidades variables
- Difícil con alta dimensionalidad

---

### **4. PCA (Principal Component Analysis)**

**¿De qué trata?**
- Reducción de dimensionalidad
- Encuentra componentes principales (máxima varianza)
- Proyecta datos a menor dimensión

**Uso:**
```
- Visualización (3D → 2D)
- Reducir features (100 → 10)
- Acelerar entrenamiento
- Eliminar ruido
```

**Implementación:**

```python
from sklearn.decomposition import PCA
from sklearn.datasets import load_digits

# Cargar dataset de dígitos (64 features)
digits = load_digits()
X, y = digits.data, digits.target

print(f"Shape original: {X.shape}")  # (1797, 64)

# PCA: Reducir a 2 componentes para visualización
pca = PCA(n_components=2)
X_pca = pca.fit_transform(X)

print(f"Shape reducida: {X_pca.shape}")  # (1797, 2)
print(f"Varianza explicada: {pca.explained_variance_ratio_}")
print(f"Varianza total: {sum(pca.explained_variance_ratio_):.2%}")

# Visualizar
plt.scatter(X_pca[:, 0], X_pca[:, 1], c=y, cmap='tab10', alpha=0.5)
plt.xlabel('PC1')
plt.ylabel('PC2')
plt.title('PCA: 64D → 2D')
plt.colorbar()
plt.show()

# Elegir número de componentes (95% varianza)
pca_full = PCA(n_components=0.95)  # 95% varianza
X_reduced = pca_full.fit_transform(X)
print(f"Componentes para 95% varianza: {pca_full.n_components_}")
```

**Ventajas:**
- Reduce dimensionalidad conservando información
- Elimina correlación entre features
- Acelera modelos
- Visualización

**Desventajas:**
- Pérdida de información
- Componentes difíciles de interpretar
- Sensible a escala (requiere normalización)
- Asume linealidad

---

### **5. t-SNE (t-Distributed Stochastic Neighbor Embedding)**

**¿De qué trata?**
- Reducción de dimensionalidad no lineal
- Visualización (principalmente 2D/3D)
- Preserva vecindad local

**Diferencia con PCA:**
```
PCA:
- Lineal
- Preserva varianza global
- Rápido

t-SNE:
- No lineal
- Preserva estructura local (vecinos)
- Lento
- Solo visualización (no usar para ML posterior)
```

**Implementación:**

```python
from sklearn.manifold import TSNE

# Cargar MNIST
from sklearn.datasets import fetch_openml
mnist = fetch_openml('mnist_784', version=1, parser='auto')
X, y = mnist.data[:5000], mnist.target[:5000]  # Solo 5k por velocidad

# t-SNE
tsne = TSNE(n_components=2, random_state=42, perplexity=30)
X_tsne = tsne.fit_transform(X)

# Visualizar
plt.figure(figsize=(12, 8))
scatter = plt.scatter(X_tsne[:, 0], X_tsne[:, 1], c=y.astype(int), cmap='tab10', alpha=0.6)
plt.colorbar(scatter)
plt.title('t-SNE de MNIST')
plt.show()
```

**Ventajas:**
- Excelente visualización de datos complejos
- Preserva estructura local
- Detecta clusters

**Desventajas:**
- Muy lento (O(n²))
- No determinista (diferentes resultados)
- Parámetro perplexity crítico
- Solo para visualización

---

## **INDICADORES DE ML (MÉTRICAS)**

### **Clasificación:**

**1. Confusion Matrix**

```
                 Predicted
                 Pos    Neg
Actual  Pos      TP     FN
        Neg      FP     TN

TP (True Positive): Predijo Pos, es Pos ✓
TN (True Negative): Predijo Neg, es Neg ✓
FP (False Positive): Predijo Pos, es Neg ✗ (Error Tipo I)
FN (False Negative): Predijo Neg, es Pos ✗ (Error Tipo II)
```

**2. Accuracy (Exactitud)**

```
Accuracy = (TP + TN) / (TP + TN + FP + FN)

Cuándo usar:
✓ Clases balanceadas (50% Pos, 50% Neg)

Cuándo NO usar:
✗ Clases desbalanceadas (ej: 95% Neg, 5% Pos)
  Predecir todo Neg → 95% accuracy (engañoso!)
```

**3. Precision (Precisión)**

```
Precision = TP / (TP + FP)

Pregunta: De los que predije Positivos, ¿cuántos son realmente Positivos?

Cuándo usar:
- FP costosos
- Spam detection (no quiero emails legítimos en spam)
- Diagnóstico médico (no alarmar pacientes sanos)
```

**4. Recall (Sensibilidad, True Positive Rate)**

```
Recall = TP / (TP + FN)

Pregunta: De los realmente Positivos, ¿cuántos detecté?

Cuándo usar:
- FN costosos
- Detección de fraude (no perder fraude real)
- Diagnóstico cáncer (no perder paciente enfermo)
```

**5. F1-Score**

```
F1 = 2 × (Precision × Recall) / (Precision + Recall)

Media armónica de Precision y Recall

Cuándo usar:
- Balance entre Precision y Recall
- Clases desbalanceadas
```

**Ejemplo:**

```python
from sklearn.metrics import confusion_matrix, accuracy_score, precision_score, recall_score, f1_score, classification_report

y_true = np.array([1, 1, 0, 1, 0, 1, 0, 0, 1, 0])
y_pred = np.array([1, 0, 0, 1, 0, 1, 1, 0, 1, 0])

# Confusion Matrix
cm = confusion_matrix(y_true, y_pred)
print("Confusion Matrix:")
print(cm)
#      Predicted
#       0   1
# Actual
# 0    [4   1]  → TN=4, FP=1
# 1    [1   4]  → FN=1, TP=4

# Métricas
accuracy = accuracy_score(y_true, y_pred)
precision = precision_score(y_true, y_pred)
recall = recall_score(y_true, y_pred)
f1 = f1_score(y_true, y_pred)

print(f"\nAccuracy:  {accuracy:.2f}")   # 0.80
print(f"Precision: {precision:.2f}")  # 0.80 (4/(4+1))
print(f"Recall:    {recall:.2f}")     # 0.80 (4/(4+1))
print(f"F1-Score:  {f1:.2f}")         # 0.80

# Reporte completo
print("\nClassification Report:")
print(classification_report(y_true, y_pred, target_names=['Clase 0', 'Clase 1']))
```

**6. ROC-AUC (Receiver Operating Characteristic - Area Under Curve)**

```
ROC Curve:
- Eje X: False Positive Rate (FPR) = FP/(FP+TN)
- Eje Y: True Positive Rate (TPR) = Recall

AUC:
- 1.0: Clasificador perfecto
- 0.5: Aleatorio
- <0.5: Peor que aleatorio

Cuándo usar:
- Evaluar modelos con probabilidades
- Comparar múltiples modelos
- Clases desbalanceadas
```

```python
from sklearn.metrics import roc_curve, roc_auc_score

# y_proba: probabilidades del modelo
y_proba = model.predict_proba(X_test)[:, 1]  # Prob de clase positiva

# Calcular AUC
auc = roc_auc_score(y_test, y_proba)
print(f"AUC: {auc:.3f}")

# ROC Curve
fpr, tpr, thresholds = roc_curve(y_test, y_proba)

plt.plot(fpr, tpr, label=f'AUC = {auc:.3f}')
plt.plot([0, 1], [0, 1], 'k--', label='Random')
plt.xlabel('False Positive Rate')
plt.ylabel('True Positive Rate')
plt.title('ROC Curve')
plt.legend()
plt.show()
```

---

### **Regresión:**

**1. Mean Absolute Error (MAE)**

```
MAE = (1/n) Σ |y_true - y_pred|

Promedio de errores absolutos
Unidades: mismas que y
Interpretable
```

**2. Mean Squared Error (MSE)**

```
MSE = (1/n) Σ (y_true - y_pred)²

Penaliza errores grandes más fuertemente
Sensible a outliers
```

**3. Root Mean Squared Error (RMSE)**

```
RMSE = √MSE

Mismas unidades que y
Más interpretable que MSE
```

**4. R² (Coefficient of Determination)**

```
R² = 1 - (SS_res / SS_tot)

SS_res = Σ(y_true - y_pred)²  (varianza residual)
SS_tot = Σ(y_true - y_mean)²  (varianza total)

Rango: -∞ a 1
- 1.0: Predicción perfecta
- 0.0: Igual que predecir media
- <0.0: Peor que media

Cuándo usar:
- Comparar modelos
- Evaluar bondad de ajuste
```

```python
from sklearn.metrics import mean_absolute_error, mean_squared_error, r2_score

y_true = np.array([100, 150, 200, 250, 300])
y_pred = np.array([110, 140, 210, 240, 290])

mae = mean_absolute_error(y_true, y_pred)
mse = mean_squared_error(y_true, y_pred)
rmse = np.sqrt(mse)
r2 = r2_score(y_true, y_pred)

print(f"MAE:  ${mae:.2f}")
print(f"MSE:  {mse:.2f}")
print(f"RMSE: ${rmse:.2f}")
print(f"R²:   {r2:.3f}")
```

---

## **SERVICIOS COGNITIVOS (COGNITIVE SERVICES)**

**¿De qué trata?**
- APIs de IA pre-entrenadas
- Integración sencilla sin ML expertise
- Servicios cloud (Azure, AWS, Google)

---

### **1. AZURE COGNITIVE SERVICES**

**Categorías:**

**a) Vision**

```
Computer Vision API:
- Análisis de imágenes (objetos, caras, texto OCR)
- Descripción automática de imágenes
- Detección de contenido adulto
- Reconocimiento de celebridades

Endpoint: https://<region>.api.cognitive.microsoft.com/vision/v3.2/
```

```python
import requests

subscription_key = "YOUR_KEY"
endpoint = "https://westus.api.cognitive.microsoft.com/vision/v3.2/analyze"

image_url = "https://example.com/image.jpg"

headers = {
    'Ocp-Apim-Subscription-Key': subscription_key,
    'Content-Type': 'application/json'
}

params = {
    'visualFeatures': 'Categories,Description,Color,Tags,Objects,Faces'
}

data = {'url': image_url}

response = requests.post(endpoint, headers=headers, params=params, json=data)
result = response.json()

print("Descripción:", result['description']['captions'][0]['text'])
print("Tags:", [tag['name'] for tag in result['tags']])
print("Objetos:", [obj['object'] for obj in result['objects']])
```

**Face API:**
```
- Detección de caras
- Reconocimiento facial (verificación, identificación)
- Análisis de emociones
- Estimación de edad/género

Endpoint: https://<region>.api.cognitive.microsoft.com/face/v1.0/
```

```python
# Detectar caras y emociones
face_api_url = "https://westus.api.cognitive.microsoft.com/face/v1.0/detect"

params = {
    'returnFaceId': 'true',
    'returnFaceAttributes': 'age,gender,emotion,smile'
}

response = requests.post(face_api_url, headers=headers, params=params, json=data)
faces = response.json()

for face in faces:
    print(f"Edad: {face['faceAttributes']['age']}")
    print(f"Género: {face['faceAttributes']['gender']}")
    print(f"Emociones: {face['faceAttributes']['emotion']}")
```

---

**b) Language**

**Text Analytics API:**
```
- Análisis de sentimientos
- Extracción de entidades (NER)
- Detección de idioma
- Key phrase extraction

Endpoint: https://<region>.api.cognitive.microsoft.com/text/analytics/v3.1/
```

```python
text_analytics_url = "https://westus.api.cognitive.microsoft.com/text/analytics/v3.1/sentiment"

documents = {
    "documents": [
        {"id": "1", "language": "es", "text": "Me encanta este producto, es increíble!"},
        {"id": "2", "language": "es", "text": "Servicio pésimo, nunca vuelvo."},
    ]
}

response = requests.post(text_analytics_url, headers=headers, json=documents)
sentiments = response.json()

for doc in sentiments['documents']:
    print(f"Texto {doc['id']}: {doc['sentiment']} (score: {doc['confidenceScores']})")
```

**Translator API:**
```
- Traducción 100+ idiomas
- Detección automática de idioma
- Transliteración

Endpoint: https://api.cognitive.microsofttranslator.com/translate
```

```python
translator_url = "https://api.cognitive.microsofttranslator.com/translate"

params = {
    'api-version': '3.0',
    'from': 'en',
    'to': ['es', 'fr', 'de']
}

body = [{'text': 'Hello, how are you?'}]

response = requests.post(translator_url, headers=headers, params=params, json=body)
translations = response.json()

for translation in translations[0]['translations']:
    print(f"{translation['to']}: {translation['text']}")
```

---

**c) Speech**

**Speech-to-Text:**
```
- Transcripción de audio
- Tiempo real o batch
- 100+ idiomas

Endpoint: https://<region>.stt.speech.microsoft.com/speech/recognition/
```

```python
import azure.cognitiveservices.speech as speechsdk

speech_key = "YOUR_KEY"
service_region = "westus"

speech_config = speechsdk.SpeechConfig(subscription=speech_key, region=service_region)
speech_config.speech_recognition_language = "es-ES"

# Desde micrófono
audio_config = speechsdk.audio.AudioConfig(use_default_microphone=True)
speech_recognizer = speechsdk.SpeechRecognizer(speech_config=speech_config, audio_config=audio_config)

print("Habla algo...")
result = speech_recognizer.recognize_once()

if result.reason == speechsdk.ResultReason.RecognizedSpeech:
    print(f"Reconocido: {result.text}")
elif result.reason == speechsdk.ResultReason.NoMatch:
    print("No se reconoció voz")
```

**Text-to-Speech:**
```
- Síntesis de voz
- Voces neuronales (realistas)
- Control de tono, velocidad

Endpoint: https://<region>.tts.speech.microsoft.com/
```

```python
speech_config = speechsdk.SpeechConfig(subscription=speech_key, region=service_region)
speech_config.speech_synthesis_voice_name = "es-ES-ElviraNeural"

audio_config = speechsdk.audio.AudioOutputConfig(use_default_speaker=True)
speech_synthesizer = speechsdk.SpeechSynthesizer(speech_config=speech_config, audio_config=audio_config)

text = "Hola, soy una voz generada por inteligencia artificial."
result = speech_synthesizer.speak_text_async(text).get()

if result.reason == speechsdk.ResultReason.SynthesizingAudioCompleted:
    print("Audio generado exitosamente")
```

---

**d) Decision**

**Anomaly Detector:**
```
- Detecta anomalías en series temporales
- Batch o streaming

Endpoint: https://<region>.api.cognitive.microsoft.com/anomalydetector/v1.0/
```

**Content Moderator:**
```
- Moderación de texto (profanidad, PII)
- Moderación de imágenes (adulto, violencia)
- Moderación de videos

Endpoint: https://<region>.api.cognitive.microsoft.com/contentmoderator/
```

---

### **2. AWS AI SERVICES**

**Amazon Rekognition (Vision):**
```
- Detección de objetos y caras
- Reconocimiento de celebridades
- Detección de texto (OCR)
- Moderación de contenido
- Face comparison
```

```python
import boto3

rekognition = boto3.client('rekognition', region_name='us-east-1')

# Detectar etiquetas en imagen
with open('image.jpg', 'rb') as image_file:
    response = rekognition.detect_labels(
        Image={'Bytes': image_file.read()},
        MaxLabels=10,
        MinConfidence=75
    )

for label in response['Labels']:
    print(f"{label['Name']}: {label['Confidence']:.2f}%")
```

**Amazon Comprehend (NLP):**
```
- Análisis de sentimientos
- Extracción de entidades
- Detección de idioma
- Key phrases
- Topic modeling
```

```python
comprehend = boto3.client('comprehend', region_name='us-east-1')

text = "Amazon Web Services es una plataforma de computación en la nube."

# Detectar idioma
lang_response = comprehend.detect_dominant_language(Text=text)
print(f"Idioma: {lang_response['Languages'][0]['LanguageCode']}")

# Análisis de sentimientos
sentiment_response = comprehend.detect_sentiment(Text=text, LanguageCode='es')
print(f"Sentimiento: {sentiment_response['Sentiment']}")

# Entidades
entities_response = comprehend.detect_entities(Text=text, LanguageCode='es')
for entity in entities_response['Entities']:
    print(f"{entity['Type']}: {entity['Text']}")
```

**Amazon Polly (Text-to-Speech):**
```
- Síntesis de voz
- Voces neuronales
- SSML support
```

**Amazon Transcribe (Speech-to-Text):**
```
- Transcripción de audio
- Tiempo real o batch
- Identificación de hablantes
```

---

### **3. GOOGLE CLOUD AI**

**Cloud Vision API:**
```
- Detección de etiquetas
- OCR
- Detección de caras y landmarks
- Detección de logos
- Safe Search (contenido explícito)
```

```python
from google.cloud import vision

client = vision.ImageAnnotatorClient()

# Cargar imagen
with open('image.jpg', 'rb') as image_file:
    content = image_file.read()

image = vision.Image(content=content)

# Detección de etiquetas
response = client.label_detection(image=image)
labels = response.label_annotations

print("Labels:")
for label in labels:
    print(f"- {label.description} ({label.score:.2f})")

# OCR
response = client.text_detection(image=image)
texts = response.text_annotations

print(f"\nTexto detectado:\n{texts[0].description}")
```

**Cloud Natural Language API:**
```
- Análisis de sentimientos
- Análisis de entidades
- Análisis sintáctico
- Clasificación de contenido
```

```python
from google.cloud import language_v1

client = language_v1.LanguageServiceClient()

text = "Google Cloud Platform ofrece servicios de inteligencia artificial avanzados."
document = language_v1.Document(content=text, type_=language_v1.Document.Type.PLAIN_TEXT)

# Análisis de sentimientos
sentiment = client.analyze_sentiment(request={'document': document}).document_sentiment
print(f"Sentimiento: score={sentiment.score}, magnitude={sentiment.magnitude}")

# Entidades
entities = client.analyze_entities(request={'document': document}).entities
for entity in entities:
    print(f"- {entity.name} ({language_v1.Entity.Type(entity.type_).name})")
```

**Cloud Speech-to-Text:**
```
- Transcripción de audio
- 120+ idiomas
- Streaming recognition
- Punctuation automática
```

**Dialogflow (Chatbots):**
```
- Construcción de chatbots conversacionales
- Procesamiento de lenguaje natural
- Integración con múltiples plataformas
- Multi-idioma
```

---

### **4. OPENAI API (GPT, DALL-E)**

**ChatGPT API:**
```python
import openai

openai.api_key = "YOUR_API_KEY"

response = openai.ChatCompletion.create(
    model="gpt-4",
    messages=[
        {"role": "system", "content": "Eres un asistente experto en IA."},
        {"role": "user", "content": "Explica qué es machine learning en 2 párrafos."}
    ],
    temperature=0.7,
    max_tokens=200
)

print(response.choices[0].message.content)
```

**DALL-E (Generación de Imágenes):**
```python
response = openai.Image.create(
    prompt="Un gato astronauta flotando en el espacio, estilo digital art",
    n=1,
    size="1024x1024"
)

image_url = response['data'][0]['url']
print(f"Imagen generada: {image_url}")
```

**Embeddings (para Búsqueda Semántica):**
```python
response = openai.Embedding.create(
    model="text-embedding-ada-002",
    input="Machine learning es una rama de la IA"
)

embedding = response['data'][0]['embedding']  # Vector de 1536 dimensiones
# Usar para búsqueda semántica, clustering, etc.
```

---

**Comparación de Servicios:**

| Proveedor | Visión          | NLP             | Voz (STT/TTS) | Precio Base        |
|-----------|-----------------|-----------------|---------------|--------------------|
| **Azure** | Computer Vision | Text Analytics  | Speech        | $1-2 por 1k trans. |
| **AWS**   | Rekognition     | Comprehend      | Transcribe    | $1-5 por 1k trans. |
| **Google**| Cloud Vision    | Natural Language| Speech-to-Text| $1.50 por 1k trans.|
| **OpenAI**| DALL-E          | GPT-4           | Whisper       | $0.002-0.12 por 1k tokens |

---

**Habilitación:**
1. Crear cuenta en plataforma (Azure, AWS, GCP)
2. Obtener API keys
3. Instalar SDK: `pip install azure-cognitiveservices-vision-computervision` (o boto3, google-cloud-vision)
4. Revisar documentación y ejemplos
5. Empezar con tier gratuito
6. Integrar en aplicación (REST API o SDK)

**Casos de Uso Empresariales:**
- **E-commerce:** Búsqueda de productos por imagen
- **Atención al cliente:** Chatbots inteligentes
- **Seguridad:** Reconocimiento facial para acceso
- **Salud:** Análisis de imágenes médicas
- **Marketing:** Análisis de sentimientos en redes sociales
- **Manufactura:** Detección de defectos con Computer Vision
- **Legal:** Extracción de entidades de contratos (NER)