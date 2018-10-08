# 5.3 Código

El código para el caso de estudio 2 monitor de signos vitales es un programa implementado en un arduino DUE para la adquisicion de las señales fisiologicas con ayuda de la plataforma e-Health Sensor Platform V2.0  y se comunica por un puerto serial con una raspberry para transmitir los datos de las señales con el fin de realizar la interfaz gráfica para el usuario en python.

### Código Arduino DUE para la adquisición de los datos:

Primero se declaran las variables globales:

```c
//Variables para contadores 
int cont=0;
int conta=0;
//Variables Fisiologicas
float SPO2=0;
float BPM=0;
float ECG=0;
float EMG=0;
float galv=0;
float temp=0;
float sp=0;
float pulse=0;
//Arreglo utilizado para leer el pulsioximetro
uint8_t digito[41]={0};
//Variables para indicar los estados del 7 Segmentos del pulsioximetro
uint8_t A = 0;
uint8_t B = 0;
uint8_t C = 0;
uint8_t D = 0;
uint8_t E = 0;
uint8_t F = 0;
uint8_t G = 0;
```

Se inicializan los pines y hardware de la plataforma:

```c
void setup() {
  //Se inicializan el puerto serial del DUE
  Serial.begin(115200);
  //Se elige la resolucion para la salida analogica
  analogWriteResolution(12);
  //Se elige la resolucion para la entrada analogica
  analogReadResolution(12);
  //Se inician los pines digitales para la lectura del pulsioximetro
  initPulsioximeter();
  
  pinMode(6, INPUT);
  //Se configura el pin 6 para recibir interrupciones del pulsioximetro y se relaciona al metodo readPulsioximeter
  attachInterrupt(6, readPulsioximeter, RISING);

}
```

Luego se crea un método para cada sensor de la plataforma , en este caso los que se van a usar en el caso de estudio:

Temperatura:

```c
//Metodo para obtener el valor de la temperatura
float getTemperature(void)
  { 
    //Variables locales
    float Temperature; //Temperatura Corporal 
    float Resistance;  //Sensor resistivo.
    float ganancia=5.0;
    float Vcc=3.3;
    float RefTension=3.0; // Voltaje de referencia para el puente de wheastone.
    float Ra=4700.0; //Resistencia del puente Wheatstone.
    float Rc=4700.0; //Resistencia del puente Wheatstone.
    float Rb=769.0; //Resistencia del puente Wheatstone.
    int sensorValue = analogRead(A3);
    
    float voltage2=((float)sensorValue*Vcc)/4095; // Conversion de binario a voltaje

    // Salida de voltaje del puente de Wheatstone.
    voltage2=voltage2/ganancia;
    // Calculo del sensor resistivo usando el voltaje
    float aux=(voltage2/RefTension)+Rb/(Rb+Ra);
    Resistance=Rc*aux/(1-aux);

    //De acuerdo al rango del valor de la resistencia se halla la temperatura    
    if (Resistance >=1822.8) {
      // if temperature between 25ÂºC and 29.9ÂºC. R(tÂª)=6638.20457*(0.95768)^t
      Temperature=log(Resistance/6638.20457)/log(0.95768);  
    } else {
      if (Resistance >=1477.1){
          // if temperature between 30ÂºC and 34.9ÂºC. R(tÂª)=6403.49306*(0.95883)^t
          Temperature=log(Resistance/6403.49306)/log(0.95883);  
      } else {
        if (Resistance >=1204.8){
          // if temperature between 35ÂºC and 39.9ÂºC. R(tÂª)=6118.01620*(0.96008)^t
          Temperature=log(Resistance/6118.01620)/log(0.96008); 
        }
        else{
          if (Resistance >=988.1){
            // if temperature between 40ÂºC and 44.9ÂºC. R(tÂª)=5859.06368*(0.96112)^t
            Temperature=log(Resistance/5859.06368)/log(0.96112); 
          }
          else {
            if (Resistance >=811.7){
              // if temperature between 45ÂºC and 50ÂºC. R(tÂª)=5575.94572*(0.96218)^t
              Temperature=log(Resistance/5575.94572)/log(0.96218); 
            }
          }
        }
      }  
    }
   
    return Temperature;
    }
```

Galvánico:

```c
 //Metodo para leer la conductancia de la piel 
  float getSkinConductance(void)
  {
    // Variables locales.   
    float resistance;
    float conductance;
    
    // Se lee el voltaje analogico del pin 2
    float sensorValue = analogRead(A2);
    float voltage = (float)sensorValue*(3.3/4095);
    //Se calcula la conductancia
    conductance = 2*((voltage - 0.5) / 100000);

    // Conductance calculation
    resistance = 1 / conductance;
    //Se multiplica por una ganancia debido a que el valor es muy bajo 
    conductance = conductance * 1000000;
   
    if (conductance > 1)  return conductance;
    else return -1.0;
  }
```

Pulsioximetro:

```c
void readPulsioximeter(void){
    
    // Condicion para enviar los datos del pulsioximetro
    if(conta>50){
    //digito[41]={0};
    
    for (int i = 0; i<41 ; i++) { // Se leen los estados de los leds del dispositivo
      A = !digitalRead(13);
      B = !digitalRead(12);
      C = !digitalRead(11);
      D = !digitalRead(10);
      E = !digitalRead(9);
      F = !digitalRead(8);
      G = !digitalRead(7);

      //Convierte los estados de los leds al numero que estan mostrando
      digito[i] = segToNumber(A, B, C ,D ,E, F,G);  
     //delay minimo para que el sistema pueda leer los leds
      delayMicroseconds(300); //300 microseconds 
      //if (digito[i]=9) Serial.println(i);     
      
    }

   //Se extrae la informacion del arreglo leido y se convierte a un numero  
   SPO2=10 * digito[27] + digito[22]+digito[9];//Concentracion de oxigeno
   BPM=100 * digito[19] + 10 * digito[2] + digito[0];//Pulso
   //Se reinicia el contador
   conta=0;  
    }
  
   }
```

