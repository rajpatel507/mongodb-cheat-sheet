# mongodb-cheat-sheet

All mongoDB commands in compact formate.

## Table of Contents

- [mongo Shell](#mongo-shell)
- [insert Document](#insert-document)


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
