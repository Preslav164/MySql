# Consultas básicas en MongoDB (con salida esperada textual)


### Consulta:
```javascript
db.llibres.find()
```

**Salida esperada:**
> Una lista de libros con todos sus campos.


### Consulta:
```javascript
db.llibres.find({ autor: 'Irene Solà' })
```

**Salida esperada:**
> Un libro titulado 'Canto jo i la muntanya balla' de Irene Solà.


### Consulta:
```javascript
db.llibres.find({ nombre_pagines: { $gt: 200 } })
```

**Salida esperada:**
> Libros con más de 200 páginas como 'Cicatriz' o 'Llibre extens'.


### Consulta:
```javascript
db.llibres.find({ autor: 'Sara Mesa', nombre_pagines: { $gt: 200 } })
```

**Salida esperada:**
> Un libro titulado 'Cicatriz' de Sara Mesa.


### Consulta:
```javascript
db.llibres.find({ $and: [ { autor: 'Sara Mesa' }, { nombre_pagines: { $lt: 200 } } ] })
```

**Salida esperada:**
> Un libro titulado 'Un amor' de Sara Mesa.


### Consulta:
```javascript
db.llibres.find({ resum: /família/ })
```

**Salida esperada:**
> Un libro cuyo resumen menciona la palabra 'família'.


### Consulta:
```javascript
db.llibres.find({ genere: { $in: ['novel·la', 'poesia'] } })
```

**Salida esperada:**
> Libros de género 'novel·la' o 'poesia', como 'Versos lliures'.


### Consulta:
```javascript
db.llibres.find({ fecha: { $gte: ISODate("2023-01-01") } })
```

**Salida esperada:**
> Libros publicados a partir del 1 de enero de 2023.


### Consulta:
```javascript
db.municipis.find({provincia: 'València'}).count()
```

**Salida esperada:**
> 266


# Teoría MongoDB — Consultas básicas

