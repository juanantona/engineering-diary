TAGS: #react 
TITLE: What Is Reactivity?
URL: https://www.pzuraq.com/blog/what-is-reactivity
AUTHOR: Kristen
___

Ember Octane ha llegado junto con una gran cantidad de nuevas características, pero ninguna de estas características me emociona más personalmente que el autoseguimiento. El autoseguimiento es el nuevo sistema de reactividad de Ember, que es lo que permite a Ember saber cuándo han cambiado los valores de estado (como las propiedades @tracked). Esta fue una actualización masiva bajo el capó e implicó reescribir completamente algunas de las abstracciones más antiguas de Ember sobre esta nueva base.

El autoseguimiento es, a primera vista, muy similar al modelo de reactividad de Ember Classic (basado en propiedades computadas, observadores y Ember.set()). Si comparas los dos lado a lado, la diferencia principal parece ser dónde se colocan las anotaciones. En Octane, decoras las propiedades en las que dependes, mientras que en Classic decoras los getters y setters.

```javascript
class OctaneGreeter {
  @tracked name = 'Liz';

  get greeting() {
    return `Hola, ${this.name}!`;
  }
}

class ClassicGreeter {
  name = 'Liz';

  @computed('name')
  get greeting() {
    return `Hola, ${this.name}!`;
  }
}
```

Pero si profundizas, descubrirás que el autoseguimiento es bastante más flexible y poderoso. Por ejemplo, puedes autoseguir los resultados de funciones, algo que era imposible en Ember Classic. Toma este modelo para un juego de video 2D simple, por ejemplo:

```javascript
class Tile {
  @tracked type;

  constructor(type) {
    this.type = type;
  }
}

class Character {
  @tracked x = 0;
  @tracked y = 0;
}

class WorldMap {
  @tracked character = new Character();

  tiles = [
    [new Tile('colinas'), new Tile('playa'), new Tile('océano')],
    [new Tile('colinas'), new Tile('playa'), new Tile('océano')],
    [new Tile('playa'), new Tile('océano'), new Tile('arrecife')]
  ];

  getType(x, y) {
    return this.tiles[x][y].type;
  }

  get isSwimming() {
    let { x, y } = this.character;

    return this.getType(x, y) === 'océano';
  }
}
```

Podemos ver que el getter isSwimming se actualizaría cada vez que el personaje cambiara de posición (coordenadas x/y). Pero también se actualizaría cada vez que se actualizara la ficha que getType devuelve, manteniendo así el sistema sincronizado. Este tipo de dinamismo surgía de vez en cuando al trabajar con propiedades computadas, sin grandes soluciones. Por lo general, requería agregar muchos valores intermedios para calcular el estado derivado.

La cuestión es que el autoseguimiento es bastante diferente al de Ember Classic. ¡Esto es genial y emocionante! Pero también es un poco confuso, porque muchos de los patrones que los desarrolladores de Ember han aprendido a lo largo de los años no funcionan tan bien en Octane.

Por eso he decidido comenzar una nueva serie de entradas en el blog sobre el autoseguimiento, discutiendo el diseño detrás del autoseguimiento como sistema. Esta serie mostrará cómo usar el autoseguimiento de diferentes maneras para una variedad de casos de uso. Debo decir desde el principio que estas entradas no pretenden ser exhaustivas. El objetivo es establecer el modelo mental de cómo funciona el autoseguimiento bajo el capó y cómo construir patrones y bibliotecas que funcionen con él.

Hasta ahora tengo planeadas 7 entradas. Las primeras serán entradas introductorias que discutirán el "panorama general", y el resto serán estudios de casos que tratarán los detalles más específicos:

¿Qué es la Reactividad? ← Esta entrada
¿Qué hace un Buen Sistema Reactivo?
Cómo Funciona el Autoseguimiento
A medida que avancemos, espero agregar más estudios de casos para casos interesantes o difíciles que los nuevos usuarios de Octane encuentren. Entonces, si hay algo que te gustaría que analizara como parte de esta serie, ¡házmelo saber! Puedes contactarme por correo electrónico o en Discord.

Ahora bien, vamos a nuestro primer tema: ¿Qué es la "reactividad"?

Reactividad en Español Sencillo
La reactividad o "programación reactiva" es una de esas palabras de moda que se ha mencionado mucho en la última década más o menos. Se ha aplicado a muchos contextos diferentes y es un concepto muy amplio, por lo que puede ser difícil intentar destilar exactamente lo que significa. Pero, voy a intentarlo 😄

>Reactividad: Un modelo de programación declarativo para actualizaciones basadas en cambios de estado.

Ten en cuenta que estoy definiendo el término "reactividad" directamente, en lugar de "programación reactiva" o "modelo de reactividad". En la conversación común, encuentro que tendemos a referirnos a "la reactividad de Ember" o "la reactividad de Vue", por lo que creo que tiene sentido como sustantivo en sí mismo en el contexto de la programación. Al final, todos estos términos significan básicamente lo mismo.

