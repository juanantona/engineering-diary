El dominio de una app es todo aquello relacionado con la lógica de negocio.

El dominio de una app es como Matrix aunque no sepamos verlo esta por todas partes.

Si estos conceptos están dispersos por ejemplo en la capa de presentación o incluso en la capa de datos resulta bastante complicado el mantenimiento de la aplicación.

-------


Hoy te voy a dar la clave para aprender a diferenciar los dos tipos de reglas de negocio existen en el desarrollo de software.

Es una de las preguntas que más veces me han hecho en redes sociales, por email o en los cursos.

Voy a usar una historía real propia, en concreto con mi coche, que suelo usar en las formaciones:

Cuando tenía 20 años tuve mi primer coche y lo tenía asegurado a todo riesgo.

Por aquel entonces, no era experimentado todavía y no tenía garaje, por lo tanto, era normal que cada cierto tiempo el coche tuviera pequeños golpes al estar aparcado siempre en la calle.

Yo iba acumulando estos golpes y cuando tenía una parte del coche con los suficientes, lo llevaba al taller para que me lo arreglarán.

Lo primero que tenía que hacer era buscar un taller que trabajará con mi aseguradora. Al llegar al taller hace 20 años lo que tenías que hacer era rellenar un parte a mano. Una hoja de papel donde poner una serie de datos.

En ese parte era obligatorio rellenar datos como nombre, apellidos, matrícula del coche y número de póliza del seguro, etc.

Si alguna vez se me olvidaba rellenar algún dato, cuando iban los peritos del seguro decían que no podían revisar el coche sin esos datos. Entonces el mecánico del taller me llamaba para pedírmelos.

A los pocos días, yo llamaba al mecánico para ver si ya estaba el coche listo. A veces había suerte, otras no y tenía que volver a llamar a los días o me llamaba el mecánico al terminar si se acordaba y no tenía mucho lío.

Con los años el proceso ha cambiado bastante.

O no tanto.

Desde hace algunos años, existen aplicaciones móviles y sistemas, está todo mucho más automatizado. Ahora al llegar al taller el parte se da por teléfono o desde una app directamente con la aseguradora.

¿Y sabes qué datos te piden? Los mismos que cuando se hacía en papel, eso no ha cambiado.

Lo que cambia son las automatizaciones que hay durante el proceso.

Ahora al registrar el parte por teléfono o desde la aplicación te llega un mensaje vía SMS o un correo con un código. Algo así como el número de pedido y se lo tienes que enviar al mecánico.

Cuando los peritos revisan el coche te llega otro mensaje. Y cuando el coche está listo, te llega uno más. Hasta otro de encuesta de satisfacción del taller llega a veces a los pocos días.

Y esas son de las automatizaciones que nos enteramos nosotros como clientes, pero habrá muchas más internamente en el proceso.

El proceso de arreglar un coche hace 20 años donde el parte se rellenaba en un papel, y en esta época donde se usa una aplicación, tienen cosas en común.

Presta atención, aquí está la clave.

Sin unos datos obligatorios, al rellenar o registrar el parte no se inicia el proceso de arreglar el coche. Estas reglas dependen puramente del negocio, no de la aplicación de software que automatiza el proceso.

Este tipo de **validaciones o invariantes que no dependen de que exista una aplicación que automatice** los procesos, sino exclusivamente del negocio, se conocen como **reglas de negocio empresarial**.

Sin embargo, hay una parte que no tienen en común. Todas esas automatizaciones que hacen la vida más fácil a las personas y que no existían cuando el proceso era manual.

Y todas esas **a reglas que existen con el objetivo de automatizar procesos dentro de un negocio a través de un sistema o aplicación**, se conocen como **reglas de negocio de aplicación**.

Estas sí dependen de la aplicación de software que automatiza el proceso.