Caso de estudio: Equipo de desarrollo de stack tecnológico React Un ejemplo más de que el contexto del proyecto y del equipo importa y mucho. Tienen problemas de mantenimiento de la aplicación. Me piden ayuda

- El backend no es suyo, es de un tercero y tiene un sistema de extension mediante apps como si fueran plugins - Por lo tanto, toda la lógica reside en la app React - Utilizan el patrón active record para comunicarse con el backend - Responsabilidades mezcladas en los modelos
- Mucha lógica en los componentes 
- Componentes muy grandes 
- No hay apenas test unitarios 
- Alguno de integración 
- Tenían end to end con Cypress, pero los desactivaron porque tenían muchos problemas de falsos errores
- Los componentes son funcionales, no de clases 
- Algún hook que otro y tienen contexto global con API context para cachear el usuario y el tema a aplicar 
- Mucho código duplicado entre componentes 
- La lógica está dispersa sin centralizar

Aplicaciones frontend con similares problemas ya sea Vue, React, Angular, etc. me encuentro habitualmente en las formaciones. En este caso es importante el contexto de la lógica de negocio debe residir al completo en la app.

La base de los problemas son los mismos casi siempre: 
- La lógica de negocio es muy importante y no está centralizada, aislada 
- Tienen lógica de presentación, de negocio de aplicación y empresarial mezclada 
- Acoplamiento entre presentación y datos 
- Código duplicado
- Es necesario ir dando forma al dominio creando entidades y value objects. 
- Crear casos de uso con lógica de aplicación 
- Crear repositorios o gateways utilizando inversion de dependencias para desacoplar la capa de datos 
- Crear un api client usado desde los repositorios

En este caso, para la capa de presentación analizamos dos opciones: 
- Utilizar el patrón bloc 
- Utilizar hooks como adaptadores de presentación Decidieron usar hooks porque ya los estaban usando y era conocimiento que ya tenía el equipo. Asumiendo el acoplamiento con React

Respecto al testing: 
- Iban a poder crear test unitarios de entidades, value objects y casos de uso 
- Para la lógica de presentación decidimos no hacer test unitarios de hooks sino en conjunto con los componentes usando React Testing Library
- En los test end to end el enfoque fue reducir su uso a happy paths sin usar fixtures que los hacían frágiles 
- Empezar a usar el plugin de Testing Library que se centra en probar de una forma más similar a como lo haría un usuario reduciendo la fragilidad de estos tests