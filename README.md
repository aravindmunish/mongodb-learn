## Mongo DB

- [ ] RDBMS         - Tables         - Rows                - Column
- [x] Mongo DB         - Collections         - Documents        - Fields

-  Documents are Case Sensitive

-  Open Mongo DB shell        - C:\Program Files\MongoDB\Server\5.0\bin\mongo.exe
-  Exit Mongo DB                - ctrl+d

```
show databases (or) show dbs
use newDB
db.createCollection('profile') (or) db.profile.insert()
show collections
db.createCollection('students') (or) db.students.insert()
show collections
db.profile.drop()
show collections
db.students.drop()
show collections
db.dropDatabase()
show dbs

db.profile.insert()
db.profile.insert({Name:"vasanth", Age:"38"})
db.profile.find()
        { "_id" : ObjectId("61e89b67ffe688be5b4bd57c"), "Name" : "vasanth",  "Age":"38" }

        ObjectId - Primary Key - 12 bytes hexadecimal - 12-byte Field Of BSON type(Binary JSON)
                        4 - Unix Timestamp of the document (sec)
                        3 - Machine Identifier (ID) on which the MongoDB server is running
                        2 - Process ID
                        3 - Counter - Increment the objectid - Incrementing value starting with a random number
                        
show dbs
```

# mongodb

All mongoDB commands

## Topics

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
    
    3. `db.users.find( { status: { $in: [ "P", "D" ] } } )` - returns collection where status equals either "P" or "D".
    
    4. `db.users.find( { status: "A", age: { $lt: 30 } } )` - documents in the users collection where the status equals "A" and age is          less than ($lt) 30 ( **AND** Condition ).
    
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
| $inc                | Increments the value of the field by the specified amount.                                                           |
| $mul                | Multiplies the value of the field by the specified amount.                                                           |
| $rename            | Renames a field.                                                                                                     |
| $setOnInsert  | Sets the value of a field if an update results in an insert of a document. Has no effect on update operations that   |                 |  modify existing documents.                                                                                          | 
| $set                | Sets the value of a field in a document.                                                                             |
| $unset            | Removes the specified field from a document.                                                                         | 
| $min                | Only updates the field if the specified value is less than the existing field value.                                 |
| $max                | Only updates the field if the specified value is greater than the existing field value.                              |
| $currentDate        | Sets the value of a field to current date, either as a Date or a Timestamp.                                          |

## Removing Documents

| Method                        | Description                                                                                          |
|-------------------------------|------------------------------------------------------------------------------------------------------|
| db.collection.remove()            | Delete a single document or all documents that match a specified filter.                             |
| db.collection.deleteOne()     | Delete at most a single document that match a specified filter even though multiple documents may    | |                               | match the specified filter.                                                                          |
| db.collection.deleteMany()    | Delete all documents that match a specified filter.                                                  |

    
## Indexes

1. `db.collection.createIndex( <key and index type specification>, <options> )`  -  creates an index if an index of the same specification does not already exist.

    Example:
        NOTE:  1 - Ascending Index
              -1 - Descending Index
    
    1. Create an Ascending Index
    
            `db.collection.createIndex(
                { dateOfBirth : 1 }, function(err, result) {
              });`
              
    2. Create a Descending Index 
    
            `db.collection.createIndex(
                { dateOfBirth : -1 }, function(err, result) {
              });`
         
    3. Create a Compound Index 
    
            `db.collection.createIndex(
                { lastName : -1, dateOfBirth : 1 }, function(err, result) {
              });`
              
    4. Create a Text Index
    
            `db.collection.createIndex(
                { comments : "text" }, function(err, result) {
              });`
              
    5. Create a Hashed Index
    
            `db.collection.createIndex(
                { timestamp : "hashed" }, function(err, result) {
              });`
        
    6. Create a Unique Index
    
            `collection.createIndex(
                { lastName : -1, dateOfBirth : 1 },
                { unique:true },
                function(err, result) {
              });`
              
    7. Create a Partial Index
    
            `collection.createIndex(
                { lastName : 1, firstName: 1 },
                { partialFilterExpression: { points: { $gt: 5 } } },
                function(err, result) {
              });`
        
              
