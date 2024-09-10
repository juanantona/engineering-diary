Por lo que mi filosofía es probar lo mínimo posible para alcanzar un determinado nivel de confianza.

Pero sospecho que ese nivel es bastante elevado en comparación con los estándares de la industria, aunque podría estar pecando de arrogante.

No compruebo las típicas cosas en las que no cometo errores, como la creación de objetos.

En lo que si soy extremadamente cuidadoso es comprobar aquello en lo que suelo fallar, un buen ejemplo es la lógica condicional con bastante complejidad.

En cambio, cuando trabajo en equipo adapto mi estrategia para probar minuciosamente aquellas partes del código en las que el grupo se tiende a equivocar.

------

Esta flexibilidad se puede conseguir en el código aplicando el mismo principio: **Separar el qué del cómo**.

Imagina que tienes que recuperar datos de facturas. Si sabes separar el momento en el qué tienes que recuperar esos datos de cómo lo haces, ganas en flexibilidad, escalabilidad y otra de regalo, testabilidad.

Esto te permite por ejemplo que cuando estás en código de producción recuperas datos reales de un servidor pero cuando estas en modo testing recuperas datos de un servidor de mentira (ej:mock web server) o un objeto de mentira (doble de test). De esta forma, puedes probar cómo responde tu aplicación a diferentes escenarios de prueba. Incluso te permite probar escenarios que no son posibles manualmente, sin hacer guarradas, como un error 500.