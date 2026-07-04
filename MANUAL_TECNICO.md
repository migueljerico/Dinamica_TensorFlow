# Documentación Técnica: Dinámica Práctica sobre TensorFlow y Configuración de Entorno Python

## 1. Arquitectura General del Entorno de Desarrollo
```
+---------------------+           +---------------------+           +--------------------------+           +------------------+
| Entorno del Usuario |           | Entorno Python 3.12 |           | TensorFlow 2.21 (Motor C++)|           | Hardware (GPU)   |
| (Desarrollador)     |           |  (Lógica de ML)     |           | (Cálculo Numérico)       |           |  (Aceleración)   |
+----------+----------+           +----------+----------+           +----------+---------------+           +--------+---------+
           |                                |                                    |                                    |
           | Comandos de gestión            | Llamadas a la API                  | Enlace/Drivers                     | Procesamiento Paralelo
           | de entorno (winget, pip)       |                                    | (CUDA Toolkit, cuDNN)              | 
           V                                V                                    V                                    V
+------------------------------------------------------------------------------------------------------------------------------------+
|                                      Sistema Operativo (Windows)                                                                   |
+------------------------------------------------------------------------------------------------------------------------------------+
```

*Descripción:*
La arquitectura conceptual de este proyecto se centra en la pila de software necesaria para ejecutar TensorFlow con soporte GPU. El `Usuario/Desarrollador` interactúa con el `Sistema Operativo` (Windows en este caso) para configurar el `Entorno Python 3.12`. Este entorno aloja la lógica de Machine Learning que utiliza la librería `TensorFlow 2.21`. Dada la naturaleza de TensorFlow como motor en C++, requiere un enlace directo con las bibliotecas de NVIDIA, `CUDA Toolkit` y `cuDNN`, para poder comunicarse y aprovechar la capacidad de procesamiento paralelo del `Hardware (GPU)`. La gestión de compatibilidad entre todas estas capas es el punto neurálgico que documenta este repositorio.

## 2. Descripción de Módulos o Componentes Principales

*   **`README.md`**
    *   **Responsabilidad**: Punto de entrada principal del repositorio. Proporciona una visión general del proyecto, el contexto, la descripción del problema de compatibilidad, una guía rápida de instalación del entorno y una lista de tecnologías clave. Su objetivo es que el usuario obtenga una comprensión inicial y los pasos básicos para empezar.
    *   **Funciones Clave / Secciones**: `Descripción`, `Funcionalidades` (Aspectos cubiertos), `Instalación`, `Uso` (Ejemplo conceptual), `Estructura del proyecto`, `Tecnologías`.

*   **`docs/Dinamica_Practica_Python_TensorFlow_Miguel_Jerico.md`**
    *   **Responsabilidad**: Documentación técnica detallada de la práctica. Profundiza en los motivos técnicos de la incompatibilidad de versiones de Python con TensorFlow y CUDA, explicando el desfase en los ciclos de lanzamiento, las dependencias de C/C++ y la ausencia de _wheels_ precompilados. Es el manual técnico subyacente que justifica las decisiones de configuración.
    *   **Funciones Clave / Secciones**: `Resumen`, `Puntos clave`, `Detalle` (con `Contexto de la Actividad`, `Librería Investigada`, `Problema de Compatibilidad y Preparación del Entorno Python`), `Instalación de Python 3.12`, `Tecnologías y Conceptos Relevantes Utilizados`, `Conclusiones / siguientes pasos`.

*   **Componentes conceptuales del entorno**:
    *   **Python 3.12**:
        *   **Responsabilidad**: Lenguaje de programación anfitrión para el desarrollo de modelos de Machine Learning. La versión 3.12 fue seleccionada específicamente por su compatibilidad certificada con TensorFlow 2.21 y el ecosistema CUDA/cuDNN de NVIDIA.
    *   **TensorFlow 2.21**:
        *   **Responsabilidad**: Plataforma de código abierto para computación numérica y Machine Learning. Proporciona las herramientas y APIs para construir, entrenar y desplegar modelos de IA, incluyendo redes neuronales profundas. Es el núcleo de la funcionalidad de ML.
    *   **CUDA Toolkit (NVIDIA)**:
        *   **Responsabilidad**: Un kit de desarrollo de software de NVIDIA que permite a los desarrolladores utilizar las GPUs de NVIDIA para computación de propósito general. Es indispensable para que TensorFlow pueda ejecutar cálculos intensivos en el hardware de la GPU.
    *   **cuDNN (NVIDIA)**:
        *   **Responsabilidad**: Una biblioteca de primitivas de redes neuronales profundas (DNN) aceleradas por GPU, proporcionada por NVIDIA. cuDNN se integra con TensorFlow para optimizar operaciones comunes en DNNs (convoluciones, _pooling_, normalización, etc.), mejorando significativamente el rendimiento del entrenamiento.

## 3. APIs y Endpoints Documentados
Este repositorio no implementa ninguna API o endpoint. Su propósito es la documentación de la configuración de un entorno de desarrollo para Machine Learning.

