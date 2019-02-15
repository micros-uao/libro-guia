# 1. Introducción

Una señal se puede definir como una secuencia de valores asociados a una magnitud, durante el procesamiento digital de señales se toman muestras de estos valores para generar un análisis de los mismos o para modificarlos, utilizando para ello un procesador implementado con sistemas digitales.

Algunos ejemplos de señales y aplicaciones de su procesamiento son los siguientes:

![The Scientish and Engineer&#x2019;s Guide to Digital Signal Processing. SW Smith.](.gitbook/assets/image%20%2863%29.png)

Ventajas del procesamiento digital de señales respecto al procesamiento analógico de señales:

* La flexibilidad al momento de cambiar parámetros o mejorar el proceso, solo cambiando el programa. Cambiar algún parámetro en un sistema analógico normalmente implica cambios en el hardware del mismo.
* Las tolerancias de los componentes electrónicos hacen que sea difícil controlar la precisión del sistema, a diferencia de un sistema digital que permite mejor control en los requisitos de precisión mediante la especificación de la longitud de la palabra, el tipo de aritmética coma fija o coma flotante y otros factores.
*  Las señales digitales se almacenan fácilmente en diferentes dispositivos \(discos, memorias usb...\) sin deterioro o perdida de la fidelidad de la señal. Por lo que se puede transportar fácilmente la información y ser procesada en tiempo no real.
* El procesamiento digital de señales permite la implementación de algoritmos mas complejos.
* Realizar operaciones matemáticas sobre señales analógicas resulta mas complejo de realizar que si se hicieran en un sistema digital, ademas de que este ultimo permite efectuar las operaciones necesarias de modo rutinario haciendo uso de un software.
* En algunos casos es mas económico implementar el procesamiento de una señal usando un sistema digital, esto ademas del costo de los componentes se debe a la flexibilidad al momento de realizar modificaciones.

El comportamiento de una señal dada puede catalogarse como transitorio o de estado estacionario. Una señal en estado estacionario exhibe periodicidad y por tanto puede ser considerada como el resultado de la suma de funciones periódicas. En el siguiente gráfico se puede observar una señal la cual se reconstruye con sus primeros armónicos, con esto se puede aclarar el concepto de que una señal periódica se puede representar por la suma infinita de sus componentes armónicas y que entre mayor numero de armónicos se use para reconstruir la señal mayor va a ser la aproximación a la señal original.

![Se&#xF1;al descompuesta en sus primeros 3 arm&#xF3;nicos ](.gitbook/assets/image%20%2899%29.png)

Cuando una señal se propaga a través de un sistema genera un efecto en sus salidas, transformación que depende de las características del sistema, las cuales, en el caso de sistemas lineales, están determinadas por su respuesta en amplitud y su respuesta en fase, las cuales indican la transformación que sufre un armónico al propagarse a través del sistema.

### Muestreo y construcción 

Para realizar operaciones de procesamiento digital sobre una señal análoga en el tiempo, primero se debe muestrear esta señal periódicamente cada T segundos, matemáticamente esto se describe como:

$$
x(n)=x_a(nT)
$$

![Se&#xF1;al muestreada peri&#xF3;dicamente cada T segundos](.gitbook/assets/image%20%2845%29.png)

### Teorema del muestreo

Comprende un proceso que sigue al de muestreo en la digitalización de una señal y que, al contrario del muestreo, no es reversible \(se produce una pérdida de información en el proceso de cuantificación, incluso en el caso ideal teórico, que se traduce en una [distorsión](https://es.wikipedia.org/wiki/Distorsi%C3%B3n) conocida como error o [ruido de cuantificación](https://es.wikipedia.org/wiki/Ruido_de_cuantificaci%C3%B3n) y que establece un límite teórico superior a la relación señal-ruido\).

![Muestreo de una se&#xF1;al mediante un tren de impulsos con Frecuencia Fs](.gitbook/assets/image%20%2826%29.png)

En procesamiento de señales, el aliasing es el efecto que causa que señales continuas distintas se tornen indistinguibles cuando se muestrean digitalmente. Cuando esto sucede, la señal original no puede ser reconstruida a partir de la señal digital. Una imagen limitada en banda y muestreada por debajo de su frecuencia de Nyquist en las direcciones "x" e "y", resulta en una superposición de las replicaciones periódicas del espectro G\(fx, fy\). Este fenómeno de superposición periódica sucesiva es lo que se conoce como aliasing o Efecto Nyquist.

![Se&#xF1;al reconstruida donde se evidencia el aliasing ](.gitbook/assets/image%20%2824%29.png)

El aliasing es un motivo de preocupación mayor en lo que concierne a la conversión analógica-digital de señales de audio y vídeo: el muestreo incorrecto de señales analógicas puede provocar que señales de alta frecuencia presenten dicho aliasing con respecto a señales de baja frecuencia. El aliasing es también una preocupación en el área de la computación gráfica e infografía, donde puede dar origen a patrones de moiré \(en las imágenes con muchos detalles finos\) y también a bordes dentados.

![Aliasing al muestrear una se&#xF1;al](.gitbook/assets/image%20%2844%29.png)

Un ejemplo de código donde se puede observar una aplicación de procesamiento digital de señales es el siguiente cogido donde se implementan unos filtros diseñados en Python.

{% embed url="https://repl.it/@micros\_uao/SelfishDarksalmonThing" caption="Ejemplo de filtro en python" %}





