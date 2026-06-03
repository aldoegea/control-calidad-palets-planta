# Control de calidad de palets en la línea de producción de una planta industrial

Notebook donde se explora el uso de técnicas de Computer Vision (OpenCV) para el control de calidad de los palets en la línea de producción de una planta industrial. Vamos a trabajar con `imágenes de profundidad` de palets en una línea de producción, con las que haremos un trabajo de inspección visual para validar que los palets cumplen con los requisitos establecidos.

## Estructura de los palets
Los palets tienen la siguiente composición: 

![alt text](https://github.com/aldoegea/control-calidad-palets-planta/blob/main/imgs/estructura_palets.png?raw=true)


## Imágenes
Las imágenes adjuntas se encuentran en la carpeta `camera_top`. Estamos utilizando imágenes de rango: el valor del píxel representa la profundidad para esta posición concreta, no el color. Son archivos tiff de 16 bits, donde 0 representa la profundidad más lejana desde la cámara.

## Guía

Las cuestiones a resolver son las siguientes: 
1. Generar una imagen normalizada de la imagen TIFF. Esto producirá una imagen con mayor contraste que la original, que podremos identificar a primera vista.  
2. Generar dos imágenes binarias a partir de la imagen normalizada, quedándonos en una con los tableros verticales y en la otra con los horizontales.
3. Hallar los contornos de los tableros en ambas imágenes.
4. Contar el número de tableros.
5. Control de calidad de los tableros.


## Jupyter Notebook
🔗 [Archivo *.ipynb original](https://github.com/aldoegea/control-calidad-palets-planta/blob/main/QC_PlantaProduccion.ipynb)


## Resultado
Estoy muy contento con el resultado porque he cumplido todos los objetivos satisfactoriamente. El sistema es capaz de detectar y contar los diferentes tableros de cada palet, así como chequear su integridad. De hecho, es esta última parte la más interesante conceptualmente:

1. Para cada tablero vertical se comprueba:

`fill_ratio`: porcentaje de píxeles blancos dentro de la caja. Sirve para detectar tableros incompletos, con partes rotas o con una inclinación/desviación irregular.

`continuidad_filas`: porcentaje de filas con suficiente presencia de píxeles blancos. Indica si el tablero mantiene una forma vertical continua.

`continuidad_columnas`: porcentaje de columnas con suficiente presencia de píxeles blancos. Ayuda a detectar estrechamientos, muescas o roturas laterales.

2. Para los tableros horizontales se usa el mismo planteamiento pero adaptado a su forma y teniendo en cuenta que están parcialmente tapados por los verticales:

`fill_ratio`: medida orientativa de ocupación de píxeles blancos dentro de la caja. No es decisivo porque no se ven los tableros completos (quedan ocluidos por los verticales).

`continuidad_filas`: comprueba si existe verdaderamente un tablero horizontal. Si solo hay unos pocos trozos o la pieza está muy rota, esa banda no se verá tan clara. No es del todo decisivo debido a la oclusión de las piezas horizontales.

`cobertura_visible`: analiza los tramos visibles entre los tableros verticales para confirmar que el tablero horizontal está presente donde debería verse.

Con estas métricas, el código detecta si falta algún tablero o si alguno está defectuoso, y finalmente marca el palet como correcto o defectuoso.