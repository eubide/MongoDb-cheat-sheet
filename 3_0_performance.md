# MongoDb Diver:

### Create Index


```sh
db.collection.createIndex({sample_id:1})
```
*The example above will create an index sample_id accending"*

### Get Index

```sh
db.collection.getIndexes()
```
*The example above will show all the indexes within the document (it works with MMAP and WIRED TIGER)"*

### Remove Index

```sh
db.collection.dropIndex({sample_id:1})
```
*The example above will remove the index sample_id accending"*

### Getting size of your index

```sh
db.collection.stats()
db.collection.totalIndexSize() // Shortcut
```
*The example above will remove the index sample_id accending"*
