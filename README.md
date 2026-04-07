Post-Contenido 1 — Manejo del DEBUG
Descripción del Laboratorio

En este laboratorio se configuró el entorno DOSBox y se utilizó el depurador DEBUG para inspeccionar el estado inicial del procesador, manipular memoria y desensamblar instrucciones. Se emplearon los comandos R, F, D, A y U para analizar el comportamiento del sistema en modo real.

El desarrollo del laboratorio se documentó mediante capturas de pantalla organizadas en el repositorio, siguiendo los checkpoints establecidos en la guía.

Entorno de Trabajo:

-DOSBox 0.74-3

-DEBUG

-Sistema Operativo: Windows

-Editor de texto: Visual Studio Code / Notepad

-GitHub para documentación


Checkpoint 1 — Estado Inicial de Registros

Se ejecutó el comando:

R

Este comando permitió visualizar el estado inicial de los registros del procesador.

Observaciones:

Los registros AX, BX, CX y DX se encontraban inicializados en 0000
El registro SP apuntaba al tope inicial de la pila
Los registros DS, ES, SS y CS tenían el mismo valor
El registro IP se encontraba en la dirección 0100
Se observó la instrucción INT 20 en la dirección inicial

Captura:

capturas/CP1_registros.png


Checkpoint 2 — Volcado de Memoria

Primero se rellenó la memoria con el comando:

F 200 L40 AB CD EF

Luego se visualizó con:

D 200 L40

Explicación de las columnas del comando D:

La primera columna representa la dirección de memoria en formato segmento:offset, indicando la ubicación de los datos. La segunda columna muestra los valores en formato hexadecimal organizados por bytes. La tercera columna corresponde a la representación ASCII de los datos almacenados. Cuando los valores no corresponden a caracteres imprimibles, DEBUG muestra puntos en su lugar. Este formato permite identificar patrones y analizar la memoria fácilmente.

Observaciones:

Se observó el patrón AB CD EF
El patrón se repite en las diferentes líneas
La columna ASCII muestra puntos por valores no imprimibles

Captura:

capturas/CP2_volcado_memoria.png


Checkpoint 3 — Ensamblado y Desensamblado

Se escribió el siguiente programa utilizando:

A 100

Programa:

MOV AX, 0005

MOV BX, 0003

ADD AX, BX

INT 20

Luego se verificó con:

U 100 109

Observaciones:

Se observó la correspondencia entre instrucciones y código máquina

MOV AX,0005 -> B8 05 00

MOV BX,0003 -> BB 03 00

ADD AX,BX -> 03 C3

INT 20 -> CD 20

Captura:

capturas/CP3_ensamblado_desensamblado.png

Conclusiones

Este laboratorio permitió comprender el funcionamiento del depurador DEBUG y la manipulación directa de memoria en modo real. Se observó cómo los registros del procesador pueden inspeccionarse y modificarse manualmente. También se analizó el comportamiento de la memoria mediante el relleno de patrones específicos.

Además, se comprobó que el procesador interpreta cualquier byte como instrucción al utilizar el comando de desensamblado. Finalmente, el ensamblado manual permitió entender la relación entre instrucciones en ensamblador y su representación en código máquina.
