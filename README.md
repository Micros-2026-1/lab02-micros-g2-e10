[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-22041afd0340ce965d47ae6ef1cefeee28c7c493a6346c4f15d667ab976d596c.svg)](https://classroom.github.com/a/KzqfxGd5)
[![Open in Visual Studio Code](https://classroom.github.com/assets/open-in-vscode-2e0aaae1b6195c2367325f4f02e2d04e9abb55f0b24a779b69b11b9e10269abc.svg)](https://classroom.github.com/online_ide?assignment_repo_id=22821779&assignment_repo_type=AssignmentRepo)
# Lab02 - Caracterización de osciladores (externo vs. interno)


## 1. Integrantes

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

### 2.2 Explicación del código implementado

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

## 2.5 Formas de onda

### INTOSC (interno) 


### HS

## RC

## 3. Evidencias de implementación

## 4. Preguntas

* ¿En qué modo se obtuvo la medición más cercana a la frecuencia teórica?

* ¿Fue posible evidenciar el fenómeno de deriva? ¿Qué factores podrían explicar la variación de frecuencia al calentar el PIC?

* ¿Cuál es más preciso en cuanto a frecuencia teórica vs. medida?


* Explique cómo usar RC0 para estimar la frecuencia del oscilador cuando RA6 no está disponible.

* Si se quisiera duplicar la frecuencia del PIC usando PLL, ¿en qué modos se podría aplicar?

* Enliste ventajas y desventajas de cada modo.

## 5. Referencias