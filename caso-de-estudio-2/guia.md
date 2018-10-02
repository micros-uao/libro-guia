# 5.1 Guía

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

![Monitor de signos vitales fijo](../.gitbook/assets/image%20%2811%29.png)

* Transporte:
  * Intrahospitalario: Utilizados para monitorear un paciente en su traslado de un area a otra dentro de la misma institución de salud, se sugiere que monitoricen ECG, SpO2, PNI y un registrador integrado. Debe tener una batería integrada con duración de al menos 2.5 horas
  * Interhospitalario: Utilizados en el transporte del paciente de una institución de salud a otra, tienen que tener los mismos parámetros sugeridos para el monitor intrahospitalario pero ademas se sugiere que tenga conexión de 12V para conectarse a la ambulancia. 

![Monitor de signos vitales portable](../.gitbook/assets/image%20%2812%29.png)

Para el caso de estudio 2 se utilizó el kit e-Health Sensor Platform V2.0 el cual permite realizar aplicaciones donde se necesita monitorizar el cuerpo. Posee  10 sensores diferentes: pulso, oxígeno en la sangre \(SPO2\), flujo de aire \(respiración\), temperatura corporal, electrocardiograma \(ECG\), glucómetro, respuesta galvánica de la piel \(GSR - sudoración\), presión arterial \(esfigmomanómetro\), posición del paciente \(acelerómetro\) y sensor de musculación / eletromiografía \(EMG\).

![e-Health Sensor Platform V2.0 for Arduino and Raspberry Pi](../.gitbook/assets/image%20%2814%29.png)

La practica solo se va a enfocar en las señales de temperatura, ECG , EMG , Galvánica, SpO2 y pulsioximetro.

### El modulo de pulso y oxigeno en la sangre

Con este sensor se puede medir la saturación de oxigeno arterial de una forma no invasiva. Se basa en la detección de hemoglobina y desoxihemoglobina, lo hace utilizando 2 longitudes de onda diferentes y midiendo la diferencia real entre los espectros de absorción de HbO2 y Hb. El torrente sanguíneo se ve afectado por la concentración de HbO2 y Hb, y sus coeficientes de absorción se miden utilizando dos longitudes de onda de 660 nm \(espectros de luz roja\) y 940 nm \(espectros de luz infrarroja\). La hemoglobina desoxigenada y oxigenada absorbe diferentes longitudes de onda.

Los rangos normales aceptables para los pacientes son del 95 al 99 por ciento, aquellos con un problema de impulsión hipóxica esperan que los valores estén entre el 88 y el 94 por ciento, los valores del 100 por ciento pueden indicar una intoxicación por monóxido de carbono.

![Modo de uso del sensor de pulso y oxigeno](../.gitbook/assets/image%20%2873%29.png)

