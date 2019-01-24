# 1. Introducción

Una señal se puede definir como una secuencia de valores asociados a una magnitud, durante el procesamiento digital de señales se toman muestras de estos valores para generar un análisis de los mismos o para modificarlos, utilizando para ello un procesador implementado con sistemas digitales.

Algunos ejemplos de señales y aplicaciones de su procesamiento son los siguientes:

![The Scientish and Engineer&#x2019;s Guide to Digital Signal Processing. SW Smith.](.gitbook/assets/image%20%2859%29.png)

Ventajas del procesamiento digital de señales respecto al procesamiento analógico de señales:

* La flexibilidad al momento de cambiar parámetros o mejorar el proceso, solo cambiando el programa. Cambiar algún parámetro en un sistema analógico normalmente implica cambios en el hardware del mismo.
* Las tolerancias de los componentes electrónicos hacen que sea difícil controlar la precisión del sistema, a diferencia de un sistema digital que permite mejor control en los requisitos de precisión mediante la especificación de la longitud de la palabra, el tipo de aritmética coma fija o coma flotante y otros factores.
*  Las señales digitales se almacenan fácilmente en diferentes dispositivos \(discos, memorias usb...\) sin deterioro o perdida de la fidelidad de la señal. Por lo que se puede transportar fácilmente la información y ser procesada en tiempo no real.
* El procesamiento digital de señales permite la implementación de algoritmos mas complejos.
* Realizar operaciones matemáticas sobre señales analógicas resulta mas complejo de realizar que si se hicieran en un sistema digital, ademas de que este ultimo permite efectuar las operaciones necesarias de modo rutinario haciendo uso de un software.
* En algunos casos es mas económico implementar el procesamiento de una señal usando un sistema digital, esto ademas del costo de los componentes se debe a la flexibilidad al momento de realizar modificaciones.

El comportamiento de una señal dada puede catalogarse como transitorio o de estado estacionario. Una señal en estado estacionario exhibe periodicidad y por tanto puede ser considerada como el resultado de la suma de funciones periódicas. En el siguiente gráfico se puede observar una señal la cual se reconstruye con sus primeros armónicos, con esto se puede aclarar el concepto de que una señal periódica se puede representar por la suma infinita de sus componentes armónicas y que entre mayor numero de armónicos se use para reconstruir la señal mayor va a ser la aproximación a la señal original.

![Se&#xF1;al descompuesta en sus primeros 3 arm&#xF3;nicos ](.gitbook/assets/image%20%2893%29.png)

Cuando una señal se propaga a través de un sistema genera un efecto en sus salidas, transformación que depende de las características del sistema, las cuales, en el caso de sistemas lineales, están determinadas por su respuesta en amplitud y su respuesta en fase, las cuales indican la transformación que sufre un armónico al propagarse a través del sistema.

{% embed url="https://repl.it/@micros\_uao/SelfishDarksalmonThing" %}



