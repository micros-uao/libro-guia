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

Método readSerialStart se encarga de crear el hilo donde se va a realizar la lectura de los datos

```python
    def readSerialStart(self):

        if self.thread == None:
            #Se crea el hilo y se relaciona con el metodo backgroundThread
            self.thread = Thread(target=self.backgroundThread)
            #Se inicia el hilo
            self.thread.start()
            # Espera a recibir valores
            while self.isReceiving != True:
                time.sleep(0.1)
```



Método initWindow se encarga de crear el canvas donde se va a situar la gráfica

```python
def initWindow(self, figure):
    self.master.title("Real Time Plot")
    canvas = FigureCanvasTkAgg(figure, master=self.master)
    #Posicion del canvas en la interfaz
    canvas.get_tk_widget().place( relx=0.35, rely=0.55, anchor=CENTER)
```

Método  backgroundThread es el que se ejecuta en el hilo y guarda los datos leídos en rawData

```python
    def backgroundThread(self):    # retrieve data
        #print("value : ")
        #Tiempo para que el buffer reciba la data
        time.sleep(1.0)
        #Limpiar buffer
        self.serialConnection.reset_input_buffer()
        #Lectura de datos
        while (self.isRun):
            #Se guardan los bytes leidos en rawdata
            self.serialConnection.readinto(self.rawData)
            #Bandera de lectura de datos
            self.isReceiving = True
```

Método getSerialData se encarga de seleccionar que datos se presentan en la gráfica, mostrar los datos que van en labels y mostrar el tiempo actual de muestreo del sistema.

```python
    def getSerialData(self, frame, lines, lineValueText, lineLabel, timeText):
        #Tiempo actual del programa
        currentTimer = time.clock()
        #Se restan el instante actual con el anterior y se multiplica por 1000
        self.plotTimer = int((currentTimer - self.previousTimer) * 1000)     # the first reading will be erroneous
        #Se guarda el instante actual en el instante anterior
        self.previousTimer = currentTimer
        #Se imprime el periodo con que se grafican los datos
        timeText.set_text('Plot Interval = ' + str(self.plotTimer) + 'ms')
        #Se guarda la data leida en la variable hola
        hola=self.rawData.decode()
        print("raw data : ")
        print(hola)
        #Se llama al objeto diferenciar el cual necesita de los datos leidos por serial
        self.diferenciar(hola)
        #Se muestra el valor de temperatura en la interfaz
        self.tempv["text"]=str('%.1f'%(self.dtemp*50))
        # Se muestra el valor del pulso en la interfaz
        self.pulsov["text"]=str(self.dpulse*200)
        # Se muestra el valor de la  concentracion de oxigeno en la interfaz
        self.oconv["text"]=str(self.dsp*100)
        #Se plotea ECG , EMG o GAlvanico dependiendo del resultado del metodo diferencia
        if (self.valor1==1):
            self.data.append(self.decg)  # we get the latest data point and append it to our array
            lines.set_data(range(self.plotMaxLength), self.data)
            lineValueText.set_text('[' + lineLabel[0] + '] = ' + str(self.decg))
        if(self.valor2==1):
            self.data.append(self.demg)  # we get the latest data point and append it to our array
            lines.set_data(range(self.plotMaxLength), self.data)
            lineValueText.set_text('[' + lineLabel[0] + '] = ' + str(self.demg))
        if(self.valor3==1):
            self.data.append(self.dgsr)  # we get the latest data point and append it to our array
            lines.set_data(range(self.plotMaxLength), self.data)
            lineValueText.set_text('[' + lineLabel[0] + '] = ' + str(self.dgsr*10))
```

Método diferenciar recibe la cadena de datos leídos , los separa de acuerdo a la cabecera de cada dato y su signo.

```python
    def diferenciar(self,dato):

        if dato[0] == "a":
            self.dtemp=float(dato[1:5])
            print("a")
        if dato[6] == "b":
            self.dsp=float(dato[7:11])
            print(dato[6])
        if dato[12] == "c":
            self.dpulse=float(dato[13:17])
            print("c")
        if dato[18] == "d":
            self.decg=float(dato[19:23])
            print("d")
        if dato[24] == "e":
            self.demg=float(dato[25:29])
            print("e")
        if dato[30] == "f":
           self.dgsr=float(dato[31:35])
           print("f")
        if dato[18] == "D":
               self.decg =-1* float(dato[19:23])
               print("D")
        if dato[24] == "E":
               self.demg =-1* float(dato[25:29])
               print("E")
        if dato[30] == "F":
               self.dgsr = -1*float(dato[31:35])
               print("F")
```

