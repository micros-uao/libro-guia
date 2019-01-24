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

### Señales continuas y discretas en el dominio del tiempo

Se clasifican de acuerdo a la variable independiente y los valores que esta tome como: señales continuas en el tiempo o señales analógicas, señales discretas en el tiempo , señales deterministas y señales aleatorias.

* Señales analógicas: Definidas en cada instante de tiempo y el intervalo de valores \[a,b\] es continuo, donde a puede ser -∞ y b puede ser ∞.  Se puede representar matemáticamente, un ejemplo es: $$x(t)=Sin(\pi t + \phi)$$ 
* Señales discretas: Solo están definidas en determinados instantes  de tiempo. Una señal discreta se puede representar matemáticamente mediante una secuencia de números reales o complejos, un ejemplo: $$x(n)=0.8^n$$ 

![Representaci&#xF3;n gr&#xE1;fica de la se&#xF1;al discreta propuesta](../.gitbook/assets/image%20%2882%29.png)

