# 7. Fase linear y no linear en filtros

Al momento de seleccionar un filtro es muy importante tener en cuenta la aplicación en la cual se va a utilizar. Si se va a utilizar un filtro FIR o un filtro IIR se debe tener en cuenta que  ambos tienen diferentes ventajas de acuerdo a la aplicación y las restricciones , pero una caracteristica que muchas veces pasa desapercibida al momento de seleccionar un filtro es el tipo de cambio que este realiza sobre la fase en la señal de salida. 

Para observar la importancia de la fase al momento de seleccionar un filtro se va a seleccionar un caso teórico y uno aplicado. La gráfica siguiente representa una señal compuesta por 3 señales senos de frecuencia 60 Hz, 120 Hz y 240 Hz y la transformada rápida de Fourier de la señal resultante de mezclar estas señales.

![Se&#xF1;al compuesta por diferentes frecuencias y su espectro ](../.gitbook/assets/image%20%285%29.png)

Haciendo uso de la herramienta sptool de matlab se desarrollan 2 filtros, uno tipo FIR y el otro IIR .En la gráfica FIR filter se puede la señal resultante después de haber pasado por un filtro FIR con ventana hamming de orden 50 y en la grafica IIR filter la señal resultante después del filtro IIR elíptico de orden 7; la idea de esta prueba no fue realizar el filtrado de alguna de las componentes de la señal sino poder observar el comportamiento que produce tener un desfase linear y uno no linear sobre la forma de onda que reconstruye el filtro.

![Se&#xF1;ales resultantes de los filtros y su respuesta en fase](../.gitbook/assets/image%20%2824%29.png)

Podemos concluir que la señal en la gráfica FIR filter se aproxima a la señal result signal de la gráfica anterior esto se debe a que la respuesta en fase de este filtro es linear. Para el caso de la gráfica IIR filter si se puede notar que la forma de la onda se ve afectada, en las partes marcada y se alcanza a detallar que algunos picos presentes en la señal cambiaron su amplitud con respecto a la señal original, esto se debe a que la respuesta en fase es no linear y en este caso para componentes cercanas a 300 Hz el desfase es lo suficientemente grande como para afectar la forma de onda al momento de que el filtro realice el procesamiento de la señal. El proceso de reconstrucción que hace el filtro toma cada componente de la señal original y la desfasa un valor de acuerdo a la respuesta en fase del filtro, en las siguientes gráficas se pueden observar los valores de desfase para cada componente según el filtro utilizado.

![Respuesta en fase del filtro FIR](../.gitbook/assets/image%20%2842%29.png)

![Respuesta en fase del filtro FIR](../.gitbook/assets/image%20%2849%29.png)

De manera que las ecuaciones resultantes serian las siguientes, donde yfir es la salida para el filtro FIR con ventana haming y la salida yiir sería la salida para el filtro IIR elíptico; a ambas señales se les suma un valor de 500 al final con la finalidad de que la señal esté compuesta por valores positivos y al momento de llevarlo a implementación sea más fácil poder reconstruirla con ayuda de un DAC\(digital-analog converter\). Se debe tener en cuenta que estas ecuaciones aplican para este caso particular donde las componentes en frecuencias no se ven afectadas por la reducción en magnitud que realiza el filtro de manera que es una aproximación bastante cercana a la salida del filtro.

$$
yfir=250(sin⁡(2π60t-9.44)+sin⁡(2π120t-18.8)+sin⁡(2π240t-37.78) )+500 \\ \space \\ yiir=250(sin⁡(2π60t-0.77)+sin⁡(2π120t-1.74)+sin⁡(2π240t-3.97) )+500
$$

Podemos observar paso por paso como la suma de las 3 señales forman la señal resultante para ambos filtros. En la siguiente grafica se pueden ver las 3 componentes con sus respectivos desfases generados por el filtro FIR con ventana hamming de orden 50, en la columna derecha se observa en cada gráfico como se suma cada componente hasta obtener la señal resultante al final en el grafico result signal after filter .

![Reconstrucci&#xF3;n del filtro FIR](../.gitbook/assets/image%20%2819%29.png)

De la misma forma se realiza la misma operación paso a paso para el filtro IIR elitpico de orden 7 y se puede notar en la figura \# como la señal resultante cambia su forma al sumar la componente de 240 Hz debido a que el desfase para esta componente se realiza cerca de la región de la respuesta en fase donde la no linearidad es más notable.

![Reconstrucci&#xF3;n del filtro IIR](../.gitbook/assets/image%20%282%29.png)

Un caso práctico al momento de trabajar filtros digitales son las señales biológicas. Debido a los muchas razones físicas, al adquirir una señal biológica esta presenta normalmente ruido el cual debe ser filtrado para poder extraer la información deseada. Un caso muy común es el ruido producido por la red eléctrica el cual se encuentra normalmente en todos los dispositivos electrónicos que se alimenten de la red e incluso algunos dispositivos inalambricos los cuales también se ven afectados. Entonces al momento de adquirir una señal biológica como un ECG\(electrocardiograma\) se implementa un filtro que elimine la componente de 60 Hz de la red \(60 Hz en América y 50 Hz en Europa\). De manera que se va a realizar un filtro FIR y un filtro IIR haciendo uso de la herramienta sptool que tiene matlab y con los resultados obtenidos se van a observar algunas de las diferencias que presenta cada uno. 

En las siguientes figuras se puede observar la respuesta en magnitud\(dB\) y en fase respectivamente del filtro pasa-baja tipo FIR con ventana Hamming de orden 60 a una frecuencia de muestreo de 500 Hz y una frecuencia de corte de 45 Hz.

![Respuesta en magnitud del filtro FIR](../.gitbook/assets/image%20%2846%29.png)

![Respuesta en fase del filtro FIR](../.gitbook/assets/image%20%2836%29.png)

En las siguientes figuras se puede observar la respuesta en magnitud\(dB\) y en fase respectivamente del filtro pasa-baja tipo IIR elíptico de orden 7 a una frecuencia de muestreo de 500 Hz y una frecuencia de corte de 45 Hz. Se elige la frecuencia de corte a 45 Hz para que la reducción de la magnitud de la componente a 60 Hz se reduzca completamente.

![Respuesta en magnitud del filtro IIR](../.gitbook/assets/image%20%2845%29.png)

![Respuesta en fase del filtro IIR](../.gitbook/assets/image%20%2857%29.png)

Con los filtros creados se procede a mirar la respuesta de cada uno ante la señal ECG con el ruido de la red. En el siguiente gráfico se puede comparar la señal ECG pura y con ruido vs la señal filtrada utilizando el filtro con ventana haming y el filtro elíptico.

![Gr&#xE1;ficos de la se&#xF1;al ECG original,con ruido y filtrada. ](../.gitbook/assets/image%20%2832%29.png)

Si se observa detalladamente la señal ECG filtrada usan el filtro eliptico la parte marcada en la imagen muestra un cambio en la forma de la onda lo cual puede ocasionar errores en la toma de decisiones de un médico al momento de diagnosticar. Este cambio ocurre debido a que el filtro IIR elíptico presenta un comportamiento en fase no linear de forma que las componentes de la señal después de ser filtrada se desfasan y la no linealidad del filtro genera deformaciones en la señal reconstruida.

![Se&#xF1;al ECG filtrada utilizando el filtro IIR](../.gitbook/assets/image%20%2852%29.png)

Lo siguiente es implementar los 2 filtros en un microcontrolador y observar la respuesta de cada uno ante una señal ECG con ruido de 60 Hz. Para esta práctica se generó la señal ECG con un Arduino Due para poder aprovechar el conversor DAC que este trae integrado , también se utilizó otro Arduino del mismo tipo para montar los filtros.

Después de implementar el código para el filtro FIR se utilizó un osciloscopio para comparar la señal de entrada y de salida para cada filtro. Enla siguiente imagen se representa la respuesta del filtro FIR, se obtuvo una señal ECG sin ruido bastante aproximada a la ECG pura que se simuló en Matlab.

![Resultado de implementar el filtro FIR](../.gitbook/assets/image%20%283%29.png)

Para el otro caso se implementó en el Arduino Due el filtro IIR elíptico, la respuesta del filtro es bastante aproximada a la simulada incluso presenta la deformación de la onda en la parte marcada.  


![Resultado de implementar el filtro IIR](../.gitbook/assets/image%20%2843%29.png)

En conclusión se puede decir que al momento de trabajar un señal biológica es muy importante tener en cuenta que información es de interés en este tipo de señal, porque si el profesional está interesado en analizar la forma de la onda, un filtro de fase no linear\(filtro IIR\) inevitablemente producirá deformaciones en la onda; aunque si se consigue que las componentes de la señal reconstruida estén en la parte aproximadamente lineal de la respuesta en fase se puede reconstruir la señal de una forma muy aproximada a la deseada; pero para evitar complicaciones resulta más sencillo implementar un filtro de fase linear\(filtro FIR\). En cambio en señales físicas como temperatura, presión, nivel donde se necesita extraer información como voltaje o frecuencia y no se necesita información de la forma de la onda, se puede utilizar un filtro de fase no linear el cual representa una carga computacional menor y cumple con su tarea de una manera más eficiente que un filtro FIR para este caso particular.

Los códigos para implementación en arduino y simulaciones de matlab se pueden encontrar en el siguiente link:

{% embed data="{\"url\":\"https://github.com/micros-uao/codigos/tree/master/Filtros\",\"type\":\"link\",\"title\":\"micros-uao/codigos\",\"description\":\"Contribute to micros-uao/codigos development by creating an account on GitHub.\",\"icon\":{\"type\":\"icon\",\"url\":\"https://github.com/fluidicon.png\",\"aspectRatio\":0},\"thumbnail\":{\"type\":\"thumbnail\",\"url\":\"https://avatars3.githubusercontent.com/u/40005563?s=400&v=4\",\"width\":420,\"height\":420,\"aspectRatio\":1}}" %}