Con los siguiente métodos se establece mediante unos botones que dato es el que se interesa ver en la gráfica

```python
    #Metodo asociado al boton para que se grafique la señal ECG
    def ECG(self):
        self.valor1= 1
        self.valor2= 0
        self.valor3= 0

    # Metodo asociado al boton para que se grafique la señal EMG
    def EMG(self):
        self.valor1 = 0
        self.valor2 = 1
        self.valor3 = 0

    # Metodo asociado al boton para que se grafique la señal GSR
    def GSR(self):
        self.valor1 = 0
        self.valor2 = 0
        self.valor3 = 1
```

createWidgets se encarga de crear, dar las características y posicionar los diferentes widgets de la aplicación entre los cuales se están usando botones y labels, 

```python
    def createWidgets(self):
        #Estilo para los botonos
        but1font = ('Helvetica', 10, 'bold')
        #Se crea el boton del ECG , se le dan las caracteristicas , metodo asociado y posicion en la interfaz
        self.ecg = Tk.Button(command=lambda : self.ECG())
        self.ecg["text"] = "ECG"
        self.ecg["bg"] = "white"
        self.ecg["height"] = 5
        self.ecg["width"] = 5
        self.ecg["fg"] = "black"
        self.ecg["font"] = but1font
        #self.ecg["command"] = print("ecg")
        self.ecg.place( relx=0.80, rely=0.7, anchor=CENTER)

        # Se crea el boton del EMG , se le dan las caracteristicas , metodo asociado y posicion en la interfaz
        self.emg = Tk.Button(command=lambda : self.EMG())
        self.emg["text"] = "EMG"
        self.emg["bg"] = "white"
        self.emg["height"] = 5
        self.emg["width"] = 5
        self.emg["fg"] = "black"
        self.emg["font"] = but1font
        self.emg.place(relx=0.87, rely=0.7, anchor=CENTER)

        # Se crea el boton del GSR , se le dan las caracteristicas , metodo asociado y posicion en la interfaz
        self.gsr = Tk.Button(command=lambda : self.GSR())
        self.gsr["text"] = "GSR"
        self.gsr["bg"] = "white"
        self.gsr["height"] = 5
        self.gsr["width"] = 5
        self.gsr["fg"] = "black"
        self.gsr["font"] = but1font
        self.gsr.place(relx=0.94, rely=0.7, anchor=CENTER)

        # Se crea el boton de SALIR , se le dan las caracteristicas , metodo asociado y posicion en la interfaz
        self.salir = Tk.Button(command=lambda : self.exit())
        self.salir["text"] = "X"
        self.salir["bg"] = "white"
        self.salir["height"] = 2
        self.salir["width"] = 3
        self.salir["fg"] = "black"
        self.salir["font"] = but1font
        #self.salir.bind("<Button-1>",self.sumarnumero())
        self.salir.place(relx=0.99, rely=0.01, anchor=CENTER)

        #Estilo para las etiquetas
        labelfont=('Helvetica',60,'bold')
        #Label para el Titulo
        hola = Label(self.master, bg='black', fg='white', font=labelfont ,text="B-learning Tools", pady=5,padx=5, relief=FLAT)
        hola.place(relx=0.5, rely=0.1, anchor=CENTER)

        labelfont1 = ('Helvetica', 20, 'bold')
        # Label con la palabra PRbpm
        pulso = Label(self.master, bg='black', fg='white', font=labelfont1, text="PRbpm♥", pady=5, padx=5,relief=FLAT)
        pulso.place(relx=0.82, rely=0.25, anchor=CENTER)

        #Label para poner el dato de pulso transmitido
        lf1 = ('Helvetica', 20, 'bold')
        self.pulsov = Label(self.master, bg='black', fg='white', font=lf1, text=str(self.numero), pady=5, padx=5,relief=FLAT)
        self.pulsov.place(relx=0.92, rely=0.25, anchor=CENTER)

        labelfont2 = ('Helvetica', 20, 'bold')
        # Label con la palabra SpO2
        ocon = Label(self.master, bg='black', fg='white', font=labelfont2, text="%SpO2", pady=5, padx=5,relief=FLAT)
        ocon.place(relx=0.82, rely=0.35, anchor=CENTER)

        lf2 = ('Helvetica', 20, 'bold')
        #Label para poner el dato de conocentracion de oxigeno transmitido
        self.oconv = Label(self.master, bg='black', fg='white', font=lf2, text="####", pady=5, padx=5,relief=FLAT)
        self.oconv.place(relx=0.92, rely=0.35, anchor=CENTER)

        labelfont3 = ('Helvetica', 20, 'bold')
        # Label con la palabra View signals
        signs = Label(self.master, bg='black', fg='white', font=labelfont3, text="View Signals", pady=5, padx=5,relief=FLAT)
        signs.place(relx=0.87, rely=0.55, anchor=CENTER)

        # Label con la palabra Temp
        temp = Label(self.master, bg='black', fg='white', font=labelfont3, text="Temp °:", pady=5, padx=5,relief=FLAT)
        temp.place(relx=0.82, rely=0.45, anchor=CENTER)

        lf3 = ('Helvetica', 20, 'bold')
        #Label para poner el dato de temperatura transmitido
        self.tempv = Label(self.master, bg='black', fg='white', font=lf3, text="#####", pady=5, padx=5,relief=FLAT)
        self.tempv.place(relx=0.92, rely=0.45, anchor=CENTER)

```

