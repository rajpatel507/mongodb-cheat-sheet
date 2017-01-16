# mongodb-cheat-sheet

All mongoDB commands in compact formate.

## Table of Contents

- [mongo Shell](#mongo-shell)
- [insert Document](#insert-document)
- [Query Documents](query-documents)
- [BSON Types](bson-types)
- [Updating Documents](updating-documents)
- [Field Update Operators](field-update-operators)
- [Removing Documents](removing-documents)
- [Indexes](indexing)



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

## BSON Types

|Type         | Value | 
|-------------|-------|
| String      |   2   |
| Array       |   4   |
| Binary Data |   5   |
| Date        |   9   | 
        

## Updating Documents

1. `db.collection.updateOne()` - Updates at most a single document that match a specified filter even though multiple documents may         match the specified filter.

2. `db.collection.updateMany()` - Update all documents that match a specified filter.

3. `db.collection.replaceOne()` - Replaces at most a single document that match a specified filter even though multiple documents may       match the specified filter.

4. `db.collection.update()` - Either updates or replaces a single document that match a specified filter or updates all documents that       match a specified filter.

5. `upsert : true` option for Update - no documents match the specified filter, then the operation creates a new document and inserts       it. If there are matching documents, then the operation modifies or replaces the matching document or documents.

## Field Update Operators

| Operator      | Description                                                                                                          |
|---------------|----------------------------------------------------------------------------------------------------------------------|
| $inc	        | Increments the value of the field by the specified amount.                                                           |
| $mul	        | Multiplies the value of the field by the specified amount.                                                           |
| $rename	    | Renames a field.                                                                                                     |
| $setOnInsert  | Sets the value of a field if an update results in an insert of a document. Has no effect on update operations that   |                 |  modify existing documents.                                                                                          | 
| $set	        | Sets the value of a field in a document.                                                                             |
| $unset	    | Removes the specified field from a document.                                                                         | 
| $min	        | Only updates the field if the specified value is less than the existing field value.                                 |
| $max	        | Only updates the field if the specified value is greater than the existing field value.                              |
| $currentDate	| Sets the value of a field to current date, either as a Date or a Timestamp.                                          |

## Removing Documents
    
## Indexes
