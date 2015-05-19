fichero test: index.html

lo que estamos trabajando:: index mapa prisiones.html

entendiendo el index.html
- d3-tip (focaliza bonito)
- margin: ancho, alto. ajustar el cuadro en la web
- para mapas vamos a poner NOM_MUNI: nom municipi
- 'var projection' y 'var path', que nos ayudará a geolocalizar cosas dentro dle mapa
- 'var color' paleta de colores para el mapa
  - /map brewser/ (?): cómo hacer escalas de colores para mapas
  - encontré esto como lo más parecido http://colorbrewer2.org/

- var 'svg': montar el svg
  - d3 trabaja con svgNOM_MUNI: nom municipi
  - append('g'): agrupar todo el svg en un grande, y dentro habrá otros objetos svg, podremos manipular objetos svg en grupo
- lo de los fors es "programación pura", hace un JOIN de la infromación del csv con la del json a través de la columna compartida. El problema es que algunas comarcas no encaja el nombre y por eso se ven en gris