Por ultimo el main del programa donde se inicializan los valores del puerto serial con sus parámetros, se crean las instancias para la interfaz , la gráfica y sus características  y los métodos relacionados con la lectura de datos. 

```python
def main():

    #Se inicializan los parametros para crear el puerto Serie
    portName = '/dev/ttyACM0'
    baudRate = 115200
    maxPlotLength = 100
    #Numero de bytes que va a leer el puerto
    dataNumBytes = 36       # number of bytes of 1 data point
    #Se crea una instancia de Tk
    root = Tk.Tk()
    #Se configura el fondo de la interfaz
    root.config(background='black')
    #Se configura el tamaño de el elemento graficador
    fig = plt.figure(figsize=(8, 5))
    #Periodo en el cual la animacion grafica cada dato
    pltInterval = 50
    #Limites de la grafica
    xmin = 0
    xmax = 100
    ymin = -(1)
    ymax = 1
    #Grafica donde se van a observar los datos y su configuracion
    ax = plt.axes(xlim=(xmin,xmax), ylim=(float(ymin - (ymax - ymin) / 10), float(ymax + (ymax - ymin) / 10)))
    #Se instancia la clase serialPlot con sus respectivos parametros
    s = serialPlot(root,fig,portName,  baudRate, maxPlotLength, dataNumBytes)
    #Se inicia la comunicacion serial
    s.readSerialStart()
    #Se configrua el color de los ejes y el marco de la grafica
    ax.spines['bottom'].set_color('white')
    ax.spines['top'].set_color('white')
    ax.spines['left'].set_color('white')
    ax.spines['right'].set_color('white')
    ax.tick_params(axis='x',colors='white')
    ax.tick_params(axis='y', colors='white')
    #Labels
    ax.set_title('e-HEALTH Monitor', color="white",fontsize=18)
    ax.set_xlabel("Time", color="white",fontsize=18)
    ax.set_ylabel("Output Value", color="white",fontsize=18)
    #
    lineLabel = ['X', 'Y', 'Z']
    style = ['w-', 'c-', 'b-']  # linestyles for the different plots

    timeText = ax.text(0.50, 0.95, '', transform=ax.transAxes, color="white")
    #Variable donde se va a guardar el dato que llegue por serial
    lines = ax.plot([], [], label=lineLabel,color="blue")[0]
    lineValueText = ax.text(0.50, 0.90, '', transform=ax.transAxes,color="blue")
    #Se crea el Canvas animation y se le pasa los argumentos
    anim = animation.FuncAnimation(fig, s.getSerialData, fargs=(lines, lineValueText, lineLabel, timeText),interval=pltInterval)  # fargs has to be a tuple
    #Se inicia la interfaz en un loop
    root.mainloop()
    #Si se cierra la interfaz el puerto serie se cierra
    s.close()

```

Para descargar los códigos completos se pueden descargar desde el repositorio.

#### Código en Python

{% embed url="https://github.com/micros-uao/codigos/tree/master/monitor" %}

#### Código para Arduino

{% embed url="https://github.com/micros-uao/codigos/tree/master/Prueba\_E-health\_Due2\_2" %}

