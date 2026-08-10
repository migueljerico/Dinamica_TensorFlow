# Documentación Técnica: Dinámica Práctica sobre TensorFlow y Configuración de Entorno Python

**Versión:** 1.1  
**Fecha de actualización:** 10 de agosto de 2026  
**Repositorio:** [migueljerico/Dinamica_TensorFlow](https://github.com/migueljerico/Dinamica_TensorFlow)  
**Autor:** Miguel Jericó

---

## 1. Arquitectura General del Entorno de Desarrollo

La arquitectura conceptual de este proyecto describe la pila de software necesaria para ejecutar TensorFlow con soporte de GPU, enfatizando la gestión de compatibilidad entre versiones. El siguiente diagrama ASCII muestra las capas que intervienen y su interacción:

```
+---------------------+           +---------------------+           +--------------------------+           +------------------+
| Entorno del Usuario |           | Entorno Python 3.12 |           | TensorFlow 2.21         |           | Hardware (GPU)   |
| (Desarrollador)     |---------->|  (Lógica de ML)     |---------->| (Motor C++)             |---------->|  (Aceleración)   |
+---------------------+           +---------------------+           +--------------------------+           +------------------+
      |                                    |                                    |                                    |
      |  Comandos de gestión               |  Llamadas a la API                  |  Enlace/Drivers                     |  Procesamiento
      |  (winget, pip, venv)               |  (tf.keras, tf.data)                |  (CUDA Toolkit, cuDNN)              |  paralelo
      V                                    V                                    V                                    V
+------------------------------------------------------------------------------------------------------------------------------------+
|                                      Sistema Operativo (Windows)                                                                   |
+------------------------------------------------------------------------------------------------------------------------------------+
```

**Descripción de las capas:**

- **Capa de presentación (Entorno del Usuario):** Incluye las herramientas de gestión de paquetes (winget, pip, venv) que el desarrollador utiliza para configurar el sistema. Esta capa interactúa directamente con el sistema operativo para instalar y mantener las dependencias.

- **Capa de lógica (Entorno Python 3.12):** Contiene la implementación de los modelos de Machine Learning. Python 3.12 fue seleccionado específicamente por su compatibilidad certificada con TensorFlow 2.21 y el ecosistema NVIDIA CUDA/cuDNN. Aquí se ejecutan los scripts que utilizan las APIs de TensorFlow.

- **Capa de datos/API (TensorFlow 2.21):** TensorFlow actúa como motor de cálculo numérico escrito en C++, con enlaces para Python. Proporciona las herramientas para construir, entrenar y evaluar modelos. Para aprovechar la GPU, esta capa se enlaza con las bibliotecas NVIDIA.

- **Capa de hardware (GPU):** La tarjeta gráfica NVIDIA ejecuta operaciones de cómputo paralelo a través de CUDA, acelerando significativamente el entrenamiento de redes neuronales.

La gestión de compatibilidad entre estas capas es el punto neurálgico que documenta este repositorio. Un cambio de versión en una de ellas (por ejemplo, Python 3.14) puede romper todo el flujo, como se explica en las secciones siguientes.

---

## 2. Estructura del Proyecto

```
Dinamica_TensorFlow/
├── README.md                                    # Vista general del proyecto y guía rápida de instalación
├── MANUAL_TECNICO.md                            # Documentación técnica detallada (este manual)
└── docs/
    └── Dinamica_Practica_Python_TensorFlow_Miguel_Jerico.md   # Informe completo de la práctica
```

**Descripción de archivos:**

| Archivo | Responsabilidad |
|---------|-----------------|
| `README.md` | Punto de entrada principal. Proporciona una visión general, contexto, funcionalidades, pasos de instalación y uso, y lista de tecnologías. |
| `MANUAL_TECNICO.md` | Manual técnico exhaustivo que cubre arquitectura, módulos, despliegue, limitaciones y mejoras. |
| `docs/Dinamica_Practica_Python_TensorFlow_Miguel_Jerico.md` | Informe técnico de la práctica, detallando el problema de compatibilidad, el proceso de downgrade y las razones técnicas. |

---

## 3. Descripción de Módulos o Componentes Principales

### 3.1 Archivos del repositorio

#### `README.md`
- **Responsabilidad:** Actúa como la puerta de entrada del repositorio. Ofrece una descripción general, los objetivos de la práctica y una guía rápida de instalación para entornos Windows.
- **Secciones destacadas:** Descripción, Funcionalidades (tabla), Instalación, Uso, Estructura del proyecto, Tecnologías.

#### `docs/Dinamica_Practica_Python_TensorFlow_Miguel_Jerico.md`
- **Responsabilidad:** Documento técnico principal que profundiza en los motivos de la incompatibilidad de Python 3.14 con TensorFlow 2.21 y CUDA, el proceso de downgrade a Python 3.12 y las tecnologías involucradas.
- **Secciones destacadas:** Resumen, Puntos clave, Detalle (Contexto de la Actividad, Librería Investigada, Problema de Compatibilidad, Instalación de Python 3.12), Tecnologías y Conceptos, Conclusiones.

### 3.2 Componentes conceptuales del entorno

#### Python 3.12
- **Responsabilidad:** Lenguaje de programación anfitrión para el desarrollo de modelos de Machine Learning. La versión 3.12 fue elegida por su soporte certificado con TensorFlow 2.21 y el ecosistema CUDA/cuDNN de NVIDIA.
- **Justificación:** Python 3.14 era demasiado reciente y no contaba con _wheels_ precompilados para TensorFlow 2.21, lo que causaba errores de instalación.

#### TensorFlow 2.21
- **Responsabilidad:** Plataforma de código abierto para computación numérica y Machine Learning. Proporciona APIs de alto nivel (`tf.keras`), herramientas de preprocesamiento de datos (`tf.data`) y soporte para aceleración por GPU.
- **Integración:** Requiere enlazarse con CUDA Toolkit y cuDNN para utilizar GPUs NVIDIA.

#### CUDA Toolkit (NVIDIA)
- **Responsabilidad:** Kit de desarrollo de software que permite a los desarrolladores usar GPUs NVIDIA para cómputo de propósito general. Proporciona las librerías y herramientas necesarias para que TensorFlow ejecute operaciones en la GPU.
- **Compatibilidad:** Debe existir una versión específica certificada para cada versión de TensorFlow y Python.

#### cuDNN (NVIDIA)
- **Responsabilidad:** Biblioteca de primitivas para redes neuronales profundas (DNN) aceleradas por GPU. Optimiza operaciones como convoluciones, pooling y normalización, mejorando el rendimiento del entrenamiento.

#### Tecnologías adicionales mencionadas
- **`tf.keras`:** API de alto nivel de TensorFlow para construir y entrenar modelos de redes neuronales.
- **MNIST:** Conjunto de datos de dígitos manuscritos, utilizado como ejemplo de clasificación de imágenes.
- **Redes neuronales:** Modelos de aprendizaje automático inspirados en el cerebro humano, implementados mediante TensorFlow.

---

## 4. APIs y Endpoints Documentados

Este repositorio **no implementa ninguna API REST o endpoints web**. Su propósito es la documentación de la configuración del entorno de desarrollo. Sin embargo, se hace referencia a las APIs internas de TensorFlow:

| API | Descripción |
|-----|-------------|
| `tensorflow` | Importación principal de la librería. |
| `tf.keras` | API de alto nivel para construcción de modelos secuenciales y funcionales. |
| `tf.config.list_physical_devices('GPU')` | Función para verificar la disponibilidad de GPUs. |
| `tf.__version__` | Atributo para consultar la versión instalada de TensorFlow. |

No se documentan endpoints HTTP porque no existe un servidor o servicio web en el proyecto.

---

## 5. Variables de Entorno

Aunque el repositorio no define variables de entorno específicas para su ejecución, el correcto funcionamiento de TensorFlow con GPU requiere la configuración de variables del sistema relacionadas con CUDA y cuDNN. A continuación se listan las más relevantes:

| Variable | Valor de ejemplo | Obligatoria | Descripción |
|----------|------------------|-------------|-------------|
| `PATH` | `C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v12.2\bin` | Sí (para CUDA) | Debe incluir los directorios binarios de CUDA Toolkit y cuDNN para que TensorFlow pueda encontrar las librerías dinámicas (`.dll` en Windows, `.so` en Linux). |
| `CUDA_PATH` | `C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v12.2` | Recomendada | Ruta base de instalación de CUDA Toolkit. Algunas herramientas la requieren. |
| `LD_LIBRARY_PATH` (Linux/macOS) | `/usr/local/cuda/lib64` | Sí en Linux | Indica la ruta a las librerías compartidas de CUDA y cuDNN. |
| `TF_CPP_MIN_LOG_LEVEL` | `2` | No | Opcional. Reduce la verbosidad de los logs de TensorFlow. |

**Nota:** Si se instala CUDA Toolkit y cuDNN mediante los instaladores oficiales en Windows, el `PATH` se actualiza automáticamente. En entornos Linux, la configuración manual suele ser necesaria.

---

## 6. Guía de Despliegue (Configuración de Entorno) Paso a Paso

La siguiente guía describe cómo configurar un entorno de desarrollo para TensorFlow 2.21 con soporte GPU en Windows. Se asume que el usuario tiene conocimientos básicos de línea de comandos.

### 6.1 Requisitos previos
- Sistema operativo Windows (10 u 11) o Linux.
- GPU NVIDIA con controladores actualizados.
- Conexión a Internet para descargar paquetes.

### 6.2 Instalación de Python 3.12

1. **Verificar la versión actual de Python** (si existe alguna instalación previa):
   ```bash
   python --version
   ```

2. **Instalar Python 3.12** usando `winget` (Windows) o el instalador oficial:
   ```cmd
   winget install --id Python.Python.3.12 --override "/"
   ```

3. **Verificar la instalación**:
   ```bash
   python --version
   ```
   Debe mostrar `Python 3.12.x`.

### 6.3 Creación y activación de un entorno virtual

Es una buena práctica aislar las dependencias del proyecto.

```bash
# Crear entorno virtual
python -m venv .venv

# Activar entorno (Windows - CMD)
.venv\Scripts\activate.bat

# Activar entorno (Windows - PowerShell)
.venv\Scripts\Activate.ps1

# Activar entorno (Linux/macOS)
source .venv/bin/activate
```

### 6.4 Instalación de CUDA Toolkit y cuDNN (para soporte GPU)

TensorFlow 2.21 requiere versiones específicas de CUDA y cuDNN. Según la [documentación oficial de TensorFlow](https://www.tensorflow.org/install/source#gpu), para la versión 2.21 se necesita:

- CUDA Toolkit 12.2 o superior (recomendado 12.3)
- cuDNN 8.9 o superior

**Pasos:**

1. Descargar e instalar el [CUDA Toolkit](https://developer.nvidia.com/cuda-toolkit-archive) desde el sitio de NVIDIA. Seleccionar la versión compatible.
2. Descargar [cuDNN](https://developer.nvidia.com/cudnn) (requiere registro gratuito) y descomprimir los archivos en el directorio de instalación de CUDA (por defecto `C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v12.2`).
3. Asegurarse de que las variables de entorno `PATH` y `CUDA_PATH` estén configuradas correctamente. En Windows, el instalador suele hacerlo automáticamente.

**Verificación de CUDA:**
```bash
nvcc --version
```
Debe mostrar la versión instalada.

### 6.5 Instalación de TensorFlow 2.21

Con el entorno virtual activado:

```bash
pip install tensorflow==2.21
```

Para instalar la versión con soporte GPU (si CUDA y cuDNN están correctamente instalados), el mismo comando instala la versión que detecta automáticamente las GPUs.

### 6.6 Verificación de la instalación

Ejecutar el siguiente script en Python:

```python
import tensorflow as tf

print(f"Versión de TensorFlow: {tf.__version__}")
print(f"GPUs disponibles: {tf.config.list_physical_devices('GPU')}")

# Prueba rápida con MNIST (opcional)
mnist = tf.keras.datasets.mnist
(x_train, y_train), (x_test, y_test) = mnist.load_data()
x_train, x_test = x_train / 255.0, x_test / 255.0

model = tf.keras.models.Sequential([
    tf.keras.layers.Flatten(input_shape=(28, 28)),
    tf.keras.layers.Dense(128, activation='relu'),
    tf.keras.layers.Dropout(0.2),
    tf.keras.layers.Dense(10, activation='softmax')
])

model.compile(optimizer='adam',
              loss='sparse_categorical_crossentropy',
              metrics=['accuracy'])

model.fit(x_train, y_train, epochs=1)
```

Si la configuración es correcta, el modelo se entrenará sin errores y se mostrará la lista de GPUs disponibles.

---

## 7. Limitaciones Conocidas y Posibles Mejoras Futuras

### 7.1 Limitaciones Conocidas

| Limitación | Descripción |
|------------|-------------|
| **Dependencia estricta de versiones** | El proyecto requiere versiones específicas de Python (3.12), TensorFlow (2.21), CUDA y cuDNN. Cambios en estas versiones pueden romper la compatibilidad. |
| **Enfoque en Windows** | La guía de instalación utiliza `winget` y comandos específicos de Windows. No se incluyen instrucciones detalladas para Linux o macOS. |
| **Ausencia de código de aplicación** | El repositorio documenta la configuración del entorno, pero no incluye un proyecto funcional de Machine Learning que demuestre el uso de TensorFlow. |
| **Instalación manual de CUDA/cuDNN** | Los detalles exactos de instalación y compatibilidad de CUDA y cuDNN no se profundizan, lo cual es un paso crítico para el soporte GPU. |
| **Documentación limitada sobre variables de entorno** | No se proporcionan ejemplos concretos de configuración de `PATH` y `CUDA_PATH` para diferentes sistemas operativos. |

### 7.2 Posibles Mejoras Futuras

1. **Actualizar la documentación de compatibilidad** con las últimas versiones de Python, TensorFlow, CUDA y cuDNN.
2. **Ampliar la guía a múltiples plataformas**, incluyendo instrucciones detalladas para Linux y macOS.
3. **Integrar herramientas de gestión de entornos más avanzadas**, como `conda` o `pipenv`, para una reproducibilidad mejorada.
4. **Añadir un ejemplo funcional completo**, como un script de clasificación de MNIST con entrenamiento y evaluación, para verificar todo el flujo.
5. **Proporcionar una guía paso a paso para la instalación y verificación de CUDA/cuDNN**, con capturas de pantalla y comandos de diagnóstico.
6. **Automatizar la configuración del entorno** mediante scripts (PowerShell o Bash) que instalen todas las dependencias con una sola ejecución.

---

## 8. Referencias

- [Documentación oficial de TensorFlow](https://www.tensorflow.org/)
- [Guía de instalación de TensorFlow con GPU](https://www.tensorflow.org/install/gpu)
- [CUDA Toolkit Archive](https://developer.nvidia.com/cuda-toolkit-archive)
- [cuDNN Downloads](https://developer.nvidia.com/cudnn)
- [Python Releases](https://www.python.org/downloads/)

---

*Este manual técnico se actualiza a medida que evoluciona el repositorio. Para contribuciones o correcciones, por favor abra un issue o pull request en GitHub.*

<p align="center">Creado por <a href="https://github.com/migueljerico">@migueljerico</a> y documentado por QwenCloud (deepseek-v4-flash-0731) desde la App Asistente de IA · 2026</p>