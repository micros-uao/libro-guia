# 3.2.1 Guía

## Monitor de signos vitales 

Un monitor de signos vitales es un dispositivo que permite medir , procesar y presentar de forma continua los parámetros fisiológicos del paciente. Ademas posee un sistema que alerta cuando el paciente presente condiciones por encima o por debajo de los limites permitidos.

Dependiendo de la configuración de los monitores, estos pueden presentar información de varios parámetros fisiológicos tales como electrocardiograma\(ECG\), frecuencia respiratoria, presión no invasiva \(PNI\) , presión invasiva \(PN\), temperatura corporal , saturación de oxigeno\(SpO2\) , electromiografia \(EMG\), entre otros.

Los médicos utilizan estos instrumentos para evaluar en todo momento y de forma completa las condiciones fisiológicas del paciente ademas de que les permite hacer mejores valoraciones y tomar decisiones para tratamiento y diagnostico.

Los monitores de signos vitales pueden ser: 

* Pre-configurados 
* Modulares 
* Mixtos

#### Pre-configurados

Los parámetros a monitorear son fijados por el proveedor desde la fabrica y no se le puede agregar un parámetro adicional.

#### Modulares 

Estos monitores proveen módulos independientes para cada uno de los parámetros \(uniparámetros\) o para un grupo de parámetros\(multipárametros\)

### Tipos de monitores:

* Fijos: Se encuentran colocados a la cabecera del paciente y son sujetos a la pared a través de un soporte
  *  Anestesia: Equipos diseñados especialmente para monitorear los sistemas que pueden sufrir daño por falta de oxigeno o circulación tales como corazón, cerebro y riñones.
  * Adulto/Pediátrico: Por lo general se usa en áreas criticas y su aplicación especifica la determina los consumibles que utilice como electrodos, brazaletes, sensores, etc...
  * Neonatal: Cuenta con sistemas mas especializados para llevar el control de la temperatura, respiración , balance de fluidos, electrolitos y un algoritmo especializado en neonatos para la detección de arritmias especificas debido a los delgados complejos QRS y las altas frecuencias cardíacas.

![Monitor de signos vitales fijo](../../.gitbook/assets/image%20%2811%29.png)

* Transporte:
  * Intrahospitalario: Utilizados para monitorear un paciente en su traslado de un area a otra dentro de la misma institución de salud, se sugiere que monitoricen ECG, SpO2, PNI y un registrador integrado. Debe tener una batería integrada con duración de al menos 2.5 horas
  * Interhospitalario: Utilizados en el transporte del paciente de una institución de salud a otra, tienen que tener los mismos parámetros sugeridos para el monitor intrahospitalario pero ademas se sugiere que tenga conexión de 12V para conectarse a la ambulancia. 

![Monitor de signos vitales portable](../../.gitbook/assets/image%20%2812%29.png)

Para el caso de estudio 2 se utilizó el kit e-Health Sensor Platform V2.0 el cual permite realizar aplicaciones donde se necesita monitorizar el cuerpo. Posee  10 sensores diferentes: pulso, oxígeno en la sangre \(SPO2\), flujo de aire \(respiración\), temperatura corporal, electrocardiograma \(ECG\), glucómetro, respuesta galvánica de la piel \(GSR - sudoración\), presión arterial \(esfigmomanómetro\), posición del paciente \(acelerómetro\) y sensor de musculación / eletromiografía \(EMG\).

![e-Health Sensor Platform V2.0 for Arduino and Raspberry Pi](../../.gitbook/assets/image%20%2814%29.png)

![Esquema de conexiones a la plataforma](../../.gitbook/assets/image%20%2865%29.png)

La practica solo se va a enfocar en las señales de SpO2 y pulsioximetro,  ECG, temperatura, Galvánica y EMG . 

### El modulo de pulso y oxigeno en la sangre

Con este sensor se puede medir la saturación de oxigeno arterial de una forma no invasiva. Se basa en la detección de hemoglobina y desoxihemoglobina, lo hace utilizando 2 longitudes de onda diferentes y midiendo la diferencia real entre los espectros de absorción de HbO2 y Hb. El torrente sanguíneo se ve afectado por la concentración de HbO2 y Hb, y sus coeficientes de absorción se miden utilizando dos longitudes de onda de 660 nm \(espectros de luz roja\) y 940 nm \(espectros de luz infrarroja\). La hemoglobina desoxigenada y oxigenada absorbe diferentes longitudes de onda.

Los rangos normales aceptables para los pacientes son del 95 al 99 por ciento, aquellos con un problema de impulsión hipóxica esperan que los valores estén entre el 88 y el 94 por ciento, los valores del 100 por ciento pueden indicar una intoxicación por monóxido de carbono.

![Modo de uso del sensor de pulso y oxigeno](../../.gitbook/assets/image%20%2894%29.png)

### Electrocardiograma

Es una herramienta de diagnóstico que se utiliza para evaluar las funciones eléctricas y musculares del corazón. 

El sensor de electrocardiograma \(ECG\) se ha convertido en uno de los exámenes médicos más utilizados en la medicina moderna. Su utilidad en el diagnóstico de una gran variedad de patologías cardíacas que van desde la isquemia miocárdica y el infarto hasta el síncope y las palpitaciones ha sido invaluable para los médicos durante décadas.

