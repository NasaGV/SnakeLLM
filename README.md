# Juego de la Serpiente con Estructura de Datos de Cola (Array)

Este repositorio contiene una implementación del clásico juego de la serpiente utilizando una estructura de datos de cola basada en un arreglo. A continuación, se explica cómo funciona el código y cómo se adaptó la lógica del juego para utilizar esta estructura.

## Estructura de Datos: Cola (Queue)

Una cola es una estructura de datos que sigue el principio FIFO (First In, First Out), es decir, el primer elemento en entrar es el primero en salir. En el contexto del juego de la serpiente:

- La cola representa el cuerpo de la serpiente.
- Cada elemento de la cola es un segmento de la serpiente, con coordenadas (x, y).
- Cuando la serpiente se mueve:
  - Se añade un nuevo segmento en la cabeza (front).
  - Se elimina el segmento más antiguo (la cola).

En esta implementación, se utiliza un arreglo para simular el comportamiento de una cola.

## Adaptación del Juego de la Serpiente

### 1. Representación de la Serpiente

La serpiente se representa como un arreglo de objetos, donde cada objeto contiene las coordenadas (x, y) de un segmento del cuerpo. Por ejemplo:

```javascript
let snake = [
    { x: 9 * box, y: 9 * box } // Cabeza de la serpiente
];
```

- El primer elemento del arreglo (`snake[0]`) es la cabeza de la serpiente.
- El último elemento del arreglo es la cola de la serpiente.

### 2. Movimiento de la Serpiente

El movimiento de la serpiente se maneja de la siguiente manera:

#### Añadir nueva cabeza

- Se calcula la nueva posición de la cabeza en función de la dirección actual (`LEFT`, `RIGHT`, `UP`, `DOWN`).
- Se añade esta nueva posición al inicio del arreglo usando `unshift`.

```javascript
const newHead = { x: snakeX, y: snakeY };
snake.unshift(newHead); // Añadir nueva cabeza
```

#### Eliminar la cola

- Si la serpiente no come comida, se elimina el último elemento del arreglo usando `pop`.

```javascript
snake.pop(); // Eliminar la cola
```

### 3. Comida y Crecimiento de la Serpiente

Cuando la serpiente come la comida:

- Se genera una nueva posición aleatoria para la comida.
- No se elimina la cola de la serpiente, lo que hace que la serpiente crezca.

```javascript
if (snakeX === food.x && snakeY === food.y) {
    food = {
        x: Math.floor(Math.random() * 20) * box,
        y: Math.floor(Math.random() * 20) * box
    };
} else {
    snake.pop(); // Solo eliminar la cola si no se come la comida
}
```

### 4. Detección de Colisiones

Se verifica si la cabeza de la serpiente choca con los límites del canvas o con su propio cuerpo:

```javascript
function collision(head, array) {
    for (let i = 0; i < array.length; i++) {
        if (head.x === array[i].x && head.y === array[i].y) {
            return true;
        }
    }
    return false;
}
```

Si hay una colisión, el juego termina.

## Código Principal

El código principal del juego se divide en las siguientes partes:

### 1. Inicialización

- Se crea el arreglo `snake` con la posición inicial de la serpiente.
- Se genera la posición inicial de la comida.

### 2. Control de Dirección

- Se actualiza la dirección de la serpiente en función de las teclas presionadas.

### 3. Función `draw`

- Se encarga de dibujar la serpiente y la comida en el `canvas`.
- Actualiza la posición de la serpiente y verifica colisiones.

### 4. Bucle del Juego

- Se utiliza `setInterval` para llamar a la función `draw` cada 100 ms.

