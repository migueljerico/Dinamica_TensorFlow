# 🧠 Dinámica TensorFlow

[![Python](https://img.shields.io/badge/Python-3.12-blue?style=for-the-badge&logo=python)](https://www.python.org/)
[![TensorFlow](https://img.shields.io/badge/TensorFlow-2.21-FF6F00?style=for-the-badge&logo=tensorflow)](https://www.tensorflow.org/)
[![Estado](https://img.shields.io/badge/Estado-En%20desarrollo-yellow?style=for-the-badge)](https://github.com/migueljerico/Dinamica_TensorFlow)
[![Licencia](https://img.shields.io/badge/Licencia-MIT-green?style=for-the-badge)](https://opensource.org/licenses/MIT)

*Exploración de TensorFlow y la crítica gestión de compatibilidad de entornos Python para ML con aceleración GPU.*


## 📋 Descripción
Este repositorio documenta una práctica centrada en la librería TensorFlow, abordando su importancia en el campo de la Inteligencia Artificial y el Aprendizaje Automático. El objetivo principal de la práctica fue investigar y comprender TensorFlow, pero un punto crítico y central de este documento es la **preparación y gestión del entorno Python**, crucial para el correcto funcionamiento de TensorFlow, especialmente cuando se busca aprovechar la aceleración por GPU mediante tecnologías como CUDA de NVIDIA.

El proyecto detalla el proceso y las razones técnicas detrás de la necesidad de realizar un _downgrade_ en la versión de Python para asegurar la compatibilidad con TensorFlow y su ecosistema de aceleración por hardware. Sirve como una guía y referencia para desarrolladores y estudiantes que se enfrentan a desafíos de compatibilidad de versiones al configurar entornos de desarrollo para Machine Learning.

## ✨ Funcionalidades
| Funcionalidad / Aspecto Cubierto | Descripción |
| :------------------------------- | :------------------------------------------------------------------------------------------------------------------------------------------------ |
| **Documentación de Incompatibilidad** | Explica detalladamente las razones técnicas detrás de la incompatibilidad de Python 3.14 con TensorFlow 2.21 y CUDA. |
| **Guía de _Downgrade_ de Python** | Proporciona los pasos y comandos para instalar una versión compatible de Python (3.12) en sistemas Windows. |
| **Descripción de TensorFlow** | Introduce TensorFlow como una plataforma de ML y sus capacidades. |
| **Contexto de Aceleración GPU** | Detalla la interacción necesaria entre TensorFlow, CUDA Toolkit y cuDNN para el uso eficiente de GPUs. |
| **Identificación de Tecnologías Clave** | Lista las herramientas y conceptos fundamentales involucrados en la práctica (TensorFlow, Python, CUDA, Keras, MNIST). |

## ⚙️ Instalación
Para replicar el entorno de trabajo documentado en esta práctica, siga los siguientes pasos:

1.  **Instalar Python 3.12 (Windows)**:
    Dado que la práctica se centró en un problema de compatibilidad con Python 3.14 y la solución fue un _downgrade_ a Python 3.12, es fundamental instalar esta versión específica. Utilice `winget` en un terminal de Windows con privilegios de administrador:

    ```cmd
    winget install --id Python.Python.3.12 --override "/"
    ```

    Asegúrese de que Python 3.12 esté correctamente añadido a su `PATH` del sistema. Puede verificar la instalación y la versión con:

    ```bash
    python --version
    ```

2.  **Crear un entorno virtual (Recomendado)**:
    Es buena práctica aislar las dependencias del proyecto. Puede usar `venv`:

    ```bash
    python -m venv .venv
    ```

3.  **Activar el entorno virtual**:
    *   En Windows (Command Prompt):
        ```cmd
        .venv\Scripts\activate.bat
        ```
    *   En Windows (PowerShell):
        ```powershell
        .venv\Scripts\Activate.ps1
        ```
    *   En Linux/macOS:
        ```bash
        source .venv/bin/activate
        ```

4.  **Instalar TensorFlow 2.21**:
    Una vez activado el entorno, instale la versión específica de TensorFlow documentada en la práctica. Si desea soporte para GPU, asegúrese de tener instalados CUDA Toolkit y cuDNN compatibles con TensorFlow 2.21 y su versión de Python.

    ```bash
    pip install tensorflow==2.21
    ```

5.  **Verificar la instalación**:
    Puede verificar que TensorFlow se ha instalado correctamente y que detecta las GPUs (si las tiene y ha configurado CUDA/cuDNN) ejecutando un pequeño script de Python:

    ```python
    import tensorflow as tf
    print(f"Versión de TensorFlow: {tf.__version__}")
    print(f"GPUs disponibles: {tf.config.list_physical_devices('GPU')}")
    ```

## 🚀 Uso
Este repositorio se centra principalmente en la documentación del proceso de configuración del entorno para trabajar con TensorFlow y resolver problemas de compatibilidad. Como tal, **no contiene código de aplicación funcional** de Machine Learning. Sin embargo, para ilustrar cómo se usaría TensorFlow una vez configurado el entorno, la práctica original mencionó el uso del conjunto de datos **MNIST** para clasificación de imágenes.

A continuación, se presenta un **ejemplo conceptual** de cómo se podría definir un modelo de red neuronal simple con `tf.keras` para clasificar dígitos MNIST, asumiendo que el entorno está correctamente configurado:

```python
import tensorflow as tf
from tensorflow.keras.datasets import mnist
from tensorflow.keras.models import Sequential
from tensorflow.keras.layers import Dense, Flatten

# 1. Cargar el dataset MNIST
(x_train, y_train), (x_test, y_test) = mnist.load_data()
x_train, x_test = x_train / 255.0, x_test / 255.0 # Normalizar imágenes

# 2. Construir el modelo
model = Sequential([
    Flatten(input_shape=(28, 28)), # Capa de entrada que "aplana" la imagen
    Dense(128, activation='relu'), # Capa oculta con 128 neuronas y activación ReLU
    Dense(10, activation='softmax') # Capa de salida con 10 neuronas (dígitos 0-9) y activación softmax
])

# 3. Compilar el modelo
model.compile(optimizer='adam',
                  loss='sparse_categorical_crossentropy',
                  metrics=['accuracy'])

# 4. Entrenar el modelo (ejemplo no ejecutado en este repo)
# print("Iniciando entrenamiento del modelo (ejemplo conceptual)...")
# model.fit(x_train, y_train, epochs=5)
#
# # 5. Evaluar el modelo
# test_loss, test_acc = model.evaluate(x_test, y_test, verbose=2)
# print(f"\nPrecisión en test: {test_acc}")

print("\nEste código es un ejemplo conceptual de uso de TensorFlow para clasificación MNIST.")
print("El repositorio se enfoca en la documentación del entorno, no en la ejecución de este modelo.")
```
*Nota: El código de ejemplo anterior es ilustrativo y no forma parte del código fuente de este repositorio, el cual se centra en la documentación de la configuración del entorno.*

## 📁 Estructura del proyecto
```
.
├── README.md
└── docs/
    └── Dinamica_Practica_Python_TensorFlow_Miguel_Jerico.md
```

## 🛠️ Tecnologías
| Herramienta | Versión / Detalle | Uso en el proyecto |
| :---------- | :---------------- | :------------------------------------------------------------------------------------- |
| **Python** | 3.12 (específica) | Lenguaje de programación principal para el desarrollo de Machine Learning con TensorFlow. |
| **TensorFlow** | 2.21 | Plataforma de código abierto para ML e IA, foco de la práctica y su configuración. |
| **`tf.keras`** | Integrado en TF 2.x | API de alto nivel para construir y entrenar redes neuronales dentro de TensorFlow. |
| **`winget`** | CLI de Windows | Gestor de paquetes utilizado para la instalación controlada de Python 3.12 en Windows. |
| **CUDA / cuDNN** | (No especificado) | Plataformas de NVIDIA cruciales para la aceleración del entrenamiento de modelos en GPUs con TensorFlow. |
| **MNIST** | Conjunto de datos | Dataset de dígitos escritos a mano, mencionado como ejemplo de uso típico para clasificación de imágenes con TensorFlow. |
| **Redes Neuronales** | Concepto | Tipo de modelo de aprendizaje automático fundamental en el uso de TensorFlow para IA. |

## 📚 Contexto formativo o motivación del proyecto
Este proyecto surge como parte de una actividad del curso "Análisis de Datos e IA" impartido por el INAEM, Bloque II. El objetivo de la actividad era investigar a fondo una librería clave en el ámbito de la Ciencia de Datos y la Inteligencia Artificial, y presentar una demostración práctica. La elección recayó en TensorFlow, dada su relevancia y complejidad, lo que llevó a la exploración detallada de su instalación y configuración del entorno, especialmente en lo referente a la compatibilidad de versiones con Python y la aceleración por hardware.

<p align="center">Desarrollado por @migueljerico y documentado mediante la app Asistente de IA para Publicar Repositorios · 2026</p>
