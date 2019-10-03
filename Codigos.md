# Creación "customer" collection

 db.customers.insert( { 
 _id: 1, 
 name:"Angela",
 surname: "Turizo", 
 mail:"some@gmail.com", 
 phone: 622622622} )
 
WriteResult({ "nInserted" : 1 })

Utilización método insert() para la creación de una colección con campos definidos por nosostros

Añadir contador de _id

Debemos añadir el contador a la par que creamos la colección

Removemos la colección creada

 show collections
customers
product
> db.customers.drop()
true
> show collections
product

# Creación coleccióncon contador de _id

 db.createCollection("customers")
{ "ok" : 1 }
> show collections
customers
product
> db.customers.insert( { "_id": "customerid", "sequencevalue": 0})
WriteResult({ "nInserted" : 1 })

# Inserción de nuevos campos en la colección

 db.customers.update( { _id: "customerid"}, { $set: { "name": "Angela", "surname": "Turizo", "mail": "some@mail.com", "phone": 622622622} }  )
WriteResult({ "nMatched" : 1, "nUpserted" : 0, "nModified" : 1 })
> db.customers.find({}).pretty()
{
        "_id" : "customerid",
        "sequencevalue" : 0,
        "mail" : "some@mail.com",
        "name" : "Angela",
        "phone" : 622622622,
        "surname" : "Turizo"
}
Utilizamos .update( { $set:{

            }
        })
para agregar nuevos campos a la colección. Debo revisar el _id, pues he podido cometer un error al no crear el campo como numérico
 # !important

 Recordar los dos ( update( { $set: { }})) métodos para añadir nuevos clientes cuando se logen!

db.customers.insert( { "_id":getNextSequenceValue("customerid"), "mail": "some2@mail.com", "name": "Roberto", "surname": "Garcia", "phone": 934444444})
WriteResult({ "nInserted" : 1 })
> db.customers.find({}).pretty()
{
        "_id" : "customerid",
        "sequencevalue" : 0,
        "mail" : "some@mail.com",
        "name" : "Angela",
        "phone" : 622622622,
        "surname" : "Turizo",
        "sequence_value" : 1
}
{
        "_id" : 1,
        "mail" : "some2@mail.com",
        "name" : "Roberto",
        "surname" : "Garcia",
        "phone" : 934444444
}
