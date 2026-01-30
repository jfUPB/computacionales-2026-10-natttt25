# Unidad 1

## Bitácora de proceso de aprendizaje

Actividad 1:

¿Qué crees que haga este programa? 
Se suman 2 valores registrados en A y D y guarda en memoria 16

Reporta tus observaciones para cada experimento en tu bitácora de aprendizaje.
¿Qué diferencia hay entre los datos almacenados en la memoria ROM y en la RAM?
el ROM es memoria permanente que se guarda en el equipo asi no esté en uso o esté apagado, mientras que la RAM es memoria que guarda información temporal.

Actividad 2:

Identifica una instrucción que use la ALU y explica qué hace.
¿Para qué sirve el registro PC?
Guarda la direccion de una instrucción

¿Cuál es la diferencia entre @i y @READKEYBOARD?
@i (posicion 16) es una variable en memoria normal y @READKEYBOARD es una dirección de entrada asociada al teclado

Describe qué se necesita para leer el teclado y mostrar información en la pantalla.

Identifica un bucle en el programa y explica su funcionamiento.

Identifica una condición en el programa y explica su funcionamiento



Actividad 3:

Escribe un programa que compare el valor almacenado en la dirección de memoria 5 con el valor 10. Si el valor 
es menor que 10, guarda el valor 1 en la dirección 7. Si el valor es mayor o igual a 10, guarda el valor 0 
en la dirección 7.

Escribe tu mismo el programa.
Simula paso a paso. Recuerda la metodología: predice, ejecuta, observa y reflexiona.


Actividad 4:
@i 
M=1

(LOOP)
@i 
D=M 
@6 
D=A-D
@FINAL 
D;JEQ

@i 
D=M

@sum 
M=D+M

@i 
M=M+1 
@LOOP 
0;JMP

(FINAL)
@sum 
D=M 
@12 
M=D 
@END 
(END) 
0;JMP

Actividad 5:



-Describe con tus palabras las tres fases del ciclo Fetch-Decode-Execute. ¿Qué rol juega el Program Counter (PC) en este ciclo? El ciclo Fetch–Decode–Execute consiste en que primero la CPU busca (fetch) en memoria la instrucción indicada por el Program Counter (PC), luego decodifica (decode) qué tipo de instrucción es y qué debe hacer, y finalmente la ejecuta (execute) realizando cálculos, asignaciones o saltos. El PC guarda la dirección de la próxima instrucción a ejecutar y normalmente se incrementa en uno, excepto cuando ocurre un salto, en cuyo caso se carga con otra dirección.

-¿Cuál es la diferencia fundamental entre una instrucción-A (que empieza con @) y una instrucción-C (que involucra D, M, A, etc.) en el lenguaje ensamblador de Hack? Da un ejemplo de cada una. La diferencia fundamental entre una instrucción A y una instrucción C en Hack es que la instrucción A (que empieza con @) solo sirve para cargar un valor o dirección en el registro A, mientras que la instrucción C se usa para realizar cálculos, mover datos entre registros y memoria, o ejecutar saltos. Un ejemplo de instrucción A es @10, y un ejemplo de instrucción C es D=M+1. -Explica la función de los siguientes componentes del computador Hack: el registro D, el registro A y la ALU.

-¿Cómo se implementa un salto condicional en Hack? Describe un ejemplo (p. ej., saltar si el valor de D es mayor que cero). El registro D se utiliza para almacenar datos temporales y resultados de cálculos, el registro A puede almacenar tanto valores como direcciones de memoria (y cuando se usa M, se accede a la memoria apuntada por A), y la ALU es la unidad que realiza todas las operaciones aritméticas y lógicas del computador Hack.

-¿Cómo se implementa un loop en el computador Hack? Describe un ejemplo (p. ej., un loop que decremente un valor hasta que llegue a cero). Un salto condicional en Hack se implementa usando una instrucción C con un campo de salto (JGT, JEQ, JLT, etc.), que depende del resultado de la ALU. Por ejemplo, para saltar si el valor del registro D es mayor que cero se usa @ETIQUETA seguido de D;JGT.

-¿Cuál es la diferencia entre la instrucción D=M y la instrucción M=D? La diferencia entre D=M y M=D es la dirección del flujo de datos: D=M copia el contenido de la memoria RAM ubicada en la dirección almacenada en A hacia el registro D, mientras que M=D copia el contenido del registro D hacia la posición de memoria RAM indicada por A.

-Describe brevemente qué se necesita para leer un valor del teclado (KBD) y para “pintar” un pixel en la pantalla (SCREEN). Para leer un valor del teclado se accede a la dirección de memoria mapeada como KBD, cuyo contenido representa la tecla presionada, mientras que para pintar un píxel en la pantalla se escribe un valor en la región de memoria SCREEN, donde cada palabra controla 16 píxeles y escribir bits en 1 permite encenderlos.



## Bitácora de aplicación 



## Bitácora de reflexión
