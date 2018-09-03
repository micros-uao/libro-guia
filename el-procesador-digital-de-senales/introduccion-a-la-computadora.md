# 3.2 Introducción a la computadora

Con el desarrollo de la electrónica surgieron circuitos que implementaban funciones específicas, como por ejemplo: sumadores, contadores, etc.; pero en muchas aplicaciones se necesitaba combinar varias de ellas y controlar de manera dinámica la ejecución de cada una dependiendo de las características de la aplicación.

### ¿Cómo resolver esta situación práctica sin necesidad de complejos diseños con sistemas lógicos de baja y mediana escala de integración \(LSI, MSI\)?.

Las soluciones propuestas a este interrogante llevaron al concepto de microprocesador; el cual podemos definir como un circuito digital cuya funcionalidad se determina en dispositivos externos a él, por lo que el mismo circuito puede servir para desarrollar diversas aplicaciones.

La integración del microprocesador con el resto de elementos necesarios para desarrollar una aplicación se denomina computadora, y de manera general está compuesta de los siguientes elementos:

![Diagrama b&#xE1;sico de una computadora](../.gitbook/assets/image%20%281%29.png)

*  Microprocesador. Administra toda la actividad dentro de la computadora. Se encarga de ejecutar las instrucciones almacenadas en la memoria de programa, procesar la información y establecer la comunicación entre el resto de los dispositivos de la computadora.
* Circuito Generador de la señal de reloj. Se encarga de suministrar la señal que impulsa las máquinas de estado que componen la unidad de control del microprocesador y de los demás componentes de la computadora.
* Circuito generador de Reset. Genera la señal que lleva al microprocesador, y a los demás componentes de la computadora, a un estado inicial conocido.
*  Memorias. Se definen como circuitos integrados que permiten el almacenamiento de información. A un microprocesador se pueden conectar diferentes tipos de memorias, las cuales se diferencian por la forma de almacenar la información, la capacidad, el modo de acceso y la rapidez de acceso.

Un microprocesador necesita de dispositivos especializados para el almacenamiento de los programas a ejecutar y los datos a procesar, es decir, los datos e instrucciones necesitan ser almacenadas para su interpretación y ejecución. De nada sirve poseer el procesador sino se le establecen las acciones que debe realizar cada elemento de la computadora de forma ordenada y sincronizada \(programa\). Además, las acciones a desarrollar deben evaluar los datos adquiridos o previamente conocidos, generando resultados parciales y finales que deben ser almacenados, por ello es indispensable el empleo de dispositivos almacenadores de la información en formato digital \(memoria de datos\).

*  La memoria de Instrucciones o de Programa. Es la encargada de almacenar la secuencia de bytes que definen la función que desarrollará el microprocesador \(Programa o instrucciones\). Generalmente es del tipo ROM, PROM, EPROM, EEPROM, o FLASH, de tal forma que al desconectar la fuente de energía el programa no desaparezca.

Los programas se almacenan como una secuencia de códigos binarios que representan cada una de las instrucciones que se desean realizar; así como también los elementos que intervienen en ellas para ingresar información a procesar o presentar los resultados del procesamiento.

* Memoria de datos. Almacena datos temporales los cuales son modificados por el microprocesador al ejecutar algún tipo de algoritmo. Generalmente son del tipo DRAM o SRAM, en cuyo caso esta información desaparece cuando se suspende la energía a la computadora.
* Buses de interconexión. Son agrupaciones de conductores que cumplen con una función específica:
* Bus de datos. Es bidireccional y transporta la información \(instrucciones y datos\) entre los componentes de la computadora. Como todos los componentes se comunican a través del mismo bus de datos es importante que todos manejen salidas de tres estados.
*  Bus de direcciones. Es un bus unidireccional a través del cual el microprocesador selecciona el dispositivo con el cual realizará una transferencia de información, para lo cual hace uso de las direcciones.

Es muy importante que solamente se seleccione un dispositivo a la vez de tal forma que no existan colisiones en el bus de datos, por lo tanto debe existir una única dirección para cada uno de los dispositivos. La función de selección de los dispositivos la realiza el bus de direcciones en conjunto con el bus de control.

* Bus de control. Es un bus unidireccional, aunque algunas señales son entrada al microprocesador mientras que otras salen del mismo. Suministra las señales de control hacia y desde los dispositivos que interactúan con el microprocesador, además indica el sentido en que fluye la información a través del bus de datos.
* Puertos de entrada y salida. Facilitan la comunicación entre el microprocesador y los periféricos, liberando al microprocesador de las tareas de sincronización con los periféricos.

Los puertos le indican al microprocesador cuando los periféricos han recibido la información que les ha enviado a través de un puerto de salida, o por el contrario, cuando los periféricos han suministrado información nueva, la cual debe ser capturada por el microprocesador haciendo uso de un puerto de entrada.

En el diagrama de la Figura 1 se considera que los puertos de interconexión hacen parte de la memoria de datos, a esta configuración se le denomina puertos mapeados en memoria.

* Periférico. Es cualquier dispositivo que le permite al microprocesador mantener, o establecer, una comunicación directa con el contexto de la aplicación. Por ejemplo: interruptores, teclados, lámparas de 7 segmentos y otros visualizadores alfanuméricos, etc. Por cuanto la razón de ser de las computadoras es procesar información, no tienen sentido considerar una computadora sin periféricos de entrada, que permitan el ingreso de información a procesar, o periféricos de salida, a través de los cuales se suministran los resultados del procesamiento. 





