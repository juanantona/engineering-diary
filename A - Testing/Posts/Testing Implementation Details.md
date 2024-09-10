TAGS: #testing  
TITLE: Testing Implementation Details  
URL: https://kentcdodds.com/blog/testing-implementation-details  
AUTHOR: Kent C Dodds  
___

Los detalles de implementación son cosas que los usuarios de su código no suelen utilizar, ver o incluso conocer.

Así que la primera pregunta a la que necesitamos respuesta es: "Quién es el usuario de este código". Bueno, el usuario final que estará interactuando con nuestro componente en el navegador es definitivamente un usuario. Estarán observando e interactuando con los botones y contenidos renderizados. Pero también tenemos al desarrollador que renderizará el acordeón con props (en nuestro caso, una lista dada de elementos). Así que los componentes React suelen tener dos usuarios: los usuarios finales y los desarrolladores. Los usuarios finales y los desarrolladores son los dos "usuarios" que el código de nuestra aplicación debe tener en cuenta.

Genial, entonces ¿qué partes de nuestro código utiliza, ve y conoce cada uno de estos usuarios? El usuario final verá/interactuará con lo que renderizamos en el método render. El desarrollador verá/interactuará con los props que pasen al componente. Así que nuestra prueba sólo debería ver/interactuar con los props que se pasan, y la salida renderizada.

Al hacer que nuestros tests utilicen el componente de forma diferente a como lo hacen los usuarios finales y los desarrolladores, creamos un tercer usuario que el código de nuestra aplicación debe tener en cuenta: ¡las pruebas!

> Cuanto más se parezcan tus pruebas a la forma en que se utiliza tu software, más confianza te darán.

1. ¿Qué parte de su código base no probado sería realmente malo si se rompiera? (El proceso de pago)
2. Trate de reducirlo a una unidad o unas pocas unidades de código (Al hacer clic en el botón "checkout" una solicitud con los artículos del carrito se envía a /checkout)
3. Observa el código y piensa quiénes son los "usuarios" (el desarrollador que crea el formulario de pago, el usuario final que pulsa el botón).
4. Escribe una lista de instrucciones para que ese usuario pruebe manualmente ese código para asegurarse de que no está roto. (Renderizar el formulario con algunos datos falsos en el carrito, hacer clic en el botón de pago, asegurarse de que la API /checkout fue llamada con los datos correctos, responder con una falsa respuesta exitosa, asegurarse de que el mensaje de éxito se muestra).
5. Convierte esa lista de instrucciones en una prueba automatizada.