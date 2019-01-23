# 2.2 Caracterización de las señales

De acuerdo a sus características una señal puede ser procesada o analizada, existen técnicas que solo aplican a familias especificas de señales, por lo que cualquier procesamiento de señales deberá empezar por la identificación de la clasificación de la señal : 

### Señales multicanal y multidimensionales.

En muchas aplicaciones se pueden encontrar múltiples sensores encargados de la adquisición de la información , estas señales se pueden representar como magnitudes escalares, magnitudes complejas o incluso como vectores.

$$
S=\begin{bmatrix}
    s_1(t)  \\
    s_2 (t) \\
    s_3(t)  \\
    \end{bmatrix}
$$

Un vector de señales como la forma anterior es una señal multicanal, un ejemplo de esto es un osciloscopio digital estándar del laboratorio de electrónica que tiene 2 canales de entrada.

 Otro caso es en el que se tenga una señal multidimensional como el caso de un televisor de color que puede escribirse en 3 funciones de intensidad de la forma $$I_r(x,y,t) , \  I_g(x,y,t) ,\ I_b(x,y,t) $$ . Las cuales corresponden al brillo de los 3 colores principales\(rojo,verde,azul\) como funciones del tiempo. Por lo que se puede decir que una imagen de televisión a color es una señal tridimensional de 3 canales. 

