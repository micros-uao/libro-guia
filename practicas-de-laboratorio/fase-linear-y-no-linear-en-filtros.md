# 7. Fase linear y no linear en filtros

Al momento de seleccionar un filtro es muy importante tener en cuenta la aplicación en la cual se va a utilizar. Si se va a utilizar un filtro FIR o un filtro IIR se debe tener en cuenta que  ambos tienen diferentes ventajas de acuerdo a la aplicación y las restricciones , pero una caracteristica que muchas veces pasa desapercibida al momento de seleccionar un filtro es el tipo de cambio que este realiza sobre la fase en la señal de salida. 

Para observar la importancia de la fase al momento de seleccionar un filtro se va a seleccionar un caso teórico y uno aplicado. La gráfica siguiente representa una señal compuesta por 3 señales senos de frecuencia 60 Hz, 120 Hz y 240 Hz y la transformada rápida de Fourier de la señal resultante de mezclar estas señales.

![Se&#xF1;al compuesta por diferentes frecuencias y su espectro ](../.gitbook/assets/image%20%283%29.png)

Haciendo uso de la herramienta sptool de matlab se desarrollan 2 filtros, uno tipo FIR y el otro IIR .En la gráfica FIR filter se puede la señal resultante después de haber pasado por un filtro FIR con ventana hamming de orden 50 y en la grafica IIR filter la señal resultante después del filtro IIR elíptico de orden 7; la idea de esta prueba no fue realizar el filtrado de alguna de las componentes de la señal sino poder observar el comportamiento que produce tener un desfase linear y uno no linear sobre la forma de onda que reconstruye el filtro.

![Se&#xF1;ales resultantes de los filtros y su respuesta en fase](../.gitbook/assets/image%20%2815%29.png)

Podemos concluir que la señal en la gráfica FIR filter se aproxima a la señal result signal de la gráfica anterior esto se debe a que la respuesta en fase de este filtro es linear. Para el caso de la gráfica IIR filter si se puede notar que la forma de la onda se ve afectada, en las partes marcada y se alcanza a detallar que algunos picos presentes en la señal cambiaron su amplitud con respecto a la señal original, esto se debe a que la respuesta en fase es no linear y en este caso para componentes cercanas a 300 Hz el desfase es lo suficientemente grande como para afectar la forma de onda al momento de que el filtro realice el procesamiento de la señal. El proceso de reconstrucción que hace el filtro toma cada componente de la señal original y la desfasa un valor de acuerdo a la respuesta en fase del filtro, en las siguientes gráficas se pueden observar los valores de desfase para cada componente según el filtro utilizado.

![Respuesta en fase del filtro FIR](../.gitbook/assets/image%20%2824%29.png)

![Respuesta en fase del filtro FIR](../.gitbook/assets/image%20%2826%29.png)

De manera que las ecuaciones resultantes serian las siguientes, donde yfir es la salida para el filtro FIR con ventana haming y la salida yiir sería la salida para el filtro IIR elíptico; a ambas señales se les suma un valor de 500 al final con la finalidad de que la señal esté compuesta por valores positivos y al momento de llevarlo a implementación sea más fácil poder reconstruirla con ayuda de un DAC\(digital-analog converter\). Se debe tener en cuenta que estas ecuaciones aplican para este caso particular donde las componentes en frecuencias no se ven afectadas por la reducción en magnitud que realiza el filtro de manera que es una aproximación bastante cercana a la salida del filtro.

$$
yfir=250(sin⁡(2π60t-9.44)+sin⁡(2π120t-18.8)+sin⁡(2π240t-37.78) )+500 \\ \space \\ yiir=250(sin⁡(2π60t-0.77)+sin⁡(2π120t-1.74)+sin⁡(2π240t-3.97) )+500
$$

Podemos observar paso por paso como la suma de las 3 señales forman la señal resultante para ambos filtros. En la siguiente grafica se pueden ver las 3 componentes con sus respectivos desfases generados por el filtro FIR con ventana hamming de orden 50, en la columna derecha se observa en cada gráfico como se suma cada componente hasta obtener la señal resultante al final en el grafico result signal after filter .

![Reconstrucci&#xF3;n del filtro FIR](../.gitbook/assets/image%20%2812%29.png)

De la misma forma se realiza la misma operación paso a paso para el filtro IIR elitpico de orden 7 y se puede notar en la figura \# como la señal resultante cambia su forma al sumar la componente de 240 Hz debido a que el desfase para esta componente se realiza cerca de la región de la respuesta en fase donde la no linearidad es más notable.

![Reconstrucci&#xF3;n del filtro IIR](../.gitbook/assets/image%20%281%29.png)

