[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-22041afd0340ce965d47ae6ef1cefeee28c7c493a6346c4f15d667ab976d596c.svg)](https://classroom.github.com/a/KzqfxGd5)
[![Open in Visual Studio Code](https://classroom.github.com/assets/open-in-vscode-2e0aaae1b6195c2367325f4f02e2d04e9abb55f0b24a779b69b11b9e10269abc.svg)](https://classroom.github.com/online_ide?assignment_repo_id=22821779&assignment_repo_type=AssignmentRepo)
# Lab02 - Caracterización de osciladores (externo vs. interno)


## 1. Integrantes

* [EDWARD ALEXANDER RODRIGUEZ](https://github.com/Edwardrodriguez99)
* [JUAN CAMILO SAMPER](https://github.com/CamiloSp22)
* [CRISTIAN FABIAN LOZANO](https://github.com/cristianfalozanoav)

## 2. Documentación

En cualquier sistema digital, el reloj es el elemento que sincroniza todas las operaciones. Sin una señal periódica estable, el sistema no puede ejecutar instrucciones de manera ordenada ni mantener coherencia temporal.

El oscilador es, por tanto, es el corazón del sistema, ya que determina la frecuencia a la que se ejecutan las instrucciones y la velocidad de operación. La elección del tipo de oscilador influye directamente en:

* Precisión de temporización

* Estabilidad del sistema

* Consumo energético

* Costo del diseño

* Complejidad del circuito

En este laboratorio se compararán dos tipos de osciladores: el oscilador interno y el oscilador externo tipo RC. Antes de analizar sus diferencias y resultados, es importante comprender con mayor detalle qué es un oscilador.

**¿Qué es un oscilador?**

Un oscilador es un circuito que genera una señal repetitiva en el tiempo. En sistemas digitales esa señal actúa como reloj. Cada pulso indica cuándo se debe ejecutar una operación.

La frecuencia del oscilador determina la velocidad del sistema. Por ejemplo, si el reloj trabaja a mayor frecuencia, el sistema puede ejecutar más instrucciones por segundo. Si la frecuencia es baja, el sistema será más lento.

Además, muchas funciones dependen directamente del reloj, como:

* Los retardos por software (delay_ms)

* Los temporizadores

* La comunicación serial

* La generación de señales PWM

**Oscilador interno**

El oscilador interno viene integrado dentro del microcontrolador. No necesita resistencias, capacitores ni cristales externos. Se configura por software y permite trabajar a distintas frecuencias.

**¿Qué ventajas tiene?**

* Es fácil de usar.

* No requiere componentes adicionales.

* Reduce el costo del circuito.

* Es bastante estable para la mayoría de aplicaciones.

**Oscilador externo RC**

El oscilador RC externo utiliza una resistencia (R) y un capacitor (C) conectados a los pines de reloj del sistema para generar la señal periódica. La frecuencia generada depende de los valores de estos dos componentes y puede estimarse con la fórmula aproximada:

f ≈ 1 / (4RC)

Esto dandonos a entender que cualquier cambio en la resistencia o el capacitor altera directamente la frecuencia del sistema. A diferencia del oscilador interno, aquí la estabilidad depende de factores físicos externos.

### 2.1 Descripción del laboratorio

Este laboratorio tiene como objetivo comparar el comportamiento de diferentes configuraciones que pueden emplearse para implementar un oscilador. Para ello, se realizarán los cálculos teóricos correspondientes a cada configuración y posteriormente se contrastarán con los resultados obtenidos en la práctica.

El propósito de esta comparación es evaluar qué tan precisos son los resultados experimentales con respecto a los cálculos realizados. Además, se analizará el comportamiento de las señales generadas mediante el uso del osciloscopio, lo que permitirá observar y estudiar las características de cada configuración de oscilador.

### 2.2 Explicación del código implementado

Una vez comprendido el papel del oscilador dentro del sistema y su influencia en la velocidad y sincronización del microcontrolador, es importante analizar cómo estas configuraciones se implementan a nivel de programación. Para ello, a continuación se presenta el código desarrollado para este laboratorio, en el cual se realiza la configuración del microcontrolador y del tipo de oscilador utilizado. Además, se explicará el funcionamiento de cada una de las secciones del programa, con el fin de entender cómo el código permite controlar el comportamiento del sistema y ejecutar las instrucciones de manera adecuada durante la práctica.

En la primera parte del código se pueden observar las siguientes instrucciones:

![Configuracion librerias](/imagenes/librerias.png)

En esta sección se incluyen las primeras líneas del programa, cuya función es incorporar las librerías necesarias para la correcta compilación y ejecución del código. El comando ```#include <xc.h>``` permite acceder a las definiciones y configuraciones propias del compilador, en este caso es el compilador XC8. Por otro lado, la librería ```#include <stdint.h>``` proporciona tipos de datos enteros de tamaño definido, lo que ayuda a manejar la memoria de forma más controlada y evita posibles desbordamientos de datos durante la ejecución del programa.

Una vez incorporadas las librerías necesarias, la siguiente parte del código se encarga de realizar la configuración inicial del sistema, permitiendo establecer los parámetros que controlarán el funcionamiento del microcontrolador durante la ejecución del programa.

![Configuracion generales del PIC](/imagenes/configuraciones.png)

Para comprender cómo funcionan estas configuraciones iniciales del sistema, es necesario analizar a qué corresponde cada una de las instrucciones presentes en el código. En este caso, varias de ellas comienzan con la palabra ```#Pragma```, la cual se utiliza para indicarle al compilador que debe aplicar ciertas configuraciones al microcontrolador antes de generar el programa final. Dicho de otra forma, estas instrucciones permiten definir algunos parámetros internos que determinan cómo se comportará el sistema cuando el programa empiece a ejecutarse.

En particular, las instrucciones que utilizan ```#pragma config``` permiten establecer lo que se conoce como bits de configuración del microcontrolador. Estos bits controlan diferentes aspectos del funcionamiento del dispositivo, como la activación o desactivación de ciertos módulos internos, opciones de protección del programa o mecanismos que ayudan a mantener estable el funcionamiento del sistema.

A continuación, se describen brevemente algunas de las configuraciones utilizadas en el código implementado:

* ```#pragma config WDTEN = OFF```
Esta configuración desactiva el Watchdog Timer, un temporizador interno que supervisa el funcionamiento del programa. Cuando este temporizador está activo, el microcontrolador puede reiniciarse automáticamente si detecta que el programa se ha detenido o no está respondiendo correctamente. En este caso se desactiva para evitar reinicios durante el desarrollo del laboratorio.

*  ```#pragma config LVP = OFF```
Esta instrucción desactiva el modo de programación a bajo voltaje. Este modo permite programar el microcontrolador utilizando una tensión menor en uno de sus pines, pero también puede interferir con el uso normal de ese pin dentro del circuito. Por esta razón, cuando no se necesita utilizar esta forma de programación, se suele deshabilitar.

* ```#pragma config PBADEN = OFF```
Define el comportamiento inicial de algunos pines del puerto B. Cuando esta opción está desactivada, dichos pines funcionan directamente como entradas o salidas digitales, lo cual facilita su uso para controlar dispositivos como LEDs o leer el estado de interruptores.

* ```#pragma config CP0 = OFF, CP1 = OFF, CP2 = OFF, CP3 = OFF```
Estas configuraciones están relacionadas con la protección del código almacenado en la memoria del microcontrolador. Cuando están activadas, impiden que el programa sea leído o copiado desde el dispositivo. En este caso se mantienen desactivadas, lo cual permite acceder al código sin restricciones durante las pruebas y el desarrollo.

* ```#pragma config BOREN = OFF```
Esta opción controla la función de reinicio por caída de voltaje. Cuando está activada, el microcontrolador se reinicia automáticamente si la tensión de alimentación cae por debajo de un nivel seguro. En este laboratorio se desactiva para simplificar el comportamiento del sistema durante la simulación.

* ```#pragma config FCMEN = OFF```
Esta configuracion corresponde a un mecanismo que supervisa el funcionamiento del reloj del sistema. Si el reloj principal falla, el microcontrolador puede cambiar automáticamente a otro reloj interno para evitar que el sistema se detenga. En este caso se desactiva porque no es necesario para el funcionamiento básico del laboratorio.

* ```#pragma config IESO = OFF```
Esta configuración está relacionada con el cambio automático entre el oscilador interno y el externo durante el arranque del sistema. Cuando está habilitada, el microcontrolador puede iniciar utilizando el oscilador interno mientras el oscilador externo se estabiliza. En este laboratorio se desactiva para mantener un comportamiento más simple y controlado del reloj del sistema.

Una vez establecidas las configuraciones generales del microcontrolador, el siguiente paso dentro del código consiste en definir el modo de oscilador que utilizará el sistema. Como se mencionó anteriormente, el oscilador es el encargado de generar la señal de reloj que sincroniza la ejecución de las instrucciones, por lo que su configuración tiene una influencia directa en la velocidad y el comportamiento del sistema.

En el código implementado se incluyó una sección que permite seleccionar entre diferentes tipos de oscilador, lo que facilita realizar pruebas y comparar su funcionamiento sin necesidad de modificar gran parte del programa. Para ello se utiliza una constante llamada ```MODE```, la cual determina qué tipo de oscilador será configurado durante la compilación.

![Modos de oscilador del PIC](/imagenes/modos.png)

* ```if MODE == 1```
Establece que cuando mi constante ```MODE``` sea 1, el sistema se configura para utilizar el oscilador interno del microcontrolador. Ademas de usar la directiva ```#pragma config FOSC = INTIO67 ``` para indicar que el oscilador empleado sera el interno; y la directiva ```USE_PLL = 0``` para no emplear el multiplicador de frecuencia.

* ```if MODE == 2 ```
Cuando la constante ```MODE``` sea 2, el microcontrolador se configura para trabajar con un cristal externo de alta velocidad (```#pragma config FOSC = HSHP```).
En este caso se emplea la directiva ```#pragma config PLLCFG = ON``` que activa el multiplicador de frecuencia PLL, el cual permite aumentar la frecuencia del reloj multiplicándola internamente y finalmente se establece ```USE_PLL = 1``` para emplear el multiplicador de frecuencia.

* ```if MODE == 3 ```
Cuando en este modo la constante ```MODE``` sea 3, el sistema configurará el microcontrolador para trabajar con un oscilador RC externo. Esto se define mediante la instrucción ```#pragma config FOSC = RC```, que indica al hardware que el reloj del sistema se obtendrá de un circuito formado por una resistencia y un condensador conectados externamente.
En este mismo bloque también se define``` USE_PLL``` con valor 0, lo que significa que el multiplicador de frecuencia PLL no se utilizará en este modo.
Finalmente, en esta sección del código se implementa una línea de código, la cual establece que, si el valor de ```MODE``` no coincide con ninguno de los modos definidos en el programa, el compilador mostrará un error indicando que el modo de oscilador es inválido. Esto sirve como una especie de protección para evitar compilar el programa con una configuración incorrecta.

**Definición de Frecuencia del oscilador**

![Modos de oscilador del PIC](/imagenes/Frecuencia.png)

En esta parte se define la constante``` _XTAL_FREQ```, que representa la frecuencia a la que trabaja el microcontrolador.
Esta constante es muy importante porque el compilador la utiliza para calcular correctamente los tiempos de las funciones de retardo como __delay_ms().
El código contempla varias situaciones. Si el programa está funcionando en los modos 1 o 2, primero se revisa si el PLL está habilitado. Si el PLL está activo, la frecuencia del sistema se multiplica y llega a 64 MHz. Si el PLL no está habilitado, la frecuencia se mantiene en 16 MHz.

**Division de funciones**

![delay](/imagenes/delay.png)

En esta sección del código se definen varias funciones, entre ellas se encuentra la siguiente función que se muestra, esta permite generar retardos en milisegundos.
La función ```delay_ms``` recibe como parámetro una variable que indica la cantidad de milisegundos que se desea esperar. Internamente se utiliza un ciclo while que se ejecuta hasta que el contador llega a cero.
En cada iteración del ciclo se llama a la función ```__delay_ms(1)```, que produce un retardo de un milisegundo. De esta forma, si se llama a la función con un valor de 10, el programa generará un retardo total de aproximadamente 10 milisegundos.

* ```Establecimiento de pines```

Antes de utilizar los pines del microcontrolador, es necesario configurarlos correctamente como entradas o salidas. Para este propósito se define la función init_pins.

![pines](/imagenes/init.png)

En este caso se configura el pin RC0 como salida digital. Esto se realiza modificando el registro TRISC, donde un valor de 0 indica que el pin funcionará como salida.
Posteriormente se utiliza el registro LATC para establecer el estado inicial del pin, colocándolo en nivel bajo. Esto asegura que el pin comience en un estado conocido cuando el programa se ejecute.

Dentro de la misma función de inicialización de pines, se incluye una condición para configurar el pin RA6 solo cuando el modo de funcionamiento lo permite.
En este fragmento se verifica si el sistema está trabajando en un modo que permite utilizar el pin RA6 como salida. Si la condición se cumple, el pin se configura como salida digital y se inicializa en nivel bajo.

* ```Oscilador```

Una vez configurados los pines, el siguiente paso consiste en preparar el sistema de reloj del microcontrolador. Esto se realiza mediante la función ```init_oscillator```.

![configuracion de oscilador](/imagenes/oscilador.png)

En este bloque se configura el registro ```OSCCON```, que controla diferentes aspectos del oscilador interno del microcontrolador. El campo ```IRCF``` se establece en el valor 0b111, lo que indica que el oscilador interno operará a una frecuencia de 16 MHz.
Posteriormente se configura el campo ```SCS```, el cual determina la fuente de reloj del sistema. En este caso se selecciona el oscilador primario como fuente principal.

* ```PLL```

En esta sección se verifica si el PLL debe activarse o mantenerse desactivado.

[PLL](/imagenes/PLL.png)

Si el valor de ```USE_PLL``` es igual a 1, el programa habilita el PLL mediante el registro ```OSCTUNE```. Esto permite multiplicar la frecuencia del reloj del sistema.
En caso contrario, el programa se asegura de que el PLL permanezca desactivado.
Esto ayuda a evitar configuraciones innecesarias o posibles conflictos en el funcionamiento del sistema.

**Programa principal**

Para finalizar abarcaremos el programa principal, el cual, tiene como punto de inicio la función main.}

![configuracion de oscilador](/imagenes/programa.png)

En esta parte del código se llaman primero las funciones encargadas de inicializar los pines y el oscilador. Esto garantiza que el microcontrolador esté correctamente configurado antes de ejecutar la lógica principal del programa.
Posteriormente el programa entra en un bucle infinito donde se ejecuta la tarea principal del sistema.
Dentro de este ciclo el pin RC0 cambia constantemente de estado. Primero se establece en nivel alto y se mantiene así durante un milisegundo. Luego se coloca en nivel bajo durante otro milisegundo.
Este proceso se repite continuamente, generando una señal cuadrada en el pin RC0. Debido a que cada ciclo completo dura aproximadamente dos milisegundos, la señal resultante tiene una frecuencia cercana a 500 Hz.
Esta señal puede utilizarse para diferentes aplicaciones, como el parpadeo de un LED, la generación de señales de prueba o la verificación del funcionamiento del sistema de reloj del microcontrolador.


### 2.3 Análisis y comparación

#### Tabla 1: Medición en frío

| Modo de oscilador | Freq. teórica Fosc | RA6 medible (CLKO)? | Freq. medida RA6 (Hz) | Freq. teórica RC0 (Hz)| Freq. medida RC0 (Hz) | Error RC0 (%) |  
|------------------|------------------|---------------------|---------------|---------------------|---------------|---------------|
| INTOSC (interno) | 16,000,000       | Sí                 |                     |                500                 |               |               | |
| HS (cristal externo 16 MHz) | 16,000,000 | No |     NA      |               500                 |               |               |
| RC externo       | ~16,000,000*     | No                                    |       N/A        | 500                 |               |               | |

#### Tabla 2: Medición con calor

| Modo de oscilador | Freq. teórica Fosc | RA6 medible (CLKO)? | Freq. medida RA6 (Hz) | Freq. teórica RC0 (Hz)| Freq. medida RC0 (Hz) | Error RC0 (%) |  
|------------------|------------------|---------------------|---------------|---------------------|---------------|---------------|
| INTOSC (interno) | 16,000,000       | Sí                 |                     |                500                 |               |               | |
| HS (cristal externo 16 MHz) | 16,000,000 | No |     NA      |               500                 |               |               |
| RC externo       | ~16,000,000*     | No                                    |       N/A        | 500                 |               |               | |

#### Tabla 3: Deriva

| Modo de oscilador |RC0 deriva (Hz) |
|------------------|--------------------|
| INTOSC (interno) |                    |                
| HS (cristal externo 16 MHz) |                |                |
| RC externo       |                 |                


<!-- Agregar tablas para valores usando PLL -->

<!-- Complemente con análisis de lo registrado en tablas -->

## 2.4 Diagramas


<p align="center">
<img src="/imagenes/HS.png" alt="esp11" width="450">
</p>
<p align="center">
  Diagrama oscilador externo HS <b>[1]</b>
</p>

<p align="center">
<img src="/imagenes/RC.png" alt="esp11" width="450">
</p>
<p align="center">
  Diagrama oscilador externo RC <b>[1]</b>
</p>

## 2.5 Formas de onda

### INTOSC (interno) 

<p align="center">
<img src="/imagenes/RA6.png" alt="esp11" width="450">
</p>
<p align="center">
  Onda oscilador interno <b>[1]</b>
</p>

### HS

<p align="center">
<img src="/imagenes/CRISTAL.png" alt="esp11" width="450">
</p>
<p align="center">
  Onda cristal config HS <b>[1]</b>
</p>

## RC

<p align="center">
<img src="/imagenes/RC2.png" alt="esp11" width="450">
</p>
<p align="center">
  Onda RC <b>[1]</b>
</p>


## 3. Evidencias de implementación

<p align="center">
<img src="/imagenes/implementacion.png" alt="esp11" width="450">
</p>
<p align="center">
  Montaje <b>[1]</b>
</p>


## 4. Preguntas

* ¿En qué modo se obtuvo la medición más cercana a la frecuencia teórica?

* ¿Fue posible evidenciar el fenómeno de deriva? ¿Qué factores podrían explicar la variación de frecuencia al calentar el PIC?

* ¿Cuál es más preciso en cuanto a frecuencia teórica vs. medida?


* Explique cómo usar RC0 para estimar la frecuencia del oscilador cuando RA6 no está disponible.

* Si se quisiera duplicar la frecuencia del PIC usando PLL, ¿en qué modos se podría aplicar?

* Enliste ventajas y desventajas de cada modo.

## 5. Referencias