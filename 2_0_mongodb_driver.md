# MongoDb Diver:

### Projection

#### $regex
The regex operator allow you to search for values that contain certain string.

```sh
db.collection.find({}, {$regex : { name : 'THE' } })
```
*The example above will find all the documents in the collection that contains an item or property called name, with a value that contains "THE"*
