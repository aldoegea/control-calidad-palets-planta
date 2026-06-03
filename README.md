# Control de calidad de palets con Computer Vision

Notebook para la inspección automática de palets industriales usando técnicas de Computer Vision (OpenCV) sobre imágener de profundidad para asegurar el control de calidad en la línea de producción.

[![Python](https://img.shields.io/badge/Python-3.14-blue.svg)](https://www.python.org/)
[![OpenCV](https://img.shields.io/badge/OpenCV-Computer%20Vision-green.svg)](https://opencv.org/)
[![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange.svg)](https://jupyter.org/)

<br>

## Estructura de los palets

![Estructura del palet](https://github.com/aldoegea/control-calidad-palets-planta/blob/main/imgs/estructura_palets.png?raw=true)

<br>

## Objetivos

| Paso | Tarea | Comentarios |
|------|-------|-------------|
| 1 | Generar una imagen normalizada de la imagen TIFF | Producirá una imagen con mayor contraste que la original, que podremos identificar a primera vista |
| 2 | Generar imágenes binarias | Una imagen con los tableros verticales y otra con los horizontales |
| 3 | Detectar contornos |
| 4 | Contar tableros |
| 5 | Evaluar la calidad de los tableros | Definir sistema de control y valores threshold

<br>

## Imágenes de entrada

Las imágenes están en la carpeta `camera_top`. Son imágenes de rango de 16 bits: cada píxel representa profundidad, no color. Por lo tanto, a primera vista no muestran ninguna información.

<br>

## Control de calidad

Para cada uno de los tableros se definen una serie de métricas:

### Tableros verticales:

`fill_ratio`: porcentaje de píxeles blancos dentro de la caja. Sirve para detectar tableros incompletos, con partes rotas o con una inclinación/desviación irregular.

`continuidad_filas`: porcentaje de filas con suficiente presencia de píxeles blancos. Indica si el tablero mantiene una forma vertical continua.

`continuidad_columnas`: porcentaje de columnas con suficiente presencia de píxeles blancos. Ayuda a detectar estrechamientos, muescas o roturas laterales.



### Tableros horizontales:

`fill_ratio`: medida orientativa de ocupación de píxeles blancos dentro de la caja. No es decisivo porque no se ven los tableros completos (quedan ocluidos por los verticales).

`continuidad_filas`: comprueba si existe verdaderamente un tablero horizontal. Si solo hay unos pocos trozos o la pieza está muy rota, esa banda no se verá tan clara. No es del todo decisivo debido a la oclusión de las piezas horizontales.

`cobertura_visible`: analiza los tramos visibles entre los tableros verticales para confirmar que el tablero horizontal está presente donde debería verse.

<br>

## Notebook

🔗 [Abrir notebook completo](https://github.com/aldoegea/control-calidad-palets-planta/blob/main/QC_PlantaProduccion.ipynb)

<br>

## Resultado

El sistema detecta correctamente el número de tableros y su estado, clasificando el palet como <b style="color:green">🟢 CORRECTO</b> o <b style="color:red">🔴 DEFECTUOSO</b>.