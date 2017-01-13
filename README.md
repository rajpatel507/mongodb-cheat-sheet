# mongodb-cheat-sheet

All mongoDB commands in compact formate.

## Table of Contents

- [mongo Shell](#mongo-shell)
- [insert Document](#insert-document)
- [Query Documents](query-documents)


## mongo shell

1. `db` - display the database you are using.

2. `use <database>` - To switch databases.


## insert Document

1. `db.<collection_name>.insertOne(<document>)` -  inserts a single document into a collection.

    Example:
    `db.users.insertOne(
       {
          name: "sue",
          age: 19,
          status: "P"
       }
    )`
    

2. `db.<collection_name>.insertMany(<document>)` - inserts multiple documents into a collection.

    Example:
    `db.users.insertMany(
       [
         { name: "bob", age: 42, status: "A", },
         { name: "ahn", age: 22, status: "A", },
         { name: "xi", age: 34, status: "D", }
       ]
    )`


3. `db.<collection_name>.insertOne(<document>)` - inserts a single document or multiple documents into a collection. To insert a single document, pass a document to the method; to insert multiple documents, pass an array of documents to the method.


## Query Documents

1. `db.collection.find( <query filter>, <projection> )` - to read documents from a collection.
    
    Example:
    
    1. `db.users.find()` or `db.users.find({})` -  returns all documents in the collection.
    
    2. `db.users.find( { status: "A" } )` - returns all documents where the status field has the value "A".
    
    3.  `db.users.find( { status: { $in: [ "P", "D" ] } } )` - returns collection where status equals either "P" or "D".
    
    4.  `db.users.find( { status: "A", age: { $lt: 30 } } )` - documents in the users collection where the status equals "A" and age is          less than ($lt) 30 ( **AND** Condition ).
    
    5.  `db.users.find(
       {
         $or: [ { status: "A" }, { age: { $lt: 30 } } ]
       }
        )` - all documents in the collection where the status equals "A" or age is less than ($lt) 30 ( **OR** condition).
        
    6.  `db.users.find( { favorites: { artist: "Picasso", food: "pizza" } } )` - all documents where the favorites field is an embedded          document that contains only the fields artist equal to "Picasso" and food equal to "pizza", in that order.
    
    7.  `db.users.find( { "favorites.artist": "Picasso" } )` - all documents where the favorites field is an embedded document that               includes the field artist equal to "Picasso" and may contain other fields.
    
    8.  `db.users.find( { badges: [ "blue", "black" ] } )` - all documents where the field badges is an array that holds exactly two                elements, "blue", and "black", in this order.
    
    9.  `db.users.find( { finished: { $elemMatch: { $gt: 15, $lt: 20 } } } )` - all documents where the finished array contains **at                least one** element that is greater than ($gt) 15 and less than ($lt) 20.
    

2.  `db.collection.findOne(query, projection)` -  Returns one document that satisfies the specified query criteria. If multiple             documents satisfy the query, this method returns the first documen.
        
    
