# Model Card · Fashion-MNIST CNN

# Model Card · Fashion-MNIST CNN

## Modelo y versión
Modelo de clasificación de imágenes desarrollado para el laboratorio U02.LAB07 de la asignatura INF-8239 Ciencia de Datos II.

Se evaluaron dos arquitecturas sobre Fashion-MNIST:

- Baseline denso.
- Red neuronal convolucional (CNN).

La configuración final evaluada de la CNN fue entrenada durante 8 épocas y guardada como:

`models/best_cnn.keras`

Entorno utilizado:

- Python 3.12.14
- TensorFlow 2.21.0
- Sistema operativo: Windows 11
- Ejecución por CPU
- GPU detectada: ninguna

## Uso previsto
El modelo fue desarrollado con fines académicos y didácticos para comparar una red densa y una red convolucional en un problema de clasificación multiclase de imágenes.

Su uso previsto es:

- demostrar un flujo reproducible de visión computacional;
- comparar desempeño predictivo y costo computacional;
- analizar errores por clase;
- estudiar diferencias entre una arquitectura densa y una CNN;
- documentar resultados mediante métricas, pruebas y evidencias visuales.

## Usos fuera de alcance
El modelo no debe utilizarse para:

- diagnóstico médico;
- reconocimiento de personas;
- vigilancia;
- decisiones automatizadas de alto impacto;
- OCR;
- clasificación de imágenes reales fuera del dominio Fashion-MNIST;
- aplicaciones comerciales sin validación adicional.

Un buen resultado sobre Fashion-MNIST no implica capacidad de generalización hacia otros dominios visuales.

## Dataset y particiones
Se utilizó Fashion-MNIST, un conjunto de datos público compuesto por imágenes de prendas de vestir.

Características principales:

- 60,000 imágenes para entrenamiento.
- 10,000 imágenes para prueba.
- Imágenes en escala de grises.
- Resolución de 28 × 28 píxeles.
- 10 clases.
- 1,000 observaciones por clase en el conjunto de prueba.

Clases utilizadas:

0. T-shirt/top
1. Trouser
2. Pullover
3. Dress
4. Coat
5. Sandal
6. Shirt
7. Sneaker
8. Bag
9. Ankle boot

Los modelos fueron evaluados bajo el mismo esquema de datos para garantizar una comparación justa.

## Preprocesamiento
Las imágenes fueron cargadas mediante el flujo definido en el proyecto base.

El preprocesamiento incluyó:

- conversión a valores numéricos normalizados;
- conservación de la estructura 28 × 28 para la CNN;
- aplanado de la imagen en el modelo denso;
- uso de las mismas particiones para ambos modelos.

No se modificó la partición de prueba para favorecer ningún modelo.

## Métricas globales y por clase
Los resultados obtenidos fueron:

### Baseline denso

- F1 macro: 0.8634
- Parámetros: 50,890
- Tiempo de entrenamiento: 15.84 segundos
- Tiempo de inferencia: 0.0917 ms por imagen

### CNN

- F1 macro: 0.7889
- Parámetros: 19,466
- Tiempo de entrenamiento: 166.14 segundos
- Tiempo de inferencia: 0.1766 ms por imagen

La clase con mayor dificultad para la CNN fue la clase 6 (`Shirt`), con aproximadamente:

- Precision: 0.499
- Recall: 0.371
- F1-score: 0.425

Los errores visuales mostraron confusiones frecuentes entre clases con siluetas semejantes, especialmente:

- Coat ↔ Pullover
- Shirt ↔ Coat
- Shirt ↔ T-shirt/top
- Dress ↔ T-shirt/top
- Ankle boot ↔ Sneaker
- Sandal ↔ Sneaker

## Comparación de costo
- Hardware: CPU en Windows 11, sin GPU disponible.
- Parámetros:
  - Denso: 50,890
  - CNN: 19,466
- Tiempo de entrenamiento:
  - Denso: 15.84 s
  - CNN: 166.14 s
- Tiempo de inferencia:
  - Denso: 0.0917 ms/imagen
  - CNN: 0.1766 ms/imagen

Aunque la CNN utilizó menos parámetros, presentó un costo temporal significativamente mayor y un F1 macro inferior al baseline denso.

En esta ejecución concreta, la mejora esperada por usar una arquitectura convolucional no compensó el mayor costo computacional.

## Limitaciones y riesgos
Las principales limitaciones son:

- Fashion-MNIST es un benchmark didáctico simplificado.
- Las imágenes tienen baja resolución.
- El conjunto está restringido a 10 categorías de prendas.
- Las imágenes son en escala de grises.
- Algunas categorías presentan siluetas visualmente similares.
- El rendimiento observado no garantiza desempeño en imágenes reales.
- La clase `Shirt` mostró una debilidad importante en la CNN.
- Los resultados dependen del entorno, configuración y condiciones de entrenamiento.

El modelo no debe extrapolarse directamente a otros dominios.

## Supervisión y monitoreo
Antes de utilizar un modelo derivado de este trabajo en otro contexto se recomienda:

- validar con datos del nuevo dominio;
- revisar métricas por clase;
- analizar falsos positivos y falsos negativos;
- monitorear cambios en la distribución de datos;
- registrar hardware y tiempos de ejecución;
- comparar el costo computacional con la mejora obtenida;
- mantener supervisión humana;
- volver a entrenar y evaluar cuando cambien los datos.

La salida del modelo debe interpretarse como una predicción condicionada por los datos y no como una verdad absoluta.
