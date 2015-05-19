# data-viz-lab
Data Visualization Lab. Learn together!

Notas colaborativas: http://etherpad.guifi.net/p/dataviz

## Sesión 3. Mapas. 2015-05-27 18:30

### Presesión
- Nos gustaría seguir con lo de la sesión 2 que nos propusimos en la sesión2 que no acaba de funcionar. Y sacarle más jugo al tema.
- Si nos da tiempo, usar como fuente osm.org


## Sesión 2. Mapas. 2015-05-19

### Presesión (Martin propuso)

Vamos a hacer un mapa del paro en CAT por municipios. Para ello bajaremos los datos geograficos y luego buscaremos los datos del paro en el IDESCAT. Ejemplo y info para los GeoJSON: http://bl.ocks.org/martgnz/1b7ba8ebd60a1567e855

Edición y conversión de shapefiles: GDAL, topojson, QGIS
- http://www.gdal.org/ogr2ogr.html
- npm install -g topojson
- http://www.qgis.org/en/site/

Obtener datos:
- http://datos.gob.es/catalogo/paro-registrado-municipios
- http://www.lavanguardia.com/vangdata/20150407/54429720751/las-cifras-del-paro-en-catalunya-por-municipios-y-comarcas.html -> mirar CSV


### En el hacklab

Decidimos hacer un mapa de puntos (redondas más grandes o pequeñas en función de un valor, esto es mu fácil hacerlo con cartodb.com, cartodb no es open source! es freemium):
- http://webs.ono.com/2geografia/images/mapasimbolos.jpg
- esto nos debería servir: http://bl.ocks.org/phil-pedruco/7745589

datos: prisiones, tenemos localización y número de presos

para ello nos pusimos a montar un mapa de Cataluña desde http://www.icc.cat/ (hay que registrarse). A partir de aquí se discutió de que sería mejor usar osm.org, lo dejamos como extensión para la sesión 3.

Vamos a trabajar con sahpe files, si quisiéramos el de otro país en google: "shapefile <país>", debería funcionar.

Requiere programa qgis
- MAC, complicao
- debian/ubuntu: sudo apt-get install qgis

SHP contiene información de los polígonos del mapa, y datos de cuáles son las comarcas, etc.
en mac hay problema con el encoding de texto (los acentos se ven mal) [no probado en gnu/linux] y hay que usar source encoding windows-1252 en el properties.

conversión de shapefile a json, ya que d3 lee json, el comando que está aquí: http://bl.ocks.org/martgnz/1b7ba8ebd60a1567e855map

[ogr2ogr not found, desde el mac instalamos http://brew.sh]

pero quitamos el filtrado de municipios (el where):

```
ogr2ogr \
  -f GeoJSON \
  -t_srs 'EPSG:4326' \
  output.json \
  input.shp
```

municipios.json (output.json): 20 MB, vamos a reducir su tamaño suavizando (eliminando detalle) de las formas con mapshaper.org, pasamos a KB

Montamos un directorio para trabajar con los datos de sesión 2. Y lo hacemos que se pueda acceder desde el navegador, en ese mismo directorio: `python -m SimpleHTTPServer`, en el navegador: localhost:8000

Códig y comentarios del código en el README de la sesión 2: https://github.com/hacklabupf/data-viz-lab/tree/master/sesion2-intro-mapas

### Postsesión: editor de texto atom

El editor de texto atom es ideal para [manejarse con código HTML/CSS](http://blog.atom.io/2015/05/15/new-autocomplete.html) 
también, [podemos encontrar qué está fallando en el código antes de probarlo](https://atom.io/packages/linter). Para instalarlo, ir a: https://github.com/atom/atom#installing

## Sesión 1. Gráficos sencillos. 2015-05-12

- Presentación
  - disponible en https://hacklabupf.github.io/data-viz-lab/d3-intro/
  - código fuente: https://github.com/hacklabupf/data-viz-lab/tree/master/d3-intro
  - wiki de d3 en github tiene mucha informacion: https://github.com/mbostock/d3/wiki
  - libro scott murray code artist d3 tutorials, recomendable: http://alignedleft.com/tutorials/d3
  - Trabajamos en bar chart: http://bl.ocks.org/mbostock/7322386
  - Otros gráficos de Martin http://bl.ocks.org/martgnz
- Ejemplos que motivan:
  - http://homicide.igarape.org.br/
  - http://earth.nullschool.net/#current/wind/surface/level/orthographic=-22.02,36.10,1451

- Chome Extension (Web technologies): Wappalyzer
- Sobre WebGL: http://webglfundamentals.org

- Otras actividades:
  - 2 a 7 de junio, Jornadas Periodismo de datos en Madrid y Barcelona: http://periodismodatos.okfn.es
  - PyladiesBCN: http://www.meetup.com/PyLadies-BCN/

## Where to find data
- http://opendata.bcn.cat/opendata/ca
- https://github.com/caesar0301/awesome-public-datasets

## Presentation (spanish)

### Qué?
Hemos decidido hacer una serie de encuentros relacionados con la Visualización de Datos en el Hacklab de la UPF

### Cómo?
- Lo haremos en base a proyectos que decidamos los allí presentes. Abordaremos problemas de visualización con datos disponibles desde los diferentes puntos de vista que cada uno tengamos. Podemos asegurar uno periodístico (martí) y otro ingenieril (pedro).
- La idea es que entre todos aprendamos de todos. Ser multidisciplinares.
- Empezaremos con d3js, y nos gustaría seguir por ahí porque creemos que es la biblioteca más interesante. Pero será en tiempo presente y espacio físico que veremos hacia dónde vamos.
- Usaremos entornos GNU/Linux. Si no tenéis GNU/Linux, vamos a intentar tener portátiles con acceso a root. Alternativamente, fuera de esas sesiones, yo mismo lo puedo instalar en vuestro ordenador.
- Usaremos este repositorio [1] para documentar el trabajo

### Cuántos? Para quién?
- Como mínimo 2, Martí y yo (Pedro), nos hemos responsabilizados para venir.
- Para quien lo considere interesante. Está abierto a todos los públicos: tanto estudiantes de la UPF como los que no lo sean. Si conocéis alguien interesado que no está en la lista hacklab, reenviarle esta información. En principio, con la red que se está montando de acceso internet para los de fuera, no debería haber problemas de acceso / acceso limitado.

### Cuándo?
- 3 sesiones [interrupción debido a exámenes de 3r Trimestre]
  - Lunes 11 y 18 de Mayo de 18:30 a 20:00
  - 26 de Mayo de 18:30 a 20:00
- En la primera sesión Martí dará una pequeña introducción de d3js como punto de partida.

### Y qué, después?
Haremos balance sobre cómo ha ido la experiencia. Se podría continuar para el próximo trimestre, o cambiar a otra área.
