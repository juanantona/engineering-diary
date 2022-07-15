# Remix
## Documentación de referencia
- [Remics docs](https://remix.run/docs/en/v1)

https://kentcdodds.com/blog/why-i-love-remix






## Caching
- [CDN Caching, Static Site Generation, and Server Side Rendering](https://www.youtube.com/watch?v=bfLFHp7Sbkg)

## [Remix vs Next.js](https://remix.run/blog/remix-vs-next)
- Básciamente Next.js es un SSG (igual que Gatsby)
- Remix no hace peticiones de datos desde el cliente
- En Next.js se produce una divergencia de arquitectura dado que se hacen peticiones de datos de APIs tanto en tiempo de build como desde el cliente -> en Remix no, y esto tiene ciertas ventajas, como no necesita autenticación en el cliente, no importa si la API soporta CORS, la cache solo funciona del lado del servidor 
- Remix construye dinamicamente páginas estáticas en un servidor y las sirve a través de un CDN (por ejemplo Vercel) con politica de cache abilitada 
- La principal desventaja de Next frente a Remix es la network waterfall chains, es decir la cadena de peticiones que son necesarias realizar para obtener datos en el cliente 


En el momento de `build`, Next.js extrae los datos de Shopify, renderiza una página en un archivo HTML y lo coloca en el directorio público. Cuando el sitio se despliega, el archivo estático se sirve ahora en `the edge` (fuera del CDN de Vercel) en lugar de atacar un servidor de origen en una sola ubicación. 

Cuando llega una solicitud, el CDN simplemente sirve el archivo. La carga de datos y la renderización ya se han realizado con antelación, por lo que el visitante no paga el coste de descarga + renderización. Además, el CDN está distribuida globalmente, cerca de los usuarios (esto es "the edge"), por lo que las solicitudes de documentos generados estáticamente no tienen que viajar hasta un único servidor de origen.

Remix no soporta SSG así que usamos la directiva de caché HTTP stale-while-revalidate (SWR, no confundir con el paquete de fetching de cliente swr de Vercel). El resultado final es el mismo: un documento estático en el borde (incluso en el mismo CDN, el de Vercel). La diferencia es cómo los documentos llegan allí.

> 
> La directiva de respuesta stale-while-revalidate indica que la caché podría reutilizar una respuesta antigua mientras la revalida a una caché.
> 
> Cache-Control: max-age=604800, stale-while-revalidate=86400
> 
> En el ejemplo anterior, la respuesta está fresca durante 7 días (604800s). Después de 7 días se vuelve obsoleta, pero la caché puede reutilizarla para cualquier petición que se haga al día siguiente (86400s), siempre que revalide la respuesta en segundo plano.
> 

En lugar de obtener todos los datos y convertir las páginas en documentos estáticos en el momento de la construcción/despliegue, la caché se prepara cuando se recibe tráfico. Los documentos se sirven desde la caché y se revalidan en segundo plano para el siguiente visitante. Al igual que SSG, ningún visitante paga el coste de descarga + renderización cuando se recibe tráfico. Si se pregunta por los fallos de la caché, hablaremos de ello más adelante.

SWR es una gran alternativa a SSG. Otra cosa que hace que el despliegue en Vercel sea genial es que su CDN lo soporta.

En páginas altamente dinámicas SSG no esacala puesto que no se pueden generar infinitas páginas estáticas con todas las variaciones posiblés de contenido.

En esos casos en los que SSG está fuera de uso se opta por traer los datos desde el cliente mediante JS.

**Por qué Next.js es más lento**: Next.js introdujo lo que llamamos una "cadena de peticiones en cascada de la red". Como no se puede utilizar SSG, la aplicación obtiene los resultados de la búsqueda desde el navegador del usuario. No puede cargar imágenes hasta que haya obtenido los datos, y no puede obtener datos hasta que haya cargado, analizado y evaluado el JavaScript.

**Por qué Remix sigue siendo tan rápido como la página de inicio**: Mientras que SSG no puede almacenar en caché la página de búsqueda, las versiones de Remix sí: con SWR o Redis.  Cuando se dispone de una forma única y dinámica de generar páginas, se puede ajustar la estrategia de almacenamiento en caché sin cambiar el código de la aplicación. El resultado es la velocidad de SSG en las páginas más visitadas.

