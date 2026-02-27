Nota del profesor: no hay evidencia de la fase de la aplicación.

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
``` c++
Apply
#include <iostream>
#include <string>

class Personaje {
public:
    std::string nombre;
    int* estadisticas;

    Personaje(std::string n, int vida, int ataque, int defensa) {
        nombre = n;
        estadisticas = new int[3];
        estadisticas[0] = vida;
        estadisticas[1] = ataque;
        estadisticas[2] = defensa;
        std::cout << "Constructor: nace " << nombre << std::endl;
    }

    void imprimir() {
        std::cout << "Personaje " << nombre
            << " [Vida: " << estadisticas[0]
            << ", ATK: " << estadisticas[1]
            << ", DEF: " << estadisticas[2]
            << "]" << std::endl;
    }
};

void simularEncuentro() {
    std::cout << "\n--- Iniciando encuentro ---" << std::endl;
    Personaje heroe("Aragorn", 100, 20, 15);

    Personaje copiaHeroe = heroe;
    copiaHeroe.nombre = "Copia de Aragorn";

    std::cout << "Saliendo del encuentro..." << std::endl;
}

int main() {
    simularEncuentro();
    std::cout << "\nSimulación terminada." << std::endl;
    return 0;
}
```
Error crítico 1. Cuando se intenta hacer la copia del objeto heroe. Solo se esta copiando la dirección de memoria del puntero, entonces ambos objetos apuntan al mismo espacio de memoria de estadisticas. Es un problema crítico porque heroe y copiaHeroe estan compartiendo estadisticas, no tienen estadisticas propias, cualquier cambio que se haga en las estadisticas de un objeto tambien afecta al otro, puede causar comportamientos raros o inesperados en el programa. 

Error crítico 2. La fuga de memoria es provocada por el arreglo "new int[3]" ya que la memoria que se crea con el "new" no se devuelve al sistema, entonces queda ocupada aunque el objeto ya no exista, esto causa la fuga de memoria y el consumo creciente de RAM. Habria que dejar de usar la memoria en el heap y usar un arreglo que se guarde automáticamente en el stack o memoria automática.

Cambiar: 
```c++
int estadisticas[3];   // ← arreglo normal (usa stack)
```
Es mejor usar el stack porque la memoria se administra automáticamente. No es necesario usar new ni delete, por lo que se evita el riesgo de fugas de memoria. Además, cada objeto tiene su propia copia de las estadísticas, lo que evita que varios objetos compartan la misma dirección de memoria. Esto hace que el programa sea más seguro y estable.


## Bitácora de aplicación 



## Bitácora de reflexión



