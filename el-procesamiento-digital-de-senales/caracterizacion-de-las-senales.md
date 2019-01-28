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

![Representaci&#xF3;n gr&#xE1;fica de la se&#xF1;al discreta propuesta](../.gitbook/assets/image%20%2886%29.png)

* Señales deterministas ,cualquier señal que se pueda escribir mediante una expresión matemática explicita, una tabla de datos o una regla definida.

![Se&#xF1;al seno](../.gitbook/assets/image%20%2887%29.png)

* Señales aleatorias, no se pueden describir con formulas matemáticas con una grado de precisión razonable o resulta demasiado complejo llegar a un modelo con tal precisión. Evolucionan en el tiempo de una manera no predecible.

![Se&#xF1;al de ruido](../.gitbook/assets/image%20%2877%29.png)

### Frecuencia en las señales continuas y discretas en el tiempo.

La frecuencia está directamente relacionado con el concepto de tiempo, en el caso de una oscilación armónica simple se puede escribir matemáticamente una señal sinusoidal continua de la siguiente forma:

$$
X(t)= Acos( Ωt+ \theta)
$$

Con esta señal básica se puede observar sus parámetros de amplitud, frecuencia y fase. Se convierte la frecuencia de radianes a Hertz con la siguiente sustitución : 

$$
Ω = 2πF
$$

De acuerdo al ejemplo anterior se puede decir que para valores de frecuencia fijo la señal es periódica ,  las señales sinusoidales con frecuencias diferentes son diferentes , incrementar la frecuencia da como resultado un mayor numero de oscilaciones en un periodo de tiempo dado.

Con la identidad de Euler se puede relacionar la señal sinusoidal anterior con exponenciales complejas de la siguiente forma.

$$
X(t)=Acos( Ωt+ \theta)= \\ \frac A 2 e^{j( Ωt+ \theta)}+\frac A 2 e^{-j( Ωt+ \theta)}
$$

En el caso de una señal sin**u**soidal discreta en el tiempo la variable independiente es n que representa el número de muestra. Una función sinusoidal discreta se escribe de la siguiente manera:

$$
X(t)= Acos( 2πFn+ \theta)
$$

Para sinusoidales discretas en el tiempo se puede decir que : Si su frecuencia es un número racional  la señal es periódica en el tiempo, las señales sinusoidales discretas en el tiempo con frecuencias separadas por múltiplos enteros de 2π son idénticas, la tasa de oscilación mas alta de una señal sinusoidal discreta se alcanza con $$ F=\frac 1 2 $$ o $$\ w=π.$$ 

![Oscilaciones de una se&#xF1;al sinusoidal b&#xE1;sica](../.gitbook/assets/image%20%2848%29.png)

> 1.  John G. Proakis Dimitris G. Manolakis. \(2007\). Tratamiento Digital de Señales. Madrid: Pearson Educación .



