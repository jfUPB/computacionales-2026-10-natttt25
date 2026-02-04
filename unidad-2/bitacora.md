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


## Bitácora de aplicación 



## Bitácora de reflexión