## 4. Variables de Entorno
No se definen variables de entorno específicas para el funcionamiento directo de este repositorio en la documentación provista, ya que se centra en la instalación de Python y TensorFlow. Sin embargo, en un entorno de trabajo real con CUDA/cuDNN, es común que se necesite configurar variables como `PATH` para incluir los directorios binarios de CUDA y `LD_LIBRARY_PATH` (en Linux) o `PATH` (en Windows) para las bibliotecas de cuDNN. La instalación a través de `winget` y `pip` suele manejar gran parte de esto, pero la configuración manual de CUDA/cuDNN puede requerir verificación.

## 5. Guía de Despliegue (Configuración de Entorno) Paso a Paso
La "guía de despliegue" para este repositorio se refiere a la configuración del entorno de desarrollo para trabajar con TensorFlow y soporte GPU en un sistema Windows.

1.  **Verificar Sistema Operativo y Hardware**:
    *   Asegúrese de estar utilizando Windows.
    *   Verifique que su sistema cuenta con una GPU compatible con NVIDIA y que los controladores más recientes están instalados.

2.  **Instalar Python 3.12**:
    *   Abra un terminal de comandos (CMD o PowerShell) como administrador.
    *   Ejecute el comando para instalar Python 3.12 utilizando `winget`:
        ```cmd
        winget install --id Python.Python.3.12 --override "/"
        ```
    *   Verifique la instalación:
        ```bash
        python --version
        ```

3.  **Configurar entorno virtual (Altamente recomendado)**:
    *   Navegue a la carpeta de su proyecto.
    *   Cree un entorno virtual:
        ```bash
        python -m venv .venv
        ```
    *   Active el entorno virtual:
        *   Windows CMD: `.venv\Scripts\activate.bat`
        *   Windows PowerShell: `.venv\Scripts\Activate.ps1`

4.  **Instalar CUDA Toolkit y cuDNN (si desea soporte GPU)**:
    *   TensorFlow 2.21 requiere versiones específicas de CUDA Toolkit y cuDNN. Investigue la compatibilidad exacta en la documentación de TensorFlow para la versión 2.21.
    *   Descargue e instale el `CUDA Toolkit` compatible desde el sitio web de NVIDIA.
    *   Descargue `cuDNN` compatible y descomprímalo en su directorio de instalación de CUDA o en una ubicación accesible en el `PATH` del sistema.
    *   Asegúrese de que las variables de entorno para CUDA y cuDNN estén configuradas correctamente (`PATH`, `CUDA_PATH`, etc.).

5.  **Instalar TensorFlow 2.21**:
    *   Con el entorno virtual activado, instale TensorFlow:
        ```bash
        pip install tensorflow==2.21
        ```
    *   Si desea la versión con soporte para GPU (asumiendo que CUDA/cuDNN están instalados), el mismo comando `pip install tensorflow` debería instalar la versión con soporte GPU si su entorno y la configuración de NVIDIA son correctos.

6.  **Verificar la instalación de TensorFlow**:
    *   Desde su terminal con el entorno virtual activado, inicie el intérprete de Python y ejecute:
        ```python
        import tensorflow as tf
        print(f"Versión de TensorFlow: {tf.__version__}")
        print(f"GPUs disponibles: {tf.config.list_physical_devices('GPU')}")
        ```
        Si `tf.config.list_physical_devices('GPU')` muestra su GPU, la configuración es exitosa.

## 6. Limitaciones Conocidas y Posibles Mejoras Futuras

*   **Limitaciones Conocidas**:
    *   **Dependencia de Versiones Estrictas**: El proyecto destaca una fuerte dependencia de versiones específicas de Python (3.12) y TensorFlow (2.21) para garantizar la compatibilidad con CUDA/cuDNN. Esto puede volverse obsoleto rápidamente a medida que salen nuevas versiones.
    *   **Enfoque en Windows**: La guía de instalación utiliza `winget`, lo que la hace específica para entornos Windows. No se proporcionan instrucciones para Linux o macOS.
    *   **Ausencia de Código de Aplicación**: El repositorio documenta la configuración del entorno, pero no incluye un proyecto funcional de Machine Learning que demuestre el uso de TensorFlow.
    *   **Detalles de CUDA/cuDNN**: Aunque se menciona su importancia, los detalles exactos de instalación y compatibilidad de CUDA Toolkit y cuDNN para TF 2.21 no se profundizan, lo cual es un paso crítico.

*   **Posibles Mejoras Futuras**:
    *   **Actualización de Compatibilidad**: Mantener la documentación actualizada con las últimas versiones compatibles de Python, TensorFlow, CUDA y cuDNN.
    *   **Soporte Multiplataforma**: Expandir la guía de instalación para incluir instrucciones detalladas para sistemas operativos Linux y macOS.
    *   **Integración de Entornos Virtuales Avanzados**: Ofrecer ejemplos de uso de `conda` o `pipenv` para una gestión de entornos más robusta y reproducible.
    *   **Añadir un Ejemplo Funcional**: Incluir un pequeño script de TensorFlow que demuestre la carga de datos (ej. MNIST), la construcción, entrenamiento y evaluación de un modelo simple para verificar la funcionalidad completa del entorno.
    *   **Guía Detallada de CUDA/cuDNN**: Proporcionar pasos más específicos y recursos para la instalación y verificación de CUDA Toolkit y cuDNN para las versiones relevantes.
    *   **Automatización de la Configuración**: Explorar scripts (e.g., PowerShell, Bash) para automatizar parte del proceso de configuración del entorno.