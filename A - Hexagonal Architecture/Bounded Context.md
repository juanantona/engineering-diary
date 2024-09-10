Como se puede aprender algo de cualquier situación, te voy a contar una cagada mía (o no solo mía) bastante gorda, y de paso vas a aprender un concepto de DDD (Domain Driven Design).

Resulta que por 2012 yo trabajaba como desarrollador de software (matiz importante para reírte más con la historia) en una empresa donde uno de los negocios era Dropshipping.

Dropshipping es un modelo de negocio donde tú compras un producto en AliExpress y lo vendes en Amazon más caro, por ejemplo. No es un negocio que vaya a mejorar la vida de nadie a través de la tecnología.

Es un modo de aprovecharse del sistema para enriquecerte y no es un negocio del que sentirse orgulloso como para que hereden tus hijos.

Por razones que no vienen a cuento, me encontraba yo un sábado subiendo ficheros Excel a mano (sí a mano) de productos a Sears (un marketplace de USA).

Después de llevar un tiempo, si no alguna hora, subiendo ficheros Excel (repito a mano), me olvidé de cambiar los precios de los productos en uno de los ficheros y se subieron portátiles a 0.02 $, que era el valor por defecto de Sears.

¿Y sabes lo mejor de todo?... hubo clientes que los compraron.

Fue una movida muy gorda en la empresa. A alguien debió parecerle que no fui el principal culpable, porque a raíz de esto casi me hacen Project Manager.

¿Cómo te quedas?, aunque esa segunda historia es más para contarla con unas cervezas.

Bueno, pero te he prometido aprender un concepto DDD con esta historia.

Dejando a un lado la idea desafortunada de tener a una persona subiendo ficheros Excel a mano un sábado por la mañana (¿te acuerdas que era desarrollador no?), un concepto de DDD que podemos aprender es el concepto de **invariante**.

En una situación donde hubiera sentido común, por algún lado, el proceso hubiera estado automatizado por una aplicación o un servicio.

Algo que debería haber hecho esa aplicación, es validar que los productos tuvieran un precio correcto.

Algo que demostré con mi cagada es qué, para mi empresa de entonces, el precio mínimo era diferente al de Sears. O por lo menos, que no se podían poner a la venta ningún portátil a 0.02 $.

Pues en alguna parte del código se debería haber validado que el precio por defecto de Sears no era el precio final al que se subía cada producto.

¿Dónde se debería hacer esta validación?

En una entidad de dominio Producto. Posiblemente en un Bounded Context llamado algo así como Sears Product Importer.

Una **invariante** es una regla de negocio empresarial que siempre debe ser consistente. Es una regla de negocio que siempre se tiene que cumplir, no se puede romper.

Las entidades deben validarse a sí mismas y si no se aseguran las invariantes, debe fallar su creación. Las entidades tampoco deben permitir modificaciones si se incumplen invariantes.

Un aggregate root es una entidad que contiene entidades hijas. Y la principal responsabilidad de un agregado es hacer cumplir la consistencia de los invariantes en todas las entidades dentro de sí mismo.