¡Así que tenemos una definición que encaja en una frase! Hasta ahora todo bien, creo que estamos superando a Wikipedia aquí.

Entrada de Wikipedia sobre Programación Reactiva

Pero ahora tenemos otros dos términos en los que se basa nuestra definición y que posiblemente sean igualmente confusos para muchos: "declarativo" y "estado". ¿Qué queremos decir con "programación declarativa" y cómo difiere de otros estilos como la programación "imperativa" y "funcional"? ¿Y qué es exactamente "estado"? Hablamos mucho de ello en el mundo de la programación, pero puede ser difícil encontrar una definición sencilla, así que vamos a profundizar en ello.

Estado
"Estado" es en muchos aspectos un término elegante para "variables". Cuando nos referimos al estado del programa, nos referimos a cualquiera de los valores que pueden cambiar dentro de él; es decir, cualquier valor que no sea estático. En JavaScript, el estado existe como:

Variables declaradas con let y const
Propiedades en objetos
Valores dentro de matrices u otras colecciones, como mapas y conjuntos
Estas son formas de lo que llamaré estado raíz, lo que significa que representan valores reales y concretos en el sistema. Por el contrario, también hay estado derivado, que es el estado que se produce combinando el estado raíz. Por ejemplo:

```javascript
let a = 1;
let b = 2;

function aMasB() {
  return a + b;
}
```

En este ejemplo, aMasB() devuelve un nuevo valor que se deriva del valor de a y b. Llamar a la función no introduce ninguna variable local o valores, por lo que no tiene su propio estado raíz. Esta es una distinción importante, porque significa que si conocemos el valor de a y el valor de b, entonces también conocemos el valor de aMasB(). También sabemos que si a o b cambia, entonces aMasB() también cambiará, lo cual es crucial para construir un sistema reactivo.

Programación Declarativa
Tal vez hayas escuchado los términos "imperativo", "declarativo" y "funcional" lanzados antes al hablar sobre varios estilos de programación, pero puede ser difícil saber exactamente cuál es la diferencia entre ellos. Fundamentalmente, se reduce a esta distinción:

En la programación declarativa, el programador describe lo que quiere que suceda, sin preocuparse por los detalles de cómo se hace.

En la programación imperativa, el programador describe los pasos exactos de cómo se debe hacer algo.

"Imperativo" significa dar una orden, y en la programación imperativa, la aplicación se ejecuta como una serie de pasos (órdenes). Esta es una definición muy amplia y no ayuda mucho; ¿no son la mayoría de los programas una "serie de pasos"? Donde importa, sin embargo, es lo que implica sobre el estado imperativamente derivado, específicamente que no es realmente estado derivado (al menos, según se define en la sección anterior).

Echemos un vistazo al primer ejemplo nuevamente y derivemos el valor de aMasB de manera imperativa. En lugar de definir una función que se pueda llamar para obtener el valor en cualquier momento, en su lugar derivaremos el valor manualmente en unos pocos pasos:

```javascript
let a = 1;
let b = 2;

let aMasB = a + b;
```

Al principio, este ejemplo puede parecer mucho más simple que el anterior, ya que solo estamos asignando una variable más en un paso más. Pero la complejidad surge cuando queremos actualizar a o b. Dado que aMasB es su propio estado raíz, ahora también debemos actualizarlo de manera imperativa:

```javascript
let a = 1;
let b = 2;

let aMasB = a + b;

// actualizar `a`
a = 4;
aMasB = a + b;

// actualizar `b`
b = 7;
aMasB = a + b;
```

Como creamos un nuevo estado raíz de manera imperativa, ahora debemos mantener siempre ese estado raíz en sincronía con el otro estado de manera imperativa también. Cada vez que ordenas al ordenador que actualice a, también debes ordenarle que actualice aMasB. Para un ejemplo más concreto, podrías imaginar una API de componente que te obligara a volver a renderizar manualmente cada vez que cambiaras un valor:

```javascript
export default class Counter extends Component {
  count = 0;

  @action
  incrementCount() {
    this.count++;
    this.rerender();
  }
}
```

Esto sería mucho para recordar, y podría introducir fácilmente errores si rerender() se llamara de la manera incorrecta, o en el momento incorrecto, o no se llamara en absoluto. El problema fundamental aquí es que ambos diseños requieren un comando para decirles que se actualicen cada vez que algo cambie.

Por el contrario, la programación "declarativa" no obliga al usuario a sincronizar manualmente las cosas cada vez. Consideremos nuevamente el ejemplo original para aMasB().

```javascript
let a = 1;
let b = 2;

function aMasB() {
  return a + b;
}
```

