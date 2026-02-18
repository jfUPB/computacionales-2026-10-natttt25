# Unidad 3

## Bitácora de proceso de aprendizaje
Actividad 1 
¿Para qué sirven los breakpoints?

Para detener la ejecucion del programa en una linea en especifico

¿Para qué se usa la ventana de depuración Autos?

Para mostrar las variables usadas en la ejecución

2

``` c++
#include <iostream>

using namespace std;

void swapPorValor(int a, int b)
{
    int c = b;
    b = a;
    a = c;

}
void swapPorReferencia(int& a, int& b)
{
    int c = b;
    b = a;
    a = c;
}
void swapPorPuntero(int* a, int* b)
{
    int c = *b;
    *b = *a;
    *a = c;
}
int main()
{
    int a = 10;
    int b = 30;
     
    swapPorPuntero(&a, &b);
    
    std::cout << "a: " << a << endl;
    std::cout << "b: " << b << endl;

    return 0;

}
```
## Bitácora de aplicación 



## Bitácora de reflexión

