### ¿Qué he aprendido?
# REACT
React es una libreria que permite construir interfaces de usuario dinámicos, tal y como la describe la propia documentación.

¿Cúeles son sus principales características?
 - Es declarativo, esto es, es un paradigma de programación (una forma de estructurar y escribir los elementos de un programa) que básicamente indica lo que debe hacer el programa y no cómo hacerlo. El ejemplo más evidente de lenguaje declarativo es SQL.
 - Esta basado en la creación de componentes que están encapsulados y manejan su propio estado.

¿Pero como funciona React?

En este gran [post](https://maggieappleton.com/reactpotato) de [Maggie Appleton](https://twitter.com/Mappletons) podemos ver a modo de metáforas visuales en que consiste React.

Es una librería que responde (reacciona) ante eventos del navegador, generalmente generados por el usuario, y modifica el interfaz del usuario pero unicamente aquellos nodos que necesitan ser modificados 

En React, todos los componentes expresan su UI dentro de las funciones de renderizado utilizando JSX, una sintaxis declarativa similar a XML que funciona dentro de JavaScript.



## Algunos conceptos interesantes
### 1. Inmutabilidad
 Inmutabilidad: Evitar la mutación directa de los datos nos permite mantener intactas las versiones anteriores de la historia del juego y reutilizarlas más adelante.
 
 El principal beneficio de la inmutabilidad es que ayuda a construir componentes puros en React. Los datos inmutables pueden determinar fácilmente si se han realizado cambios, lo que ayuda a determinar cuándo un componente requiere una nueva renderización.

 https://reactkungfu.com/2015/08/pros-and-cons-of-using-immutability-with-react-js/

 ### 2. Composition vs Inheritance
 React tiene un potente modelo de composición, y recomendamos utilizar la composición en lugar de la herencia para reutilizar el código entre los componentes.


### 3. User Interface
 La forma más fácil es construir una versión que tome tu modelo de datos y renderice la UI pero que no tenga interactividad. Es mejor desacoplar estos procesos porque la construcción de una versión estática requiere un montón de escribir y no pensar, y la adición de la interactividad requiere un montón de pensar y no un montón de escribir

 Manejar el estado de la aplicación / componentes esta reservado para cuando incluimos interoperabilidad

 suele ser más fácil ir de arriba a abajo, y en los proyectos más grandes, es más fácil ir de abajo a arriba y escribir pruebas a medida que se construye

### 4.Flujo de datos unidirecional 
 Si haces un cambio en tu modelo de datos subyacente y llamas a ReactDOM.render() de nuevo, la UI se actualizará. Puedes ver cómo se actualiza tu UI y dónde hacer los cambios. El flujo de datos unidireccional de React (también llamado one-way binding) mantiene todo modular y rápido.