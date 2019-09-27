# Mongo CRUD operations

### Basic operations

to interact with mongoDB API you need to always use the `DB` Object, followed by the `CollectionName`, followed by the action to execute.

In the following example I just want to get all the documents from a collection called `contacts`. The way you do it is using the method `find` from the collection.

```sh
db.contacts.find()

// arguments
db.contacts.find({selector}, {projection}, {options})
```
*The example above retrieve all the documents from the contacts collection in packages of 20 documents per call*

#### The find method
As mentioned in the previous example, the find methods get all the fields from the collection. To extend or modify your search criterias the find method take arguments as Json.

```sh
db.contacts.find({ name : "Leo Javier" });
```
*The example above retrieve only the documents that contains a propery called `name` with `Leo Javier` as a value. This is the `WHERE` version of MongoDB*


#### IMPORT OPERATORS
----
to import a json file into our mongoDB from the Shell follow the example below.

```sh
mongoImport -d collectionName -c CollectionName dataFile.json
```


#### UPDATE METHOD
----

Update contains a collection of operators to modify your documents whithin your collections. However, out of the box the `update` method looks that was designed to work with one document at the time. The following example will alter a the first document that the cursor find that match your search criteria (a document with a property called **name** with the value **Leo Javier**).


```sh
// This is a dangerous operation
db.contacts.update({ name : "Leo Javier" }, { age : 30 });
```
*IMPORTANT: The example above will change all the fields in the document. if this document happend to have another field, it would be removed from the document.*


#### $set operator
The set operator only affect the field specified from the document, and if the field doesn't exist it will create the new field and assing the new value (in this case 30).
```sh
// This is a safe
db.contacts.update({ name : "Leo Javier" }, { age : { $set : 30 } });
```
*This is a more reliable operation. It will only modify the property specified with the `$set` operator*

in Order to alter all the fields in your collection you must pass an empty object as an the first argument. and set the flag `multi` to true.

```sh
// the empty object {}, is equivalent to All
db.contacts.update({}, { $set : {age : 30 }}, {multi: true});
```
*The example above will add the age item with the value 30 to every document within the collection*


#### $inc operator
This operator increment the current value of a field by the value specified. If the field doesn't exist, it would create a new field with the value specified
```sh
// This is a safe
db.contacts.update({ name : "Leo Javier" }, { $inc : { age : 1 } });
```
*This is a more reliable operation. It will only modify the property specified with the `$set` operator*

#### $unset operator
This operator is often used to change the current schema of a document in a collection

```sh
// remove the field "age" ant its value from the document
db.contacts.update({ name : "Leo Javier" }, { $unset { age : 30 }});
```

#### Array operators
These operators mimic the same methods available for an array in Javascript, plus a few others.
* **$push**: add a new item to the array
* **$pop**: remove the last item to the array (using -1 as a value remove the first value)
* **$pushAll**: add a new set of items(needs to be provided as an array) to the array
* **$pull**: this operator will remove the value referenced regardless its position within the array
* **$pullAll**: Just like the `$pushAll` operator takes and array of values to remove
* **$addToSet**: behaves as the `$push` but if the item and value exists, it doesn't do anything.


```sh
// Method $push
db.array.update({ name : "Leo Javier" }, { $push : { item : 30 }});

// Method $pop
db.array.update({ name : "Leo Javier" }, { $pop : { item : 30 }});

// Method $pushAll
db.array.update({ name : "Leo Javier" }, { $pushAll : { item : [2,23,4,34] }});
```
*NOTE: you can always access to the items in an array using the dot notation*

#### $upsert operator
This operator works as a flag. If the `$upsert` is set to true it will attempt to create a new document if it doesn't find a document that match your search criteria.

```sh
// Method $pushAll
db.array.update({ name : "Leo Javier" }, { $set : { item : [2,23,4,34] }}, {$upsert : true});
```

#### DELETE OPERATORS
----

There are two methods available to delete items or collections in MongoDb.

**remove:** this method remove a document that match your search criteria. If you pass an empty object as an argument`{}` it will delete every document in your collection one by one. However if you want to remove the whole collection, it is more efficient to use the drop method.

```sh
// This example will remove every document that contains a property younger than 40 years
db.array.remove( {age : { $lt : 40 } }) 
```

```sh
// This example will remove every document within the collection
db.array.remove({})
```

```sh
// This example will remove every the whole collection
db.array.drop({})
```