EMG:

```c
//Metodo para leer el voltaje analogico del EMG
 float  getEMG(void)
  {
    float analog0;
    // Read from analogic in. 
    analog0=analogRead(A8);
    // binary to voltage conversion
    return analog0 = analog0 * (3.3 / 4095.0); 
  }
```

ECG:

```c
//Metodo para leer el voltaje analogico del ECG
float getECG(void)
  {
    float analog0;
    // Read from analogic in. 
    analog0=analogRead(A0);
    // binary to voltage conversion
    return analog0 = analog0 * 3.3 / 4095.0;   
    //return analog0;
  }
```

Ciclo del programa:

```c
void loop() {
          //Contador para que se envie el dato del pulsioximetro despues de 50 interrupciones
          conta=conta+1;
          //Se almacena el dato ECG
          ECG = getECG()-1.5;
          //Se almacena el dato EMG
          EMG= getEMG();
          //Se almacena el dato Galvanico 
          galv=getSkinConductance();
          //Se almacena el dato de temperatura
          temp=getTemperature()/50.0;
          //Envio de datos, se especifica la cantidad de bytes por dato y una letra asociada a cada dato
          Serial.print('a');
          Serial.print(temp,3);

          Serial.print('b');
          Serial.print(SPO2/100,3);
          
          Serial.print('c');
          Serial.print(BPM/200,3);

          //Los datos que tienen valores negativos se envian con una letra mayuscula primero
          if(ECG<0){
          Serial.print('D');
          Serial.print(abs(ECG),3);
          }else{
          Serial.print('d');
          Serial.print(ECG,3);
          }

          
          Serial.print('e');
          Serial.print(EMG,3);

          if(galv<0){
          Serial.print('F');
          Serial.print(abs(galv),3);
          }else{
          Serial.print('f');
          Serial.print(galv/10,3);
          }
          //retraso para volver a enviar datos
          delay(50);
} 
```

### Código en Python para gráficar los datos:

Primero se importan las librerías necesarias, pueden utilizar el pip para instalar las que no tengas. El Código se realizó en python 2.7 para trabajar en raspberry pi 3.

```python
# Se importan las librerias
from ttk import *
from Tkinter import *
from threading import Thread
import serial
import time
import collections
import matplotlib.pyplot as plt
import matplotlib.animation as animation
from matplotlib.backends.backend_tkagg import FigureCanvasTkAgg, NavigationToolbar2TkAgg
import Tkinter as Tk
from ttk import Frame

```

Para realizar el programa se utilizó una clase llamada serialPlot la cual se modificó para el caso de estudio, los métodos que se utilizaron de la clase son los siguientes:

Metodo \_\_init\_\_ es el encargado de inicializar los valores de las variables que utilizan los métodos

```python
#Metodo que inicializa la clase , recibe unos argumentos necesarios para establecer la comunicacion
def __init__(self, master, figure, serialPort , serialBaud , plotLength , dataNumBytes ):
     global ax
     #Se inicia la clase Frame para usar sus widgets posteriormente
     Frame.__init__(self, master)
     #Las siguientes son Variables que sirven para la ejecucion de los metodos de la clase serialPlot
     self.port = serialPort
     self.baud = serialBaud
     self.plotMaxLength = plotLength
     self.dataNumBytes = dataNumBytes
     #Se crea un arreglo de bytes para recibir los datos leidos por el serial
     self.rawData = bytearray(dataNumBytes)
     self.data = collections.deque([0] * plotLength, maxlen=plotLength)
     self.isRun = True
     self.isReceiving = False
     self.thread = None
     self.plotTimer = 0
     self.previousTimer = 0
     self.dtemp=0
     self.dsp=0
     self.dpulse=0
     self.decg=0
     self.demg=0
     self.dgsr=0
     self.valor1 = 0
     self.valor2 = 0
     self.valor3 = 0
     self.numero = 0
     #Se agregan los wigets a la interfaz
     self.pack()
     #Se crean los widgets
     self.createWidgets()
     self.entry = None
     self.setPoint = None
     self.master = master  # a reference to the master window
     #SE activa la caracteristica del fig para que cuando se presiones Esc se cierre el programa
     self.master.bind("<Escape>", exit)
     #Se guardan el ancho y alto del monitor
     w, h = self.master.winfo_screenwidth(), self.master.winfo_screenheight()
     # use the next line if you also want to get rid of the titlebar
     # self.master.overrideredirect(1)
     #Se le dan las medidas a la ventana del programa
     self.master.geometry("%dx%d+0+0" % (w, h))
     #Se inicializa la ventana y se le pasa por parametro la grafica
     self.initWindow(figure)  # initialize the window with our settings

     print('Trying to connect to: ' + str(serialPort) + ' at ' + str(serialBaud) + ' BAUD.')
     #SE crea la intancia para el puerto Serial
     try:
         self.serialConnection = serial.Serial(serialPort, serialBaud, timeout=4)
         print('Connected to ' + str(serialPort) + ' at ' + str(serialBaud) + ' BAUD.')
     except:
         print("Failed to connect with " + str(serialPort) + ' at ' + str(serialBaud) + ' BAUD.')
```

