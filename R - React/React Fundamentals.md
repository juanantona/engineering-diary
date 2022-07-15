# Docs
- #### [React Beta Documentation](https://beta.reactjs.org/)
- #### [Getting to Know… React](https://aarontgrogg.com/blog/2022/01/06/getting-to-know-react/)


# Props vs state
 #### [Props vs state](https://github.com/uberVU/react-guide/blob/master/props-vs-state.md)
 
 Se podría decir que props + state son los datos de entrada para la función render() de un Componente

Antes de separar los props y el estado, identifiquemos también dónde se solapan.

- Tanto los props como el estado son objetos JS simples
- Tanto los cambios de props como los de estado provocan una actualización de la renderización
- Tanto las props como el estado son deterministas. Si tu Componente genera diferentes salidas para la misma combinación de props y state, entonces estás haciendo algo mal.


Si un Componente necesita alterar uno de sus atributos en algún momento, ese atributo debe ser parte de su estado, de lo contrario debe ser sólo un prop para ese Componente.

Un Componente no puede cambiar sus props, pero es responsable de juntar los props de sus Componentes hijos.

El estado es opcional. Dado que el estado aumenta la complejidad y reduce la previsibilidad, es preferible un componente sin estado. Aunque está claro que no puedes prescindir del estado en una aplicación interactiva, deberías evitar tener demasiados componentes con estado.

# [Hooks](https://medium.com/@dan_abramov/making-sense-of-react-hooks-fdbde8803889)
Por qué hooks? porque con clases era imposible extraer el manejp del estado de un componente para fuse reusable por otros componentes

Los hooks son funciones que permiten "hook into" el estado de React y las características del ciclo de vida de los componentes de la función

- Es difícil reutilizar la lógica de estado entre componentes

Los hooks son metodos de una API que permite acceder a partes internas de React

Con los Hooks, se puede extraer la lógica de estado de un componente para que pueda ser probado de forma independiente y reutilizado.

Los Hooks proporcionan acceso a escotillas de escape imperativas y no requieren que se aprendan complejas técnicas de programación funcional o reactiva.

Los Hooks se diseñaron pensando en el tipado estática. Como son funciones, son más fáciles de escribir correctamente que los patrones como los componentes de orden superior

### useEffect
#### [A Complete Guide to useEffect by Dan Abramov](https://overreacted.io/a-complete-guide-to-useeffect/)

lo más potente de useEffect es que te permite agrupar la logica en differentes useEffects de tal forma que no este mezclada dentro de los mismos métodos de manejo del ciclo de vida en componentes basados en clases. Esto ayuda a evitar bugs e inconsistencias

En muchos casos no es posible dividir estos componentes en otros más pequeños porque la lógica de estado está por todas partes. También es difícil probarlos. Esta es una de las razones por las que mucha gente prefiere combinar React con una librería de gestión de estados independiente

También puede optar por gestionar el estado local del componente con un reductor para hacerlo más predecible.

Las clases también presentan problemas para las herramientas actuales. Por ejemplo, las clases no se minifican muy bien, y hacen que la recarga en caliente sea escasa y poco fiable. Queremos presentar una API que haga más probable que el código se mantenga en el camino de la optimización.

### UseState
Post de Kent C. Dodds donde se recomienda restringir el numero de variables de estado haciendo que las otras dependan de ellas: [Don't Sync State. Derive It!](https://kentcdodds.com/blog/dont-sync-state-derive-it)

Better Avoid Props In Initial State

useState hook initializes the state only once - when the component is rendered and is not able to capture further changes in the initialValue prop.

### useRef
https://opinionatedreact.com/useRef.pdf

# Data Fetching
 React issuse discussion where Dan abramov: https://github.com/facebook/react/issues/14326

#### [How to fetch data with React Hooks](https://www.robinwieruch.de/react-hooks-fetch-data/)


### React Server Components
https://reactjs.org/blog/2020/12/21/data-fetching-with-react-server-components.html




### Code splitting 
La mejor manera de introducir división de código en tu aplicación es a través de la sintaxis de `import()` dinámico.
