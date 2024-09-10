URL: https://tkdodo.eu/blog/practical-react-query  
TAGS: #react  

Practical React Query
https://tkdodo.eu/blog/practical-react-query

What Apollo gives you is not just the ability to describe which data you want and to fetch that data, it also comes with a cache for that server data. This means that you can just use the same useQuery hook in multiple components, and it will only fetch data once and then subsequently return it from the cache.

So it seems that we have always been treating this server state like any other client state.
Except that when it comes to server state your app does not own it. We have only borrowed it to display the most recent version of it on the screen for the user.
It is the server who owns the data.

To me, that introduced a paradigm shift in how to think about data. If we can leverage the cache to display data that we do not own, there isn't really much left that is real client state that also needs to be made available to the whole app.

---

Lo que Apollo te ofrece no es sólo la capacidad de describir los datos que quieres y de obtenerlos, sino que también viene con una caché para esos datos del servidor. Esto significa que puedes utilizar el mismo hook useQuery en varios componentes, y sólo obtendrá los datos una vez y posteriormente los devolverá de la caché.

Obtener datos del servidor y hacerlos disponibles en cualquier lugar.



