Este código JavaScript está diseñado para implementar una funcionalidad de arrastrar y soltar (drag and drop) en elementos del DOM, específicamente en elementos `article`. La funcionalidad permite al usuario "deslizar" una tarjeta (representada por un elemento `article`) hacia la derecha o hacia la izquierda con el mouse o con el dedo en dispositivos táctiles, emulando una interacción común en aplicaciones de citas o de decisión. Aquí está el desglose de lo que hace el código:

1. **Variables Iniciales:**
   - `DECISION_THRESHOLD`: Un umbral (75px en este caso) que determina cuánta distancia debe ser arrastrada la tarjeta para considerar que se ha tomado una decisión (me gusta o no me gusta).
   - `isAnimating`: Un indicador de si la tarjeta está siendo animada.
   - `pullDeltaX`: La distancia horizontal que la tarjeta ha sido arrastrada.

2. **Función `startDrag(event)`:** Se activa al iniciar el arrastre. Verifica si ya hay una animación en curso o si el evento no se originó en un elemento `article` para salir temprano si es necesario. Calcula la posición inicial del arrastre basándose en el evento de mouse o táctil.

3. **Eventos de Movimiento (`onMove`) y Fin de Arrastre (`onEnd`):**
   - **`onMove`:** Se llama mientras el usuario arrastra la tarjeta. Calcula la distancia arrastrada (`pullDeltaX`), aplica una transformación al elemento `article` para moverlo y rotarlo basándose en esta distancia, y modifica la opacidad de algún elemento de "elección" (`like` o `nope`) dentro de la tarjeta para indicar la dirección del deslizamiento.
   - **`onEnd`:** Se llama cuando el usuario suelta la tarjeta. Elimina los manejadores de eventos para evitar llamadas redundantes. Decide si se ha realizado una acción suficiente para considerar que se ha tomado una decisión (basado en `DECISION_THRESHOLD`) y, en ese caso, anima la tarjeta fuera de la pantalla y luego la elimina. Si no se ha alcanzado el umbral, la tarjeta se restablece a su posición original.

4. **Suscripción a Eventos de Inicio de Arrastre:** El documento escucha los eventos `mousedown` y `touchstart` para iniciar el proceso de arrastre, llamando a `startDrag` cuando estos eventos ocurren.

El código hace uso de varias técnicas importantes en el desarrollo web moderno, como la manipulación de eventos, transformaciones CSS para movimiento y rotación, y la gestión de la interacción táctil versus el uso del mouse. Esta implementación proporciona una experiencia de usuario interactiva y atractiva, común en interfaces donde la decisión rápida (como deslizar hacia la derecha o izquierda para indicar preferencia) es una parte central de la navegación o el flujo de trabajo de la aplicación.


### Revisar

Esto NO funciona

```css
            & .go-left {
                transform: translateX(-100%) rotate(-20deg) !important;
                transition: transform .3s ease, rotate .3s ease;
                
            }

            & .go-right{
                transform: translateX(100%) rotate(20deg) !important;
                transition: transform .3s ease, rotate .3s ease;
            }

            & .reset{
                transform: translateX(0) !important;
                transition: transform .3s ease;
                
            }
```

Esto SI funciona

```css
      &.go-left {
        transform: translateX(-150%) rotate(-30deg) !important;
      }

      &.go-right {
        transform: translateX(150%) rotate(30deg) !important;
      }

      &.go-left,
      &.go-right {
        transition: transform .3s ease, rotate .3s ease;
      }

      &.reset {
        transition: transform .3s ease;
        transform: translateX(0) !important;
      }
```

El problema es el espacio entre el & y el punto