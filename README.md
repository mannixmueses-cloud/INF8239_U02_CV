# INF-8239 · Unidad 02 · Proyecto de visión

Autor académico: Edwin Ramón José Nolasco

## CPU
```bash
uv python install 3.12
uv sync --extra cpu
uv run python scripts/check_runtime.py
uv run python scripts/train_cv.py --epochs 8
```

## GPU
La ruta GPU se utiliza solamente en WSL2/Linux con NVIDIA correctamente configurada:
```bash
uv sync --extra gpu
```

Resultados LAB07
Cierre interpretativo
Uso de IA

## Resultados LAB07

Se ejecutó el laboratorio U02.LAB07 utilizando Fashion-MNIST para comparar un modelo denso de referencia y una red neuronal convolucional (CNN) bajo condiciones reproducibles.

### Resultados principales

| Métrica | Baseline denso | CNN |
|---|---:|---:|
| F1 macro | 0.8634 | 0.7889 |
| Parámetros | 50,890 | 19,466 |
| Tiempo de entrenamiento | 15.84 s | 166.14 s |
| Inferencia por imagen | 0.0917 ms | 0.1766 ms |

En esta ejecución, el modelo denso obtuvo un F1 macro superior y necesitó considerablemente menos tiempo de entrenamiento. Aunque la CNN utilizó menos parámetros, presentó mayor costo temporal y peor desempeño predictivo.

### Clase con mayor dificultad

La clase con mayor dificultad para la CNN fue la clase 6 (`Shirt`), con aproximadamente:

- Precision: 0.499
- Recall: 0.371
- F1-score: 0.425

### Análisis de errores visuales

El archivo `reports/cnn_errors.png` mostró errores principalmente entre categorías visualmente semejantes.

Entre las confusiones observadas se encuentran:

- `Coat` ↔ `Pullover`
- `Shirt` ↔ `Coat`
- `Shirt` ↔ `T-shirt/top`
- `Dress` ↔ `T-shirt/top`
- `Ankle boot` ↔ `Sneaker`
- `Sandal` ↔ `Sneaker`

Estas confusiones pueden relacionarse con la baja resolución de Fashion-MNIST, el uso de imágenes en escala de grises y la similitud de las siluetas entre determinadas categorías.

### Evidencias generadas

El entrenamiento produjo las siguientes evidencias:

- `reports/cv_metrics.json`
- `reports/confusion_cnn.png`
- `reports/cnn_errors.png`
- `models/best_cnn.keras`

Las pruebas automatizadas finalizaron correctamente con:

`3 passed`

## Cierre interpretativo LAB07

### Resultado principal
El modelo denso superó a la CNN en F1 macro dentro de esta ejecución, con un valor aproximado de 0.8634 frente a 0.7889.

### Evidencia predictiva
La comparación se realizó utilizando el mismo dataset y esquema de evaluación. Los resultados quedaron registrados en `reports/cv_metrics.json`, además de la matriz de confusión y las evidencias visuales de error.

### Clase más difícil
La clase 6 (`Shirt`) fue la más difícil para la CNN, con recall aproximado de 0.371 y F1 de 0.425.

### Costo comparado
El baseline denso utilizó 50,890 parámetros y tardó aproximadamente 15.84 segundos en entrenarse. La CNN utilizó 19,466 parámetros, pero requirió aproximadamente 166.14 segundos de entrenamiento.

### ¿La mejora justifica el costo?
En esta ejecución, no se observó una mejora predictiva que justificara el costo adicional de la CNN. El modelo denso obtuvo mejor F1 macro, menor tiempo de entrenamiento y menor tiempo de inferencia.

### Limitación del benchmark
Fashion-MNIST es un benchmark didáctico con imágenes de baja resolución, en escala de grises y limitado a diez categorías de prendas. Por ello, los resultados no deben extrapolarse directamente a imágenes médicas, OCR, vigilancia ni otros dominios.

### Decisión antes de usar otro dominio
Antes de reutilizar alguno de estos modelos en otro dominio sería necesario recopilar o seleccionar datos representativos, redefinir el preprocesamiento, volver a entrenar, evaluar las métricas por clase y validar que el costo computacional se justifique frente al desempeño obtenido.

## Uso de herramientas de IA

Se utilizó ChatGPT como apoyo para:

- interpretar instrucciones del laboratorio;
- explicar errores y resultados;
- revisar métricas;
- redactar documentación técnica;
- organizar el README y el Model Card.

Prompts relevantes utilizados incluyeron solicitudes para explicar paso a paso la ejecución de LAB07, interpretar métricas de Fashion-MNIST, analizar errores visuales y documentar el modelo.

Todas las métricas, tiempos, archivos generados y resultados incluidos en este proyecto fueron verificados mediante la ejecución local del código y las evidencias producidas por el repositorio.

La responsabilidad final sobre el código, las conclusiones y la documentación corresponde al estudiante.