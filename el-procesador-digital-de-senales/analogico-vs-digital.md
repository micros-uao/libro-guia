# 3.1 Analógico vs digital

## Conversión analógico-digital

Las señales a procesar en los casos de las aplicaciones propuestas son de origen analógico, por tal razón es necesario convertirlas en un formato digital.

![](../.gitbook/assets/image%20%2882%29.png)

## Teorema del muestro

Una de los aspectos más importantes en el tratamiento digital de señales análogas está relacionado con la velocidad a la cual se toman muestras de la señal análoga, esta se encuentra definida por el Teorema del muestreo, el cual establece que:

![](../.gitbook/assets/image%20%287%29.png)

En donde es la frecuencia de muestreo de la señal análoga, y es la frecuencia del armónico de más alta frecuencia que contiene la señal análoga a procesar.

## Cuantificación

La cuantificación es el proceso mediante el cual se representa de manera digital la magnitud muestreada de la señal análoga a procesar, esto se realiza mediante una cierta cantidad de bits.

Uno de los métodos utilizados para realizar la representación de la magnitud análoga en forma digital consiste en aproximarla al valor digital más próximo al valor a representar, esto se conoce con el nombre de redondeo. De allí que la cuantificación resulte en un proceso de pérdida de información, lo cual introduce un error en el sistema de procesamiento, el cual depende de la cantidad de bits utilizados para representar la magnitud análoga.

La relación señal / ruido de cuantificación \(SQNR, signal to quantization noise ratio\) proporciona la relación entre la potencia de la señal y la del ruido introducido por el proceso de cuantificación, esta se define como:

![](../.gitbook/assets/image%20%2881%29.png)

Donde representa la cantidad de bits que se utilizan para representar la señal análoga en forma digital. Se puede apreciar que cada vez que se duplica el número de niveles de cuantificación \(se agrega un bit a la representación de la señal\), la SQNR aumenta aproximadamente 6 dB. Por lo cual, si se utiliza un conversor de 16 bits la SQNR será aproximadamente de 96 dB.

Una representación de valores en 16 bits es adecuada para disminuir los efectos de cuantificación en la implementación de sistemas de procesamiento digital de señales análogas. Sin embargo, con relación a la etapa de adquisición de la señal, la tecnología actual utiliza niveles de voltaje bajos \(entre 1.8 a 3V\), lo cual presenta inconvenientes cuando la resolución del conversor A/D es muy alta por cuanto se generan errores de conversión debido a pequeños ruidos en la señal.  


## Representación de números

Al comparar las representación en punto fijo y punto flotante se obtienen las siguientes consideraciones:

*  La representación en punto flotante tiene la característica de permitir un rango dinámico mayor variando la resolución a lo largo del rango, esto se logra disminuyendo la resolución con un incremento en el tamaño de números consecutivos. Por lo tanto, para representaciones de magnitudes pequeñas la representación en punto flotante proporciona una resolución mucho más fina que la representación del mismo número en punto fijo. Pero la resolución en punto flotante se hace mas gruesa con relación a la representación en punto fijo cuando las magnitudes son grandes. 
* La representación en punto fijo proporciona una resolución uniforme en todo el rango de valores a representar.

## Implementación de sistemas discretos lineales e invariantes con el tiempo

La forma general de la relación de entrada-salida en un sistema Lineal e Invariante con el Tiempo \(LTI\) es la siguiente:

![](../.gitbook/assets/image%20%2875%29.png)

Siendo x,y la entrada y salida del sistema respectivamente, a y b  los coeficientes de la función de transferencia que relaciona la salida y la entrada del sistema.

Otra forma de representar los sistemas discretos lineales e invariantes con el tiempo es mediante su respuesta impulsional h\(n\), con lo cual tenemos:

![](../.gitbook/assets/image%20%281%29.png)

Dependiendo de los valores de los coeficientes a y b los sistemas se pueden clasificar en dos grupos:  


![](../.gitbook/assets/image%20%289%29.png)

Existen diversas estructuras para representar la estructura de sistemas FIR e IIR, entre ellas tenemos:

* Estructura en Forma Directa 
* Estructura en Forma de cascada 
* Estructura en Forma Paralela 
* Estructura de Muestreo en Frecuencia 
* Estructura en Celosía

La forma en cascada es más robusta ante la presencia de cuantificación de los coeficientes, y es recomendada especialmente cuando se emplea una representación en punto fijo.

La estructura en cascada se obtiene factorizando la respuesta impulsional H\(z\)

![Estructura de sistemas discretos en forma de cascada](../.gitbook/assets/image%20%2831%29.png)



