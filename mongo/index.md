# index
## create
```
 db.collectionName.createIndex( { "$**": "text" } ) # 全文索引 def
 db.collectionName.createIndex( { "$field": "text" }) # default_language　企业版才支持中文...
```
## drop
```
  db.collectionName.dropIndex('indexName')
```
## get
```
  db.collectionName.getIndexes()
```
## log
```
db.setLogLevel() 
# db.setLogLevel(3,'query')
```
