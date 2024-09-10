URL: https://kentcdodds.com/blog/write-tests  
TAGS: #react  #testing  

Cuando te esfuerzas por alcanzar el 100% del code coverage todo el tiempo, te encuentras gastando tiempo probando cosas que realmente no necesitan ser probadas.
 
Lo mejor es que evites probar los detalles de implementación porque no te da mucha confianza en que tu aplicación funcione y te ralentiza a la hora de refactorizar.

Si compruebas de manera aislada dos componentes que deben trabajar juntos descubrirá que, si comprueba que funcionan juntos correctamente, a menudo no tendrás que molestarte en probarlos de forma aislada.

Creo que lo mejor que puedes hacer para escribir más tests de integración es dejar de simular tantas cosas. Cuando imitas algo estás eliminando toda confianza en la integración entre lo que estás probando y lo que está siendo imitado.

No creo que nadie pueda argumentar que probar software es una pérdida de tiempo. El mayor reto es saber qué probar y cómo hacerlo de forma que ofrezca verdadera confianza en lugar de la falsa confianza de probar detalles de implementación.

---