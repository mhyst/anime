# anime 
Mantiene el control del anime que sigues

## Problemática

Me gusta el anime. Y he descubierto que no importa el empeño que le pongas, siempre hay series anime de las que ya no te quedan episodios por ver hasta que saquen el siguiente o la siguiente temporada. Acabas rellenando el hueco dejado con otro anime. Este esquema de cosas tiende a replicarse y al final acabas con un buen número de series que sigues. Y entonces descubres que de tal anime que te gustaba mucho no recuerdas por qué episodio te llegabas. Muchas veces he hecho el apaño de dejar varias pestañas del navegador con jkanime o animeflv abiertas para no perder el hilo. Pero esa solución acaba desaprovechando recursos y tampoco es muy bueno el uso de marcadores, a menos que dediques tu tiempo a mantenerlos actualizados. No es imposible, pero tampoco cómodo.

Ese es el problema que he tratado de resolver con este script. Imaginemos una simple tabla en una base de datos sqlite que tenga un registro por cada anime que sigues y las columas id, titulo, url y episodio. Como somos olvidadizos, un menu que nos recuerde qué cosas seguimos viene bien. La mayoría de animes tienen urls que incluyen el número de episodio, por lo que si cogemos el resto de la url (sin el http:// o el https;//) podemos acceder a cualquier episodio cocatenando esta url con el número del episodio almacenado. Solo nos resta una manera de incrementar el número del episodio cuando hayamos terminado de ver el anterior. Para eso el script simplemente pregunta si queremos avanzar el puntero justo después de abrir el anime en el navegador. De esa forma no tenemos por qué percatarnos de la pregunta hasta después de haber terminado de ver el episodio. Lo he hecho así ya que muchas veces empezamos a ver un episodio y lo tenemos que dejar. De todas formas, gracias a mi otro script sintel, podemos manipular todo a mano después de manera muy simple; mediante el nuevo módulo anime. Y también existe una solución más prosaica: mantener abierta la pestaña del último anime que nos dejamos a medias y quitar el if de modo que siempre se avance el episodio automáticamente. Es cuestión de elegir una filosofía.

Con este simple script podemos cerrar todas esas pestañas de anime que tenemos abiertas y saber en todo momento por qué episodio nos llegábamos de aquel anime tan bueno que hace tiempo que dejamos de ver.

## Motivo por el que este script utiliza sintel

Sintel ya incluye todo el tratamiento de la base de datos, varios módulos y montones de funciones disponibles; todo lo cual hace que crear un módulo de anime dentro de sintel fuera más sencillo y rápido que escribir todo el script de cero. Sintel es un trabajo en progreso que ha ido creciendo conforme lo he ido necesitando. Creció tan rápido que aunque al principio iba a contar con un interfaz de línea de comandos complejo, es decir, un nombre de opción para cada función pública, muy pronto me di cuenta que iba a ser mucho más práctico si ideara una manera de invocar cualquier función y pasarle argumentos directamente por la línea de comandos en lugar de hacerlo con opciones más crípticas. Así fue como surgió primero la opción de invocación de funciones '-f' y finalmente la más avanzada '-n'.

Por lo tanto el script, más que algo completo, es una especie de frontend del módulo anime de sintel.

## Dependencias
- sqlite3 (por sintel)
- sintel
- un navegador

## Inicializar la base de datos de anime

Por el momento el script no permite agregar animes. Para agregarlos hay que utilizar sintel de la siguiente forma:

---

sintel -n anime.add:"Shingeki no Kyojin|animeflv.net/ver/52275/shingeki-no-kyojin-season-3-part-2-"

---

Como se puede ver, basta con llamar a la función add del módulo anime que tiene sintel integrada y pasarle como argumentos el título y la url. Esta última sin el prefijo. Una vez que ya tenemos los animes que seguimos añadidos de esta forma, solo nos queda actualizar el número de episodio de cada uno, ya que por defecto se inicaliza con 1. Eso se hace también con sintel:

---

sintel -n anime.updateEpisodio:"1|131"

---

En este caso tenemos que invocar la función updateEpisodio del módulo anime, indicando el id del anime que queremos modificar y el siguiente episodio que tenemos que ver. Al insertar un anime nuevo anime.add devuelve el id del anime, pero en caso de que queramos consultar los animes que tenemos ya metidos podemos hacerlo con el siguiente comando:

---

sintel -n anime.list

---

En realidad sintel hace casi todo el trabajo. El script 'anime' lo único que hace es presentar los datos de una forma más amigable para el usuario.

## Instalación ##

Basta con clonar el repositorio y mover el archivo 'anime' a cualquier carpeta que se encuentre en el PATH. Las posibilidades son varias, aunque las más recomendables son estas:

- /usr/local/bin
- /home/<usuario>/bin

Alternativamente puede descargarse el paquete deb de la última release. Una vez descargado basta con ejecutar:

---

sudo dpkg -i anime-sintel.1.0.deb

---

Para poder instalarlo de esta manera debe instalar antes sintel mediante el mismo procedimiento.

Puesto que este script requiere tener sintel instalado, recomendamos mirar el proceso de instalación de sintel en el [repositorio correspondiente](https://github.com/mhyst/sintel).
