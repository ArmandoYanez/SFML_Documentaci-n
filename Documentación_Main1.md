<h1 style="text-align: center; color: mediumvioletred">EJERCICIO SFML _ MAIN 1</h1>
<h4 style="text-align: center; color: white">ARMANDO LEONEL YAÑEZ AREVALO | PROGRAMACION 2</h4>

<div style="text-align: justify;">
En este primer programa, lo que se muestra en la pantalla al ejecutarlo es una pantalla negra con 
una figura dentro de ella. Para esto, se utilizó el siguiente código, el cual será explicado parte por parte.

Lo primero que se debe hacer es incluir la librería SFML y, específicamente, el paquete "Graphics". Este paquete 
incluye funciones con gráficos que podremos usar, como la creación de pantallas.
</div>

```c++
//Se incluye la libreria
#include <SFML/Graphics.hpp>

int main() {
    
    //Creación de la ventana.
sf::RenderWindow window(sf::VideoMode(800, 600), "SFML Window");
```
<div style="text-align: justify;">

Aquí tienes el texto corregido con los errores ortográficos resueltos:

En esta última línea creamos la ventana. Para esto, es importante especificar 
de dónde viene esa variable que queremos utilizar. Por esa razón, se utiliza sf::RenderWindow. 
Esta clase hereda de dos clases, las cuales son Window y RenderTarget. Esto significa que RenderWindow 
nos permitirá la configuración de la ventana y de lo que hay dentro de ella.

Después tenemos sf::VideoMode, esta clase define el modo video de una ventana. Para esta parte, también
se tendrán que rellenar los paréntesis con dos parámetros, los cuales son el ancho y el alto de la pantalla, en 
este caso, 800 y 600 píxeles.

Ahora tenemos el siguiente bloque de código:
</div>

```c++
//Creamos rectangulo.
sf::RectangleShape rectangle(sf::Vector2f(128, 128));

//Le damos un color al rectangulo.
rectangle.setFillColor(sf::Color::Red);

//Lo posicionamos.
rectangle.setPosition(100, 100);

//En esta ultima linea creamos otro rectangulo con unas medidas diferntes.
sf::RectangleShape rectangle2(sf::Vector2f(128, 128));
```
<div style="text-align: justify;">
En estas líneas anteriores es muy fácil saber qué es lo que hace, ya que
simplemente leyendo se puede deducir. Primero, se crea un rectángulo; para
esto se utiliza directamente la clase RectangleShape, la nombramos (en nuestro
caso, rectangle) y le damos sus dimensiones.

Después, la siguiente línea se encarga de darle color. Esto se hace con un método 
llamado setFillColor, al cual le tendremos que especificar el color. Esto se puede
hacer utilizando las palabras reservadas de cada color o utilizando un código hexadecimal.

Por último, la penúltima línea posiciona el rectángulo en la posición 100, 100. Esto se maneja con coordenadas.

La última línea simplemente crea otro rectángulo, pero ahora llamado rectangle2.
</div>


```c++
// Loop para mantener la pantalla abierta.
    while (window.isOpen()) {
        sf::Event event;
        // Se crea una variable tipo evento.
        // Se crea loop que para hasta que no haya más eventos por procesar. 
        while (window.pollEvent(event)) {
            // En caso de precionar exit la ventana se cerrara.
            if (event.type == sf::Event::Closed) {
                window.close();
            }
        }
```
<div style="text-align: justify;">
Aquí tienes el texto corregido con los errores ortográficos resueltos:

Este último bloque de código es el bucle que permite que la pantalla exista
hasta que se cierre.

La primera línea es un ciclo while que comprueba si la ventana está abierta. 
Para esto se utiliza window.isOpen(), que retorna un booleano. Si es verdadero, 
el while seguirá ejecutándose.

Dentro del while, se declara una variable de tipo evento que nos ayudará a almacenar
un evento. Luego se crea otro ciclo while con el objetivo de verificar eventos disponibles 
para procesar. En caso de que no haya eventos, devolverá false (un evento podría ser que el 
usuario presione el botón de cerrar ventana).

Dentro del segundo while, hay un if que se encarga de comprobar si el evento 
recibido es de tipo Closed. Esto significa que verifica si se solicitó cerrar 
la ventana. En caso de que coincida, se utiliza window.close() para cerrar la pantalla. 
En caso contrario, el código continuará con las siguientes instrucciones:
</div>

```c++
        // La pantalla se limpia con el color negro
        window.clear(sf::Color::Black);

        // La pantalla imprime el rectangulo.
        window.draw(rectangle);

        // Se actualiza el contenido.
        window.display();
    }

    return 0;
}
```

<div style="text-align: justify;">
En este bloque de código, la instrucción prácticamente limpia la pantalla con 
el color negro en este caso. Luego se utiliza el método .draw para dibujar nuevamente
el rectángulo en la pantalla y, por último, se utiliza window.display(). Esto se hace 
con el objetivo de actualizar los nuevos datos que la pantalla debe mostrar.

Este proceso se realiza dentro del bucle con la finalidad de que no desaparezca lo que 
se está estableciendo desde el inicio. Prácticamente provoca que esta pantalla y su contenido
no se eliminen, por lo cual esta parte final es sumamente importante.

Para terminar, usamos return 0 para indicar el final del programa.


</div>