Es posible que no siempre aparezca un problema cardíaco en el ECG. Algunas afecciones cardíacas nunca producen cambios específicos en el ECG. 

Con el ECG se puede medir la orientación del corazón en la cavidad torácica, evidencia de aumento en el grosor del músculo cardíaco , evidencia de daño a las diversas partes del músculo cardíaco , evidencia de flujo sanguíneo agudamente afectado al músculo cardíaco y patrones de actividad eléctrica anormal.

En la siguiente imagen se puede observar la forma de una señal ECG normal y como se divide en diferentes tramos donde cada uno indica un movimiento particular del corazón.  

![Representaci&#xF3;n de una se&#xF1;al ECG normal](../../.gitbook/assets/image%20%2873%29.png)

Tomado de: An Approach for Classifying ECG Arrhythmia Based on Features Extracted from EMD and Wavelet Packet Domains

Se conecta a la plataforma de la siguiente forma que indica la imagen, lo mismo para la conexión de los electrodos al cuerpo.

![Esquema de conexiones para el ECG](../../.gitbook/assets/image%20%28100%29.png)

### Temperatura corporal

La temperatura corporal depende del lugar del cuerpo en el que se realiza la medición y de la hora del día y el nivel de actividad de la persona. Diferentes partes del cuerpo tienen diferentes temperaturas.

La temperatura promedio del cuerpo comúnmente aceptada \(tomada internamente\) es de 37.0 ° C \(98.6 ° F\). En adultos sanos, la temperatura corporal fluctúa alrededor de 0.5 ° C \(0.9 ° F\) a lo largo del día, con temperaturas más bajas en la mañana y temperaturas más altas al final de la tarde y la noche, a medida que cambian las necesidades y actividades del cuerpo.

Es de gran importancia médica medir la temperatura corporal. La razón es que varias enfermedades están acompañadas por cambios característicos en la temperatura corporal. Del mismo modo, el curso de ciertas enfermedades se puede monitorear midiendo la temperatura corporal, y la eficacia de un tratamiento iniciado puede ser evaluada por el médico.

Para conectar el sensor de temperatura se conecta el jack a la tarjeta en la entrada de temperatura y se amarra al dedo indice como se indica en la siguiente imagen.

![Conexi&#xF3;n del sensor de temperatura](../../.gitbook/assets/image%20%2854%29.png)

### Galvánico o conductancia de la piel

La conductancia de la piel, también conocida como respuesta galvánica de la piel \(GSR\) es un método para medir la conductancia eléctrica de la piel, que varía con su nivel de humedad. Esto es de interés porque las glándulas sudoríparas están controladas por el sistema nervioso simpático, por lo que los momentos de emoción fuerte cambian la resistencia eléctrica de la piel. La conductancia de la piel se usa como una indicación de activación psicológica o fisiológica. El sensor de respuesta galvánica de la piel \(GSR, sudoración\) mide la conductancia eléctrica entre 2 puntos y es esencialmente un tipo de óhmetro.

En el método de respuesta de conductancia de la piel, la conductividad de la piel se mide en los dedos de la palma. El principio o teoría detrás del funcionamiento del sensor de respuesta galvánica es medir la resistencia eléctrica de la piel basada en el sudor producido por el cuerpo. Cuando se produce un alto nivel de sudoración, la resistencia eléctrica de la piel disminuye. Una piel más seca registra una resistencia mucho mayor. El sensor de respuesta de conductancia de la piel mide el reflejo psico-galvánico del cuerpo. Las emociones como la excitación, el estrés, el shock, etc. pueden provocar la fluctuación de la conductividad de la piel. La medición de la conductancia de la piel es un componente de los dispositivos poligráficos y se utiliza en la investigación científica de la excitación emocional o fisiológica.

El modo de uso es el siguiente:

![Conexi&#xF3;n sensor galv&#xE1;nico](../../.gitbook/assets/image%20%2892%29.png)

### Electromiografia\(EMG\) 

Un electromiograma \(EMG\) mide la actividad eléctrica de los músculos en reposo y durante la contracción.La electromiografía \(EMG\) es una técnica para evaluar y registrar la actividad eléctrica producida por los músculos esqueléticos.

Un electromiógrafo detecta el potencial eléctrico generado por las células musculares cuando estas células se activan eléctrica o neurológicamente. Las señales pueden analizarse para detectar anomalías médicas, nivel de activación, orden de reclutamiento o para analizar la biomecánica del movimiento humano o animal.

La EMG se utiliza como herramienta de diagnóstico para identificar enfermedades neuromusculares, evaluar el dolor lumbar, la kinesiología y los trastornos del control motor. Las señales de EMG también se usan como una señal de control para dispositivos protésicos como prótesis de manos, brazos y extremidades inferiores.

Este sensor medirá la actividad eléctrica filtrada y rectificada de un músculo, dependiendo de la cantidad de actividad en el músculo seleccionado.

En la siguiente imagen se puede observar la forma de conexión a la plataforma y al brazo para sensar la actividad del bíceps. Se utilizan electrodos para realizar la conexión directamente al brazo.

![Conexi&#xF3;n para medir la se&#xF1;al EMG del b&#xED;ceps](../../.gitbook/assets/image%20%2843%29.png)