## Consultas básicas
Todas las consultas en MongoDB se realizan mediante la llamada a la función
find
sobre una colección.
db.collection.
find
()
Esta función devuelve los 20 primeros documentos de la colección. Si queremos ver los siguientes 20 documentos, podemos utilizar la función
it
:
it
Ejemplo
Consultamos todos los documentos de la colección
llibres
:
db.llibres.
find
()
## Filtrar documentos
Podemos filtrar los documentos que devuelve la consulta añadiendo un objeto con los criterios como parámetro de la función
find
:
db.collection.
find
(
{
camp
:
valor
}
)
Ejemplo
Consultamos los libros del autor
Irene Solà
:
db.llibres.
find
(
{
autor
:
'Irene Solà'
}
)
## Operadores de comparación
Podemos utilizar los siguientes operadores de comparación para filtrar los documentos:
* `$eq`
: al igual que (
ecual
). Éste es el operador por defecto.
* `$ne`
: diferente de (
not ecual
).
* `$gt`
: mayor que ( greater
than
).
* `$gte`
: mayor o igual que ( greater than or ecual
)
.
* `$lt`
: más pequeño que (
less than
).
* `$lte`
: más pequeño o igual que ( less than
or ecuals
).
* `$eq`
La consulta anterior es equivalente a:
db.llibres.
find
(
{
autor
:
{
* `$eq`
:
'Irene Solà'
}
}
)
* `$gt`
Consultamos los libros con más de 200 páginas:
db.llibres.
find
(
{
nombre_pagines
:
{
* `$gt`
:
200
}
}
)
## Múltiples criterios
Podemos añadir múltiples criterios de filtrado a la consulta, que deben cumplirse todos:
db.collection.
find
(
{
camp1
:
valor1
,
camp2
:
valor2
}
)
Ejemplo
Consultamos los libros de la autora
Sara Mesa
con más de 200 páginas:
db.llibres.
find
(
{
autor
:
'Sara Mesa'
,
nombre_pagines
:
{
* `$gt`
:
200
}
}
)
## Operadores lógicos
Podemos utilizar los siguientes operadores lógicos para combinar criterios de filtrado:
* `$and`
* `$or`
* `$not`
* `$and`
Consultamos los libros de la autora
Sara Mesa
con menos de 200 páginas:
db.llibres.
find
(
{
* `$and`
:
[
{
autor
:
'Sara Mesa'
}
,
{
nombre_pagines
:
{
* `$lt`
:
200
}
}
]
}
)
* `$not`
Consultamos los libros que no son de la autora
Sara Mesa
:
db.llibres.
find
(
{
autor
:
{
* `$not`
:
{
* `$eq`
:
'Sara Mesa'
}
}
}
)
## Operadores con strings
MongoDB apoya
expresiones regulares
para filtrar strings:
db.collection.
find
(
{
camp
:
/expressió/
}
)
db.collection.
find
(
{
camp
:
{
* `$regex`
:
'expressió'
}
}
)
Ejemplo
Consultamos los libros que contienen la palabra 'familia' en el resumen:
db.llibres.
find
(
{
resum
:
/família/
}
)
## Operadores con arrays
Podemos utilizar los siguientes operadores para filtrar arrays:
* `$in`
: contiene alguno de los elementos (
in
).
* `$nin`
: no contiene ninguno de los elementos (
not in
).
* `$all`
: contiene todos los elementos (
all
).
* `$size`
: tiene el tamaño (
size
).
* `$elemMatch`
: contiene algún elemento que cumpla los criterios (
element match
).
* `$in`
Consultamos los libros que son del género
novel·la
o
poesia
:
db.llibres.
find
(
{
genere
:
{
* `$in`
:
[
'novel·la'
,
'poesia'
]
}
}
)
* `$all`
Consultamos los libros que son de los géneros
ciència-ficció
y
bèl·lic
:
db.llibres.
find
(
{
genere
:
{
* `$all`
:
[
'ciència-ficció'
,
'bèl·lic'
]
}
}
)
* `$elemMatch`
Consultamos los libros que tienen un género que contiene la palabra
ficció
:
db.llibres.
find
(
{
genere
:
{
* `$elemMatch`
:
{
* `$regex`
:
'ficció'
}
}
}
)
## Operadores con fechas
Podemos utilizar los siguientes operadores para filtrar fechas:
## Ordenación
Podemos ordenar los documentos de una consulta con la función
sort
:
db.collection.
find
().
sort
(
{
camp
:
1
}
)
El valor del objeto pasado en la función
sort
es:
1
: ordenación ascendente (
ascendente
).
-1
: ordenación descendente (
descendente
).
Se pueden ordenar por múltiples campos añadiéndolos al objeto:
db.collection.
find
().
sort
(
{
camp1
:
1
,
camp2
:
-1
}
)
Ejemplo
Consultamos los libros ordenados por fecha de publicación de forma descendente:
db.llibres.
find
().
sort
(
{
data_publicacio
:
-1
}
)
## Selección de campos
La función
find
acepta un segundo parámetro para seleccionar los campos que queremos mostrar:
db.collection.
find
(
{
}
,
{
camp1
:
1
,
camp2
:
1
}
)
Los valores para seleccionar los campos son:
1
: incluir el campo (
include
).
0
: excluir el campo (
exclude
).
El comportamiento es el siguiente:
Si no se especifica este campo, se mostrarán todos los campos de los documentos.
Si se especifica este campo, por defecto sólo se mostrarán los campos
_id
y los que se especifican con el valor
1
.
Ejemplo
Consultamos los títulos de los libros de la autora
Sara Mesa
sin incluir el identificador:
db.llibres.
find
(
{
autor
:
'Sara Mesa'
}
,
{
_id
:
0
,
titol
:
1
}
)
[
{
titol
:
'La familia'
}
,
{
titol
:
'Un amor'
}
]
## Operadores de comparación:
* `$gt`
,
* `$gte`
,
* `$lt`
,
* `$lte`
.
## Operadores de tiempo:
$year
,
$month
,
$dayOfMonth
,
$dayOfWeek
.
* `$gte y $lte`
Consultamos los libros publicados entre las fechas
2022-06-01
y
2022-12-31
:
db.llibres.
find
(
{
data_publicacio
:
{
* `$gte`
:
new
Date
(
'2022-06-01'
)
,
* `$lte`
:
new
Date
(
'2022-12-31'
)
}
}
)
