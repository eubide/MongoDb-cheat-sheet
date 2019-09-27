
## GEOspatial Index

### Store an Index
```sh
db.collection.ensureIndex({location:'2D', type:1})
```
The example above will create a 2D geospatial index"

```sh
db.collection.ensureIndex({location:'2DSphere', type:1})
```
The example above will create a 2D geospatial with lat and long"

### Find the closest points
```sh
db.collection.find({location:{$near:[50,50]}})

db.collection.find({location:{$near:[50,50]}}).limit(3) // Get the closest 3
```
