
## GEOspatial Index


### Store an Index
```sh
db.collection.ensureIndex({word:'text'})
```
The example above will create a text index

### find text
```sh
db.collection.find({{$text:{$search:'test'}}});
```

The example above will search for the word\ "test"
