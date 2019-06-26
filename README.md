# anime 
Mantiene el control del anime que sigues

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

. /usr/local/bin
- /home/<usuario>/bin

Puesto que este script requiere tener sintel instalado, recomendamos mirar el proceso de instalación de sintel en el [link](https://github.com/mhyst/sintel "repositorio correspondiente").
