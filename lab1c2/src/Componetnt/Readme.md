# Laboratorio 1 - Segundo Cómputo
**Asignatura:** Programación Computacional IV
**Integrantes:** Pareja por afinidad

## 1. Situación Problemática
**Enunciado:** Actualmente, muchas microempresas del sector comercio (como pequeñas panaderías o tiendas de abarrotes) registran sus ventas diarias de forma manual en libretas de papel. Esto genera errores de cálculo, pérdida de información y dificultad para conocer el total de ingresos al final del día.

**Sector Enfocado:** Microempresas y Emprendedores del sector comercio minorista.

**Resolución del Problema:** La aplicación desarrollada con Vue.js permitirá a los dueños de negocios registrar cada venta ingresando el nombre del producto, su precio y categoría. El sistema validará que los datos sean correctos, mostrará una lista dinámica de las ventas realizadas y calculará automáticamente el total acumulado, eliminando la necesidad de cálculos manuales y reduciendo el margen de error.

---

## 7. Preguntas de Reflexión

*   **¿Qué es Vue.js y cuál es su función dentro de la página web desarrollada?**
    Vue.js es un framework progresivo de JavaScript utilizado para construir interfaces de usuario. Su función en este proyecto es gestionar la "reactividad" de la página, permitiendo que la interfaz se actualice automáticamente cada vez que el usuario agrega o elimina una venta sin necesidad de recargar el navegador.

*   **Describa qué variables reactivas utilizó en su aplicación y cuál es la función de cada una.**
    1. `ventas`: Un arreglo que almacena todos los objetos de ventas realizados.
    2. `nuevoNombre`: Almacena temporalmente el nombre del producto ingresado en el input.
    3. `nuevoPrecio`: Almacena el valor numérico del precio del producto.
    4. `nuevaCategoria`: Guarda la categoría seleccionada para el producto.
    5. `mostrarMensaje`: Un booleano que controla la visibilidad de una alerta de éxito tras registrar una venta.

*   **Explique la diferencia entre las directivas v-bind y v-model.**
    - `v-bind`: Se utiliza para enlazar una propiedad de los datos hacia un atributo de una etiqueta HTML (enlace unidireccional). Por ejemplo, para cambiar dinámicamente el color de un texto.
    - `v-model`: Crea un enlace bidireccional (two-way binding) entre un elemento de entrada (input, select) y una variable de Vue. Si el usuario escribe en el input, la variable cambia; si la variable cambia por código, el input se actualiza.

*   **Mencione al menos un ejemplo de evento utilizado dentro de su aplicación.**
    Se utilizó el evento `@click` en el botón de "Registrar Venta" para disparar la función `agregarVenta()`, y el evento `@click` en los botones de "Eliminar" para quitar registros específicos.

*   **¿Para qué utilizó la directiva v-for dentro de su aplicación?**
    Se utilizó para recorrer el arreglo `ventas` y generar dinámicamente una fila en la tabla (etiqueta `<tr>`) por cada registro almacenado, mostrando los detalles de cada venta de forma automática.

*   **Describa en qué situación utilizó v-if y qué problema resuelve dentro de su interfaz.**
    Se utilizó `v-if` para mostrar un mensaje de "No hay ventas registradas" cuando el arreglo está vacío. Esto resuelve el problema estético de mostrar una tabla vacía o confusa, mejorando la experiencia del usuario (UX).

*   **Explique cómo se realiza la validación de datos en su aplicación y por qué es importante.**
    La validación se realiza mediante una estructura `if` dentro de la función `agregarVenta`, verificando que el nombre no esté vacío y que el precio sea mayor a cero. Es importante porque evita que se procesen cálculos con datos erróneos o nulos que podrían corromper la información financiera del negocio.
