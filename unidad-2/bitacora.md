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

Implementa ambos programas en lenguaje ensamblador.
Capturas de pantalla donde muestres una parte de la simulación y expliques qué se ve en esas capturas.
Captura de pantalla del simulador mostrando el resultado final correcto.

Primer programa:
#include <iostream>

void swap(int* pa, int* pb){
    int tmp = *pa;
    *pa = *pb;
    *pb = tmp;
}

int main()
{
    int a = 10;
    int b = 20;
    std::cout<<"a: " << a <<" b: "<< b<< std::endl;
    swap(&a,&b);
    std::cout<<"a: " << a <<" b: "<< b<< std::endl;
    return 0;
}

En este problema intercambiamos valores a través de punteros, tenemos las variables a y b

En lenguaje ensamblador:
@10
D=A
@16
M=D    // RAM[16] = VARIABLE a = 10

@20
D=A
@17
M=D    // RAM[17] = VARIABLE b = 20

@16
D=A
@R0
M=D    

@17
D=A
@R1
M=D



@retornoDespuesCambio
D=A
@R15
M=D

@swap
0;JMP


(retornoDespuesCambio)
@END
0;JMP

(END)
0;JMP

(swap)
    
@R0
A=M
D=M
@13
M=D

@R1
A=M
D=M
@R0
A=M
M=D

@13
D=M
@R1
A=M
M=D

@15
A=M
0;JMP

<img width="615" height="244" alt="image" src="https://github.com/user-attachments/assets/9cf812e4-07e5-4754-870e-1f16ae440569" />
Iniciamos con las variables a y b
<img width="357" height="251" alt="image" src="https://github.com/user-attachments/assets/f5917135-b8d7-441a-952c-101f49b0d785" />
Guardamos las direcciones de los punteros en 16 y 17 
<img width="849" height="810" alt="image" src="https://github.com/user-attachments/assets/6eee380d-6655-4224-84d9-3d1760d5d192" />
Vamos a la funcion de cambio, guardamos los valores de a y b temporalmente en otra direccion para luego hacer el cambio y poner el valor de b en a y el de a en b.
<img width="236" height="159" alt="image" src="https://github.com/user-attachments/assets/d37ab7d9-9c59-46d6-9b69-4cc3242883e9" />
Podemos observar como en la direccion 16 y 17 guardamos los valores de a y b, es decir, los valores de 10 y 20
<img width="1065" height="447" alt="image" src="https://github.com/user-attachments/assets/f195aa71-783d-4ec9-9afa-8be8746f8d53" />

<img width="1183" height="680" alt="image" src="https://github.com/user-attachments/assets/9e0986b2-936b-4d2a-8f43-90e668fe0640" />

<img width="679" height="417" alt="image" src="https://github.com/user-attachments/assets/1c2637ea-bc6e-4082-b07a-ec5022ed0508" />
Finalizamos guardando los valores de a y b temporalmente en otras direcciones y luego se hace el cambio, a queda como 20 y b como 10

Segundo programa:

#include <iostream>

int calSum(int* parr,int arrSize){
    int sum = 0;
    for(int i= 0; i < arrSize;i++){
        sum = sum + *(parr+i);
    }
    return sum;
}

int main()
{
    int arr[] = {10,15,2,3,50};
    int sum = calSum(arr,5);
    std::cout<<"Sum: " << sum << std::endl;
    return 0;
}
Aqui analizamos un arreglo usando los punteros











## Bitácora de aplicación 



## Bitácora de reflexión