2. `db.collection.dropIndex()` - Remove an index

3. `db.collection.dropIndexes()` - Remove All Indexes

4. `db.accounts.reIndex()` - Rebuild all indexes on a collection in a single operation. This operation drops all indexes, including the     _id index, and then rebuilds all indexes.

5. `db.collection.getIndexes()` - To return a list of all indexes on a collection
 
---------------------

# MongoDB

## Show All Databases

```
show dbs
```

## Show Current Database

```
db
```

## Create Or Switch Database

```
use atlas
```

## Drop

```
db.dropDatabase()
```

## Create Collection

```
db.createCollection('posts')
```

## Show Collections

```
show collections
```

## Insert Row

```
db.posts.insert({
  title: 'Post One',
  body: 'Body of post one',
  category: 'News',
  tags: ['news', 'events'],
  user: {
    name: 'John Doe',
    status: 'author'
  },
  date: Date()
})
```

## Insert Multiple Rows

```
db.posts.insertMany([
  {
    title: 'Post Two',
    body: 'Body of post two',
    category: 'Technology',
    date: Date()
  },
  {
    title: 'Post Three',
    body: 'Body of post three',
    category: 'News',
    date: Date()
  },
  {
    title: 'Post Four',
    body: 'Body of post three',
    category: 'Entertainment',
    date: Date()
  }
])
```

## Get All Rows

```
db.posts.find() (or) db.posts.find().pretty()
```

## Find Rows

```
db.posts.find({ category: 'News' })
```

## Sort Rows

```
# asc
db.posts.find().sort({ title: 1 })
# desc
db.posts.find().sort({ title: -1 })
```

## Count Rows

```
db.posts.find().count()
db.posts.find({ category: 'News' }).count()
```

## Limit Rows

```
db.posts.find().limit(2)
```

## Chaining

```
db.posts.find().limit(2).sort({ title: 1 })
```

## Foreach

```
db.posts.find().forEach(function(doc) {
  print("Blog Post: " + doc.title)
})
```

## Find One Row

```
db.posts.findOne({ category: 'News' })
```

## Find Specific Fields

```
db.posts.find({ title: 'Post One' }, {
  title: 1,
  author: 1
})
```

## Update Row

```
db.posts.update({ title: 'Post Two' },
{
  title: 'Post Two',
  body: 'New body for post 2',
  date: Date()
},
{
  upsert: true
})
```

## Update Specific Field

```
db.posts.update({ title: 'Post Two' },
{
  $set: {
    body: 'Body for post 2',
    category: 'Technology'
  }
})
```

## Increment Field (\$inc)

```
db.posts.update({ title: 'Post Two' },
{
  $inc: {
    likes: 5
  }
})
```

## Rename Field

```
db.posts.update({ title: 'Post Two' },
{
  $rename: {
    likes: 'views'
  }
})
```

## Delete Row

```
db.posts.remove({ title: 'Post Four' })
```

## Delete Empty Row

```
db.posts.updateMany({"name": ""}, { $unset : {"name" : 1 }});

```

## Sub-Documents

```
db.posts.update({ title: 'Post One' },
{
  $set: {
    comments: [
      {
        body: 'Comment One',
        user: 'Mary Williams',
        date: Date()
      },
      {
        body: 'Comment Two',
        user: 'Harry White',
        date: Date()
      }
    ]
  }
})
```

## Find By Element in Array (\$elemMatch)

```
db.posts.find({
  comments: {
     $elemMatch: {
       author: 'Mary Williams'
       }
    }
  }
)
```

## Add Index

```
db.posts.createIndex({ title: 'text' })
```

## Text Search

```
db.posts.find({
  $text: {
    $search: "\"Post O\""
    }
})
```

## Greater & Less Than

```
db.posts.find({ views: { $gt: 2 } })
db.posts.find({ views: { $gte: 7 } })
db.posts.find({ views: { $lt: 7 } })
db.posts.find({ views: { $lte: 7 } })
        
 














        


