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
