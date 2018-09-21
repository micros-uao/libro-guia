# 7. Retrasos en sistemas de control

En los sistemas de control se han analizado diferentes algoritmos de control usando protocolos de red con retrasos constantes y variables. Sin embargo no existe una técnica para cualquier sistema de control debido que depende de la configuración de la red, el protocolo de comunicaciones, las aproximaciones que se hagan del sistema y el algoritmo de control.

En la mayoría de trabajos realizados sobre NCS\(Networked control system\) se analiza el desempeño del sistema considerando únicamente la estabilidad del lazo cerrado, este es un requisito indispensable para el sistema pero en muchos casos prácticos  los criterios de desempeño deseados en los sistemas de control se especifican en términos de la respuesta transitoria del sistema frente a una entrada especifica. Por lo que se propone analizar el efecto que genera el retraso sobre la respuesta transitoria del sistema.

La estructura del NCS que se va a presentar en este trabajo utiliza un ZOH \(retenedor de orden cero\) en la entrada de la planta. Los retrasos son generados por el envió de la información a través de la red entre medidor-controlador y controlador-actuador.

El NCS considerado presenta las siguientes suposiciones:

* Sistemas de control SISO\(Single Input, Single Output\)
* El sistema de control se encuentra sincronizado. En este caso la tarea que realiza la medición se activa periódicamente, y las tareas que realizan el calculo de la acción de control y actúan sobre el sistema se activan por eventos
* El retraso presente entre los instantes en que se inicia la medición y se finaliza la actuación es menor o igual a Ts
* Las tramas son transmitidas y recibidas libres de error

Entonces el sistema de control en lazo cerrado se representa de la siguiente forma:

![Diagrama de bloque del sistema a trabajar](../.gitbook/assets/image%20%2815%29.png)

Debido a que el sistema esta sincronizado se puede considerar los retrasos en el sistema como un solo retraso:

![Diagrama de bloque simplificado del sistema a trabajar](../.gitbook/assets/image%20%2829%29.png)

El retraso se puede modelar como $$ e^{-TrS}$$, con $$ T_r=(1-m)T_s$$. Donde $$ T_r$$ representa la suma de los retrasos entre medidor\_controlador y controlador-actuador.

Empleando la transformada Z modificada es posible encontrar la función de transferencia en lazo cerrado del sistema entre 2 periodos de muestreo consecutivos, de lo cual se obtiene:

$$
H_{(Z,m)} = \frac {Gc_{(Z)}Gp_{(Z,m)}}{1+Gc_{(Z)}Gp_{(Z,m)}}
$$





