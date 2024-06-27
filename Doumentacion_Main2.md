<h1 style="text-align: center; color: mediumvioletred">EJERCICIO SFML _ MAIN 2</h1>
<h4 style="text-align: center; color: white">ARMANDO LEONEL YAÑEZ AREVALO | PROGRAMACION 2</h4>

<div style="text-align: justify;">
Este programa lo que hace es ejecutarse y crear una ventana con la bandera LGBT+. 
Para lograr esto se utilizó el siguiente código, y se explicará paso a paso todos 
los pasos que recorre el código.

En las primeras líneas de código podemos ver las librerías que se están utilizando.
En este caso, se están empleando tres diferentes: la librería <SFML/Graphics.hpp>, 
la cual se encarga del funcionamiento de las pantallas y la personalización de las mismas,
<iostream>, que permite la entrada y salida de datos; y por último, la librería <sstream>,
la cual tiene capacidades para manipular cadenas de texto.
</div>

```c++
//Librerias que se utilizaran.
#include <SFML/Graphics.hpp>
#include <iostream>
#include <sstream>
```
<div style="text-align: justify;">
Ahora, en lugar de ir directamente al main, crearemos 1 funcion. Esta se explicarán a continuación:
</div>

```c++
// Función de conversion de hexadecimal a sf::Color
sf::Color hexToColor(const std::string& hex) {
    // valida si la cadena comienza con '#'
    if (hex[0] != '#') {
        throw std::invalid_argument("Hex color must start with #");
    }

    // Crear cadena nueva sin el primer #.
    std::string hexColor = hex.substr(1);
    std::stringstream ss;
    ss << std::hex << hexColor;
```

<div style="text-align: justify;">
Esta función devuelve un objeto de tipo sf::Color y requiere una cadena de caracteres para 
poder funcionar. Lo primero que hace es validar si la cadena que entra contiene al inicio un 
#, para así comprobar si efectivamente es un código de color hexadecimal.

Después, lo que se hace en esta parte del código es crear una copia de la cadena pero sin el #,
eliminándolo de la misma. Despues tenemos este bloque:

</div>

```c++
// Lee y almacena el valor del color en un numero sin signo.
uint32_t color;
ss >> color;

// Comprueba que el color es valido en base a su alpha  y las longitude de cada valor.
if (hexColor.length() == 6) {
return sf::Color((color >> 16) & 0xFF, (color >> 8) & 0xFF, color & 0xFF);
} else if (hexColor.length() == 8) {
return sf::Color((color >> 24) & 0xFF, (color >> 16) & 0xFF, (color >> 8) & 0xFF, color & 0xFF);
} else {
throw std::invalid_argument("Hex color must be 7 or 9 characters long, including #");
}
```
<div style="text-align: justify;">
Las 2 primeras lineas son las encargadas de crear una variable para guardar un numero sin signos para
posteriormente gaurdar el valor de la cadena en esa nueva variable.

Posterioirmente llega a una zona de comparaciones, donde el codigo numerico del color se verifica tomando
en cuneta que si tiene 6 caracteres, extrae y devuelve los componentes rojo, verde y azul o en otro caso
si tiene 8 caracteres, también extrae y devuelve el componente alfa.

Si este se encunetra devuelve el color y en caso contrario lanza un mensaje de error.

Ahora si inicia el main como tal, en esta parte se hara funcionar la ventana y se integraran las
respectivas figuras.
</div>

```c++
int main() {
    // Crear ventana
    sf::RenderWindow window(sf::VideoMode(800, 600), "Pride Flag");

    // Definir los colores de la bandera.
    std::vector<sf::Color> colors = {
            hexToColor("#FF0000"), // Red
            hexToColor("#FF8C00"), // Orange
            hexToColor("#FFFF00"), // Yellow
            hexToColor("#008000"), // Green
            hexToColor("#0000FF"), // Blue
            hexToColor("#8B00FF")  // Purple
    };
```
<div style="text-align: justify;">
En este primer bloque del código main, es fácil entender lo que se hace. La primera línea crea 
un objeto de tipo RenderWindow y complementa sus parámetros con el VideoMode para asignarle un tamaño 
y una cadena de caracteres con la cual se nombra la ventana (este nombre se encuentra en la esquina superior 
izquierda de la ventana).

Después, tenemos un vector que se rellena de objetos de tipo Color. Estos son rellenados con los distintos códigos
de color de la bandera.

Después tenemos lo siguiente:
</div>

```c++
 // Creamos rectangulo por cada franja.
std::vector<sf::RectangleShape> stripes;
float stripeHeight = window.getSize().y / colors.size();

for (size_t i = 0; i < colors.size(); ++i) {
sf::RectangleShape stripe(sf::Vector2f(window.getSize().x, stripeHeight));
stripe.setFillColor(colors[i]);
stripe.setPosition(0, i * stripeHeight);
stripes.push_back(stripe);
}
```
<div style="text-align: justify;">
En la primera línea creamos un vector donde guardaremos cada franja.

La segunda línea calcula el tamaño total de la pantalla y, con base en ese tamaño, se determina cuánto debe 
medir cada franja. Esto se hace con una simple división, ya que se conoce la cantidad de colores que tendrá.

Después, se utiliza un bucle for para configurar cada una de estas franjas para su aparición. Primero se crea,
luego se le da color, después se posiciona y finalmente se agrega al vector.

Por ultimo tenemos el main loop, este funciona practicamente igual que el del main 1, pero
con una variación la cuál explicare más adelante.
</div>

```c++
 // Loop principal
while (window.isOpen()) {
    sf::Event event;
    while (window.pollEvent(event)) {
    if (event.type == sf::Event::Closed) {
    window.close();
        }
    }
    window.clear(sf::Color::Black);

    // Se imprimen las figuras
    for (const auto& stripe : stripes) {
    window.draw(stripe);
    }

    window.display();
}

return 0;
}
```
<div style="text-align: justify;">
Primero que nada, tenemos el primer bucle, el cual, en caso de que se detecte que la ventana está abierta, 
no dejará de repetirse. Dentro de este bucle, creamos un objeto de tipo Evento y, posteriormente, otro bucle
que comprueba si entró algún evento o no.

En caso de que algún evento haya entrado, habrá una comparación para saber si el evento que entró es el de close y, 
en caso de ser verdadero, se usará el método window.close para cerrar la ventana. En caso contrario, continuará.

Si continúa, nos daremos cuenta de que se limpiará la pantalla, se volverán a imprimir las figuras con ayuda de un for y, 
después, se actualizará la pantalla gracias al window.display. Si nos damos cuenta, es un proceso prácticamente
idéntico al del main 1, pero este tiene la diferencia de que se le debe dar tratamiento a muchas figuras a la vez y no solo a una.
</div>
