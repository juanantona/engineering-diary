### Eficiencia

### [Effective Engineer - Notes](https://gist.github.com/rondy/af1dee1d28c02e9a225ae55da2674a6f)
### Resumen


### [How to Become a More Productive Software Engineer (Productivity Tips & Workflows)](https://plan.io/blog/become-a-productive-software-engineer/#develop-feedback-loops-to-know-what-work-brings-the-biggest-results)


### [SOFTWARE DEVELOPMENT, THE PARETO PRINCIPLE, AND THE 80% SOLUTION](https://projectricochet.com/blog/software-development-pareto-principle-and-80-solution)

### Resumen
Puntos previos a tener en cuenta:
- Los ingenieros muchas veces emplean demasiado tiempo en algo solo por el hecho de que les parece interesante
- Los ingenieros intentan pensar a largo plazo cuando en ocasiones la funcionalidad no lo requiere porque simplemente se quiere probar algo 
- Muchas veces los PM desconocen la implicación técnica de una funcionalidad y empujan a crear funcionalidades que implican un consumo excesivo de recursos
- En general todo el mundo es deficiente en cuanto a comunicación 
- Siempre es más seguro hacer sobre ingeniería que no hacerla
- En general los ingenieros no son conscientes del coste para la empresa de los desarrollos


### [The 80/20 Principle in Programming](https://blog.finxter.com/the-80-20-principle-in-programming/)
### Resumen
- Necesitas encontrar las metricas apropiadas que tienes que mejorar para aumentar tu productividad
- Una vez identificadas, ser más perezoso (menos perfecionista) en el resto de tareas, en lugar de ser aprendiz de mucho y maestro de nada.
- En programación los resultados están mucho más sesgados hacia arriba que en la mayoría de los otros campos. Es más 90/10. ¿Por qué?:
	- Resolver problemas que nadie más puede resolver
	- Escribir código con menos bugs
	- Ecribir código más escalable 
	- Proporcionar soluciones creativas, que busquen soluciones más sencillas poniendo en foco en lo más importante
- Es iportante buscar las métricas correctas porque de otro modo estarás esclavizado por aquellas que no son importantes 
- Incluso un pequeño aumento de la productividad puede traducirse en un gran incremento de los resultados


### [We could say **productivity is more of a means to an end – performance.**](https://medium.com/oreillymedia/measuring-engineering-productivity-a6da8605ffae) 

### [The SPACE of Developer Productivity](https://queue.acm.org/detail.cfm?id=3454124)

- Un desarrollador que optimiza sólo para su propia productividad personal puede perjudicar la productividad del equipo
- Las actividades más centradas en el equipo, como las revisiones de código, y el desarrollo y la gestión de sistemas de ingeniería, ayudan a mantener la calidad de la base de código y del producto/servicio.
- Es fundamental encontrar el equilibrio adecuado para optimizar la productividad individual, del equipo y de la organización, así como comprender las posibles compensaciones.

### [Assessing Employee Performance](https://medium.com/javascript-scene/assessing-employee-performance-1a8bdee45c1a) by Eric Elliot


### TOOLS FOR AUTOMATING METRICS
- Waydev
- [LinearB](https://linearb.io/) -> [Docs](https://linearb.helpdocs.io/)
	- Metrics (DORA)
		- Cycle Time: The amount of time it takes for code to get into production
		- Deployment Frequency: How often an organization successfully releases to production
		- Mean Time ToRestore: How long it takes an organization to recover from a failure in production
		- Change Failure Rate: The percentage of deployments causing a failure in production
- [Sleuth](https://help.sleuth.io/)
	- Metrics:
		- Deployments per day (indica el tamaño de los deployments)
		- Time from the first commit to deploy
		- Failures
		- The time a project spends in a failure state
	- Puedes agrupar un conjunto de repos como un proyecto
	- Integraciones: DataDog, bugsnag
	- Tiene en cuenta diferentes entornos
- [Haystack](https://www.usehaystack.io/)
	- Metricas:	
		- Merged PR over time per week
		- Average Time from first commit to merging a PR
		- Number of deployments per week
		- Relation between deployments and bugs
- [GitClear](https://www.gitclear.com/)
	- Poco maduro



