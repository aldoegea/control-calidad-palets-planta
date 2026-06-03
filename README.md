# Control de calidad de palets en la línea de producción de una planta industrial

Notebook donde se explora el uso de técnicas de Computer Vision (OpenCV) para el control de calidad de los palets en la línea de producción de una planta industrial. Vamos a trabajar con `imágenes de profundidad` de palets en una línea de producción, con las que haremos un trabajo de inspección visual para validar que los palets cumplen con los requisitos establecidos.

## Estructura de los palets
Los palets tienen la siguiente composición: 

![alt text](https://github.com/aldoegea/control-calidad-palets-planta/blob/main/imgs/estructura_palets.png?raw=true)


## Imágenes
Las imágenes adjuntas se encuentran en la carpeta `camera_top`. Estamos utilizando imágenes de rango: el valor del píxel representa la profundidad para esta posición concreta, no el color. Son archivos tiff de 16 bits, donde 0 representa la profundidad más lejana desde la cámara.

## Proyecto

Las cuestiones a resolver son las siguientes: 
1. Generar una imagen normalizada de la imagen TIFF. Esto producirá una imagen con mayor contraste que la original, que podremos identificar a primera vista.  
2. Generar dos imágenes binarias a partir de la imagen normalizada, quedándonos en una con los tableros verticales y en la otra con los horizontales.
3. Hallar los contornos de los tableros en ambas imágenes.
4. Contar el número de tableros.
5. Control de calidad de los tableros.
