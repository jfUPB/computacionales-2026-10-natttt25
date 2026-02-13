# Unidad 2

## Bitácora de proceso de aprendizaje
1. <img width="1295" height="601" alt="image" src="https://github.com/user-attachments/assets/790479ba-2794-4f4d-8cf3-0b79af42ee9e" />

2.<img width="1183" height="579" alt="image" src="https://github.com/user-attachments/assets/b5016cfc-ac50-4e04-90c3-b2b413b5ab55" />


3.(START)
//i = SCREEN
@SCREEN
D=A
@i
M=D
// Inicio la pantalla pintando una linea
@SCREEN
M=-1

// Detecta si se esta presionando "d" o "i"
(LOOP)
@KBD
D=M
@100
D=D-A
@DERECHA
D;JEQ

@KBD
D=M
@105
D=D-A
@IZQUIERDA
D;JEQ
@LOOP
0;JMP

// Si se presiona "d" se moverá a la derecha
(DERECHA)
@i
A=M
M=0
A=A+1
M=-1
D=A
@i
M=D

@LOOP
0;JMP

// Si se presiona "i" se moverá a la izquierda
(IZQUIERDA)
@i
A=M
M=0
A=A-1
M=-1
D=A
@i
M=D

@LOOP
0;JMP

@FIN
(FIN)
0;JMP

Actividad 4
Actividad 5
Traducción de:
int a = 10;
int* p;
p = &a;
*p = 20;

<img width="1320" height="606" alt="image" src="https://github.com/user-attachments/assets/13144a83-a9a4-47d7-8bbd-948dad9c2024" />
Traducción de: 
int a = 10;
int b = 5;
int *p;
p = &a;
b = *p;

<img width="1484" height="711" alt="image" src="https://github.com/user-attachments/assets/27380512-8bd8-4289-90ca-da64180a8f8a" />
Actividad 6
-Implementa el programa anterior en lenguaje ensamblador aplicando el concepto de punteros.
-Considera que los datos del arreglo están almacenados desde la dirección 16. Inicializa el arreglo en lenguaje ensamblador.
-Simula paso a paso el programa en ensamblador. Recuerda la metodología: predice, ejecuta, observa y reflexiona.
-Construye tu programa PASO A PASO mediante pruebas. Indica qué característica vas a implementar con cada prueba y cómo la probaste.
-Muestra el programa final y cómo lo probaste.
Actividad 7

Actividad 8


## Bitácora de aplicación 



## Bitácora de reflexión



