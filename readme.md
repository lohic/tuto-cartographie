# Cartographie interactive #

avec [leafletJS](http://leafletjs.com)

## Faire une carte personnalisée avec des dimensions en pixels ##

###Dimensions de la carte ###

Les tuiles gérées par lealetJS ont toutes une dimension de 256 x 256 pixels. Sachant qu'au changement d'échelle, chaque tuile est divisée en 4, les dimensions optimales d'une image devraient respecter la progression suivante :

- level 0 > 256
- level 1 > 512
- level 2 > 1024
- level 3 > 2048
- level 4 > 4096
- level 5 > 8192
- level 6 > 16348
- …

### Générer la carte ###

Vous pouvez générer les différentes **tuiles** avec un script dans le terminal de votre ordinateur en utilisant un programme nommé imagemagick (cf le tutorial sur cette page : [http://omarriott.com/aux/leaflet-js-non-geographical-imagery/](http://omarriott.com/aux/leaflet-js-non-geographical-imagery/)).

Néanmoins cette méthode peut être assez technique. Vous pouvez également utiliser un programme comme [MapTiler](http://www.maptiler.org). Celui ci s'occupe de générer toutes les vignettes de votre carte, ainsi que le fichier html nécessaire à l'utilisation de leafletJS. Attention, dans sa version gratuite, le programme ne permet pas de gérer des images dont les dimensions sont supérieures à 10240 pixels. Les *tuile* auront également un watermark "maptiler" inscrit dessus.


### Placer un marqueur avec des coordonnées en pixels ###

Même avec une carte en pixels le système de coordonnées adopté est basé sur les coordonnées GPS d'OpenStreetMap. Ceci, notamment pour prévenir les problèmes de positionnement lié aux changements d'échelle.

Pour pouvoir positionner l'abcisse et l'ordonnée d'un point en pixels, il faut utiliser la fonction suivante :

```js
map.unproject(
  [x, y],
  map.getMaxZoom()
)

```

Ainsi le positionnement d'un marqueur au point 1000, 1000 se fera de la manière suivante :

```js
var marker = L.marker(
    map.unproject(
      [1000, 1000],
      map.getMaxZoom()
    )
).addTo(map);
```

