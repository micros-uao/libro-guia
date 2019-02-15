# El efecto de la implementación de paso de parámetros por valor o por referencia

## Invocar una Función: Pasando Apuntador vs Pasando una Referencia

Como se ha mencionado anteriormente en esta guía. Cuando se desarrolla un programa en c/c++ es necesario disponer de un compilador el cual transforma el código en lenguaje de alto a nivel a instrucciones de máquina. Muchas veces una sola instrucción en c/c++ puede corresponder muchas instrucciones en lenguaje de máquina. Esto en parte contribuye a que el desarrollo de programas en lenguajes de alto nivel sea mas eficiente. Sin embargo, cuando se trabaja con potencias computacionales limitadas, como es el caso de algunos microcontroladores, puede ser muy conveniente tener un conocimiento de este fenómeno para poder optimizar el uso de recursos.

 A manera de ejemplo se puede considerar el caso en que se desea pasar un arreglo como argumento de una función. Existen 2 posibilidades, se puede pasar el arreglo directamente como parámetro o en su lugar se puede usar un apuntador. Cuando se invoca una función se hace una copia de los parámetros de la función en un espacio en memoria diferente al de los datos originales. Lo anterior permite manipular los datos dentro de la función sin temor a perder los datos originales. 

Sin embargo, esto hace el código menos eficiente ya que se debe dedicar instrucciones del procesador a hacer la copia de los datos. Por otro lado, si se usa un apuntador, ya no es necesario realizar esta copia ya que el apuntador indica directamente la posición en memoria de los datos por lo que se manipulan directamente dentro de la función. En este caso es mas eficiente porque no es necesario realizar una copia de los datos, pero el inconveniente es que se corre el riesgo de perder los datos originales. Para comparar el tiempo de ejecución de ambas alternativas se usó un ATmega162. Este microcontrolador se configuro para usar una señal de reloj externa, la cual se generó con un circuito externo.

![Hardware empleado para comparar el tiempo de ejecuci&#xF3;n ](../.gitbook/assets/image%20%2827%29.png)

A continuación, se muestra el programa usado para el ATmega162. Dentro del ciclo while hay un if-else que decise si se ejecuta una función de prueba pasando directamente un arreglo o su correspondiente apuntador. Como se puede ver en la Ilustración 40 que hay un pulsador conectado a una de las entradas digitales del ATmega162. Esta entrada digital es la que es verificada en el if-else para decidir que función se ejecuta. Para medir el tiempo de ejecución se hace la articulación de una de las salidas digitales.

```c
#define F_CPU 464UL //(500Khz) macro para definir la frecuencia de trabajo del microcontrolador. se usa en la implementacion del comando delay.

#include <avr/io.h>

#include <avr/io.h>
#include <avr/interrupt.h> // libreria de AVR que facilita uso de interrupciones
#include <util/delay.h>

// #define _BV( bit ) ( 1<<(bit) ) // macro para facilitar la escritura de los comandos para leer y escribir sobre registros del microcontrolador.

				
				
int mit_zeiger(double *p);
int kein_zeiger(double Ar[192]);


int main(void)
{
	
	// coeficientes del filtro FIR
	double FIR[] = {-1000, 2000, 3000, 40000,
					-100, 244, 355, 455,
					-1555, 2777, 377, 47,
					-1111, 2888, 3888, 4555,
					-11234, 2432, 364, 2004,
					-1347, 23754, 33456, 46345,
					-1567, 2987, 3263, 452345,
					-15678, 27878, 35867, 45345,
					-15678, 28765, 38768, 45876,
					-16587, 26875, 35876, 47568,
					-17658, 25867, 358, 485,
					-15987, 22352, 35245, 4542534,
					
					-1000, 2000, 3000, 40000,
					-100, 244, 355, 455,
					-1555, 2777, 377, 47,
					-1111, 2888, 3888, 4555,
					-11234, 2432, 364, 2004,
					-1347, 23754, 33456, 46345,
					-1567, 2987, 3263, 452345,
					-15678, 27878, 35867, 45345,
					-15678, 28765, 38768, 45876,
					-16587, 26875, 35876, 47568,
					-17658, 25867, 358, 485,
					-15987, 22352, 35245, 4542534,
					
					-1000, 2000, 3000, 40000,
					-100, 244, 355, 455,
					-1555, 2777, 377, 47,
					-1111, 2888, 3888, 4555,
					-11234, 2432, 364, 2004,
					-1347, 23754, 33456, 46345,
					-1567, 2987, 3263, 452345,
					-15678, 27878, 35867, 45345,
					-15678, 28765, 38768, 45876,
					-16587, 26875, 35876, 47568,
					-17658, 25867, 358, 485,
					-15987, 22352, 35245, 4542534,
					
					-1000, 2000, 3000, 40000,
					-100, 244, 355, 455,
					-1555, 2777, 377, 47,
					-1111, 2888, 3888, 4555,
					-11234, 2432, 364, 2004,
					-1347, 23754, 33456, 46345,
					-1567, 2987, 3263, 452345,
					-15678, 27878, 35867, 45345,
					-15678, 28765, 38768, 45876,
					-16587, 26875, 35876, 47568,
					-17658, 25867, 358, 485,
					-15987, 22352, 35245, 4542534					
	};
	
	
	// pin 0 del puerto C como salida digital.
	DDRC |= _BV(0);
	
	double *p = FIR; // se obtiene el apuntador del arreglo de 480 elementos.
	
    while (1) 
    {
		int k;
		if( PINC&_BV(1) ){
				k = mit_zeiger(p);
		} else {
				k = kein_zeiger(FIR);
		}
    }
}



// con apuntador.
int mit_zeiger(double *p){
	PORTC ^= _BV(0);
	return 1;
};


// pasando el arreglo completo.
int kein_zeiger(double Ar[192]){
	PORTC ^= _BV(0);
	return 1;
};

```

En el siguiente link de youtube : [https://youtu.be/l8B30wse0uI](https://youtu.be/l8B30wse0uI) se puede ver la ejecución del programa anterior donde se compara la velocidad de ejecución en ambos casos. 

{% embed url="https://youtu.be/l8B30wse0uI" %}

Se puede observar que pasando un apuntador en lugar de enviar directamente el arreglo se logra un tiempo de ejecución menor. Pasando el arreglo como argumento el tiempo de ejecución es 70.40s mientras que usando apuntador es 67.20s







