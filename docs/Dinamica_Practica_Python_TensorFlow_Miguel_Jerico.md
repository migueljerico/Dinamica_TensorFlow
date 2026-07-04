# Documentación Técnica: Dinámica Práctica sobre TensorFlow y Configuración de Entorno Python

## 📋 Resumen
Este documento detalla una práctica sobre la librería TensorFlow, cubriendo su propósito en Inteligencia Artificial y Aprendizaje Automático. Se enfoca en la crucial preparación del entorno Python, explicando los motivos y el proceso para asegurar la compatibilidad con TensorFlow y las tecnologías de aceleración de GPU como CUDA.

## 🔑 Puntos clave
- **TensorFlow** es una plataforma de código abierto de Google para construir, entrenar y desplegar modelos de aprendizaje automático e inteligencia artificial.
- La **compatibilidad de versiones de Python** es un factor crítico para la instalación y el funcionamiento correcto de TensorFlow, especialmente con soporte para GPU (CUDA).
- Se realizó un **_downgrade_ de Python 3.14 a Python 3.12** debido a incompatibilidades con TensorFlow 2.21 y el ecosistema CUDA de NVIDIA.
- Las razones de la incompatibilidad incluyen el **desfase en el ciclo de lanzamientos** (falta de _wheels_ precompilados para Python 3.14), las **dependencias de C/C++** y los controladores de NVIDIA, y la **ausencia de paquetes precompilados** (_wheels_) específicos.
- TensorFlow, al ser un motor en C++, requiere **enlazarse con CUDA Toolkit y cuDNN** para aprovechar el hardware de GPU.

## 📝 Detalle

### Contexto de la Actividad
La actividad, parte del curso "Análisis de Datos e IA" del INAEM, tuvo como objetivo investigar una librería de Python para Ciencia de Datos e Inteligencia Artificial y presentar una demostración práctica. La investigación se centró en **TensorFlow**, una plataforma de código abierto creada por Google para el desarrollo, entrenamiento y despliegue de modelos de Machine Learning e IA. El enfoque práctico incluyó la preparación del entorno, la instalación de dependencias y la ejecución de código.

*   **Autor:** Miguel Jericó
*   **Fecha:** Julio 2026
*   **Curso:** INAEM · Análisis de Datos e IA · Bloque II

### Librería Investigada: TensorFlow
TensorFlow es una plataforma robusta y flexible utilizada para una amplia gama de tareas de Machine Learning, desde modelos simples hasta redes neuronales profundas. Su arquitectura permite una gran eficiencia, especialmente cuando se integra con aceleración por hardware.

### Problema de Compatibilidad y Preparación del Entorno Python
Un punto crítico de la práctica fue la necesidad de ajustar la versión de Python antes de instalar TensorFlow. La versión inicial del equipo, Python 3.14, resultó ser incompatible con la versión de TensorFlow (TensorFlow 2.21) y sus dependencias.

Por ello, se realizó un _**downgrade**_ a **Python 3.12**. Los motivos técnicos para esta decisión, documentados en las notas de versión de TensorFlow y CUDA, fueron los siguientes:

#### 1. Desfase en el ciclo de lanzamientos
*   Python 3.14 era una versión muy reciente.
*   TensorFlow 2.21 tiene soporte optimizado para Python 3.10 hasta 3.13.
*   Los archivos binarios oficiales (_wheels_) para la estructura interna de Python 3.14 aún no habían sido compilados, lo que provocaba errores inmediatos al intentar la instalación.

#### 2. Dependencias de C/C++ y controladores de NVIDIA (CUDA)
*   TensorFlow es un motor principal escrito en C++ que interactúa directamente con el hardware.
*   Para utilizar la GPU, TensorFlow necesita enlazarse con los controladores de NVIDIA (CUDA Toolkit y cuDNN).
*   Estas herramientas de NVIDIA requieren ser testeadas y adaptadas para cada nueva versión de Python, especialmente en su API de C. Python 3.14 era demasiado nuevo, y NVIDIA y Google aún no habían certificado esa combinación.

#### 3. Ausencia de "wheels" precompilados
*   El gestor de paquetes `pip` busca archivos precompilados (`.whl`) que coincidan exactamente con el sistema operativo, la arquitectura y la versión de Python.
*   Al no existir un paquete que indicara compatibilidad con "Python 3.14 y CUDA" en los servidores de PyPI, la instalación de TensorFlow fallaba con el error `No matching distribution found`.

### Instalación de Python 3.12
Para resolver el problema de compatibilidad, se utilizó el siguiente comando en Windows para instalar Python 3.12:

```cmd
winget install --id Python.Python.3.12 --override "/"
```

### Tecnologías y Conceptos Relevantes Utilizados
*   **TensorFlow 2.21:** Versión específica de la librería principal.
*   **Python 3.12:** Versión de Python seleccionada para la compatibilidad.
*   **`tf.keras`:** API de alto nivel dentro de TensorFlow para la construcción y entrenamiento de modelos de redes neuronales.
*   **MNIST:** Conjunto de datos de dígitos escritos a mano, frecuentemente utilizado como "Hola Mundo" en Machine Learning para clasificación de imágenes.
*   **CUDA / cuDNN:** Plataformas y bibliotecas de NVIDIA que permiten la computación paralela en GPUs, esenciales para acelerar el entrenamiento de modelos de Machine Learning con TensorFlow.
*   **Redes neuronales:** Tipo de modelos de aprendizaje automático inspirados en el cerebro humano, que TensorFlow facilita su implementación.

## ✅ Conclusiones / siguientes pasos
Esta práctica subraya la importancia crítica de la **gestión de entornos y la verificación de compatibilidad de versiones** al trabajar con librerías complejas como TensorFlow, especialmente cuando se busca aprovechar la aceleración por hardware (GPU). Asegurar un entorno estable y compatible es un paso fundamental antes de sumergirse en la implementación de modelos de Machine Learning. El proceso de _downgrade_ y la comprensión de sus motivos técnicos son un claro ejemplo de los desafíos y soluciones en la configuración de un entorno de desarrollo de IA.