En este diseño, en lugar de asignar el valor a una nueva variable que debemos actualizar, creamos una función que deriva el valor. Efectivamente, estamos describiendo el "cómo" una vez, para que nunca tengamos que hacerlo de nuevo. En cambio, en todas partes de nuestro código, podemos llamar a aMasB() y saber que obtendremos el resultado correcto. Podemos declarar los valores que queremos usar y luego declarar cómo deberían interactuar con su entorno.

Esto es lo que hace que las plantillas en frameworks como Ember, Vue y Svelte sean tan poderosas, y (si acaso en menor medida) lo que hace que JSX se sienta mejor que devolver manualmente las llamadas de función a las que JSX se compila. HTML es fundamentalmente un lenguaje de programación puramente declarativo: no puedes decirle al navegador cómo renderizar, solo puedes decirle qué renderizar. Al extender HTML, las plantillas están extendiendo ese paradigma declarativo, y los frameworks modernos utilizan eso como base para su reactividad. El "qué" que los programadores están describiendo es, en última instancia, el DOM, y los frameworks descubren cómo traducir el estado de tu aplicación en ese DOM, sin que tú nunca tengas que preocuparte por ello.

¿Y el FP?
Hay muchas formas diferentes de lograr la programación declarativa. Puedes usar "streams" y "agents" y "actors", puedes usar objetos o funciones o una mezcla de ambos. Puedes crear tu propio lenguaje, como HTML, que sea puramente declarativo, y muchos sistemas de IU han hecho esto en el pasado debido a lo bien que funciona en general.

Una de esas formas es la programación funcional (o FP), que ha estado muy de moda recientemente por una variedad de razones. En lo que se conoce como programación funcional "pura", nunca se introduce ni cambia un nuevo estado raíz al calcular un valor; todo es un resultado directo de sus entradas.

```javascript
let a = 1;
let b = 2;

function sumar(primer, segundo) {
  return primer + segundo;
}

// para obtener a + b;
sumar(a, b);
```

En la forma más extrema de este modelo, el estado para toda la aplicación está completamente externalizado y luego se alimenta a la función principal de la aplicación. Cuando se actualiza el estado, ejecutas la función nuevamente con el nuevo estado, generando la nueva salida.

Diagrama de actualización de estado

Puede parecer una estrategia costosa, pero hay formas de reducir el costo (profundizaremos más en eso en la próxima entrada). Lo importante aquí es que el FP puro es necesariamente declarativo, porque todo se reduce a una función que recibe una entrada y produce una salida, sin hacer ningún cambio. Esto significa que no hay margen de maniobra para pasos imperativos que puedan hacer que las cosas estén fuera de sincronización.

Esta es una de las razones por las que a

 la gente le gusta la programación funcional. Es una forma muy estricta de programar, pero tiene muchos beneficios que vienen con esa rigidez, la declaratividad es uno de ellos.

Al final, sin embargo, la programación declarativa no se limita a la programación funcional, y por lo tanto, la reactividad en su conjunto tampoco lo está. La mayoría de los sistemas reactivos acaban siendo una mezcla de abstracciones y paradigmas, algunos inclinan más hacia un estilo de FP "puro" y otros se inclinan hacia la Programación Orientada a Objetos en algún nivel (por ejemplo, los sistemas basados en actores finalmente almacenan estado por proceso, lo que no es muy diferente de OOP. ¡Echa un vistazo a la historia del término "mensaje-paso" para ver algunas similitudes más!). Sin embargo, lo que tiene en común cada sistema reactivo es la declaratividad.

Resumiendo
Entonces, en esta entrada aprendimos:

"Reactividad" significa aproximadamente "un modelo de programación declarativo para actualizaciones basadas en cambios de estado". ¡Esta definición probablemente no pasaría el corte académico, pero es la definición que estoy usando para esta serie al menos!

"Estado" significa todos los valores que pueden cambiar en un programa. Hay dos tipos de estado (de nuevo, para los fines de esta serie):

Estado raíz, que son valores reales almacenados en variables, en matrices o en objetos directamente.
Estado derivado, que son valores que se derivan del estado raíz a través de getters, funciones, plantillas u otros medios.
La "programación declarativa" significa un estilo en el que el programador describe lo que quiere que sea su salida, sin describir cómo se hace exactamente. HTML es un ejemplo de un lenguaje de programación puramente declarativo, y la programación funcional es un estilo que asegura que el código sea declarativo. Hay muchas formas de escribir programas, bibliotecas y marcos declarativos utilizando cada paradigma de programación.

La próxima vez profundizaremos en varios modelos de reactividad a un alto nivel y discutiremos cuáles son las propiedades de un buen sistema reactivo. Discutiremos, en particular, cómo es posible crear sistemas reactivos que incorporen código orientado a objetos e imperativo, manteniendo aún así fundamentalmente la declaratividad. Y discutiremos dónde están las trampas de esos estilos y cómo los usuarios pueden "romper" la declaratividad en algunos casos.