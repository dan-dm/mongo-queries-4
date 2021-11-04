# mongo-queries-4

1. Insertar los documentos de la colección media.json en una base de datos llamada «media» en una única
operación.

```
db.getCollection("media").find({})
```

2. Actualizar el documento que hace referencia a la película «Matrix», de manera que se cambia su estructura a:
{“tipo”: “DVD”,
“Titulo”: “Matrix”,
“estreno”: 1999,
“genero”:”accion”
}

```
db.media.updateOne( 
// Query
{Titulo: "Matrix" },
// Set
{$set: 
    {
        tipo: "DVD",
        Titulo: "Matrix",
        estreno: 1999,
        genero:"accion"
     }
})
```

3. Considerar un nuevo documento para la colección media:
{“tipo”: “Libro”,
“Titulo”: “Constantinopla”,
“capitulos”:12,
“leidos”:3
}
Añadir el documento a la colección media y a continuación incrementar en 5 unidades el valor de la clave
«leídos».
```
db.media.insertOne(
    {
        tipo: "Libro",
        Titulo: "Constantinopla",
        capitulos:12,
        leidos:3
    }
)

db.media.updateOne(
    {Titulo: "Constantinopla"},
    {
        $inc: {leidos:5}
    }
)
```

EJERCICIO 4(CONT)
Actualización de Documentos
4. Actualizar el documento referido a la película «Matrix» cambiando el valor de la clave «género» a «ciencia
ficción».

```
db.media.updateOne(
    {Titulo:"Matrix43"},
    {$set: {genero: "ciencia ficción"}}
)
```

5. Actualizar el documento referido al libro «Java para todos» de manera que se elimine la clave «editorial».

```
db.media.updateOne(
    {titulo: "Java para todos"},
    {$unset: {editorial: ""}}
)
```

6. Actualizar el documento referido al libro «Java para todos» añadiendo el autor «María Sancho» al array de
autores.

```
db.media.updateOne(
    {titulo: "Java para todos"},
    {$push: {Autor: "María Sancho"}}
)
```

7. Actualizar el documento referido a la película «Matrix» añadiendo al array «actores» los valores de
«Antonio Banderas» y «Brad Pitt» en una única operación.

```
db.media.updateOne(
    {Titulo: "Matrix"},
    {$push: {actores: { $each: ["Antonio Banderas", "Brad Pitt"]}}}
)
```

8. Actualizar el documento referido a la película «Matrix» añadiendo al array «actores» los valores «Joe
Pantoliano», «Brad Pitt» y «Natalie Portman» en caso de que no se encuentren, y si se encuentran no se
hace nada.

```
db.media.updateOne(
    {Titulo: "Matrix"},
    {$addToSet: {actores: { $each: ["Joe Pantoliano", "Brad Pitt", "Natalie Portman"]}}}
)
```

9. Actualizar el documento referido a la película «Matrix» eliminando del array el primer y último actor.

```
db.media.updateOne(
    {Titulo: "Matrix"},
    {$pop: {actores:-1,actores:1}}
)
```

10. Actualizar el documento referido a la película «Matrix» añadiendo al array actores los valores «Joe
Pantoliano» y «Antonio Banderas».

```
db.media.updateOne(
    {Titulo: "Matrix"},
    {$push:{actores:{$each:["Joe Pantoliano","Antonio Banderas"]}}}
)
```

EJERCICIO 4(CONT)
Actualización de Documentos
11. Actualizar el documento referido a la película «Matrix» eliminado todas las apariciones en el array
«actores» de los valores «Joe Pantoliano» y «Antonio Banderas».

```
db.media.updateOne(
  {Titulo:"Matrix"},
  {$pullAll:{actores:[
    "Joe Pantoliano",
    "Antonio Banderas"]}})
```

12. Actualizar el documento referido al disco «Recuerdos» y añadir una nueva canción al array «canciones»:
{“cancion”:5,
“titulo”: “El atardecer”,
“longitud”: “6:50”
}

```
db.media.updateOne(
    {Titulo: "Recuerdos"},
    {$push:{canciones:{cancion:5,titulo: "El atardecer",longitud:"6:50"}}}
)
```

13. Actualizar el documento referido al disco «Recuerdos» de manera que la canción «El atardecer» tenga
asignado el número 3 en vez de 5.

```
db.media.updateOne(
    {$and:[
        {Titulo: "Recuerdos"},
        {"canciones.cancion": 5}
        ]
    },
    {$set:{"canciones.$.cancion": 3}}
)
```

14. Actualizar el documento referido al disco «Recuerdos» de manera que en una sola operación se cambia el
nombre del artista a «Los piratillas» y se muestre el documento resultante.

```
db.media.findOneAndUpdate(
    {Titulo: "Recuerdos"},
    {$set:{Artista:"Los Piratillas"}},
    {returnNewDocument:true}
)
```

15. Renombrar el nombre de la colección «media» a «multimedia».

```
db.media.renameCollection("multimedia")
```
