# Index Commands
This File consist curl commands on Elastic search index that we mostly used
***
##### - Note: Below two field you can replace with yours value accordingly <br/>
- indexName = Your Index name that present in your elastic search.
- typeName = Your type name associated with that index. From elasticSearch v6 onwards type name is by default "_doc" and from v7 you don't have any mapping type name present in elastic search.
- aliasName = Your alias name that present in your elastic search.
***

### Create index
   ```javascript
  curl -X PUT "localhost:9200/indexName?pretty"
  ```

### Create index with additional settings [Update following json with your configurations]
  ```javascript
  curl -X PUT "localhost:9200/indexName?pretty" -H 'Content-Type: application/json' -d'
  {
      "settings" : {
          "index" : {
              "number_of_shards" : 3, 
              "number_of_replicas" : 2 
          }
      }
  }
  '
  ```
  
### Create index with mappings [Update following json with your mappings]
  ```javascript
  curl -X PUT "localhost:9200/indexName?pretty" -H 'Content-Type: application/json' -d'
  {
      "mappings" : {
          "_doc" : {
             "properties" : {
                  "field1" : { "type" : "text" }
              }
          }
      }
  }
  '
  ```
  

### Get list of indices from Elastic Search
  ```javascript
  curl -X GET "http://localhost:9200/_cat/indices?pretty"
  ```
  
### Get mappings for given indices
  ```javascript
  curl -X GET "http://localhost:9200/indexName/_mapping?pretty"
  ```

### Delete Index
  ```javascript
  curl -X DELETE "http://localhost:9200/indexName?pretty"
  ```

### Copy all documents from one index to another index (Reindexing)
###### Suppose if you want to copy all documents from index_v1 to index_v2, then query will be,
  ```javascript
  curl -X POST "http://localhost:9200/_reindex?pretty" -H 'Content-Type: application/json' -d'
  {
    "source": {
      "index": "index_v1"
    },
    "dest": {
      "index": "index_v2"
    }
  }
  '
  ```
  
### Get which index point to which alias by alias name
  ```javascript
  curl -X GET "http://localhost:9200/aliasName/_alias/*?pretty"
  ```
  
### Add alias to index
###### - Add Single alias
  ```javascript
  curl -X PUT "http://localhost:9200/indexName/_alias/aliasName?pretty"
  ```
###### - Add Multiple alias to different indexes
  ```javascript
  curl -X POST "http://localhost:9200/_aliases?pretty" -H 'Content-Type: application/json' -d'
  {
    "actions" : [
      { "add" : { "index" : "indexName_v1", "alias" : "aliasName1" }},
      { "add" : { "index" : "indexName_v1", "alias" : "aliasName2" }},
      { "add" : { "index" : "indexName_v2", "alias" : "aliasName1" }}
    ]
  }
  '
  ```

### Remove alias from index
###### - Remove single alias
  ```javascript
  curl -X POST "http://localhost:9200/_aliases?pretty" -H 'Content-Type: application/json' -d'
  {
      "actions": [
          { "remove": { "index": "indexName", "alias": "aliasName" }}
      ]
  }
  '
  ```
###### - Remove multiple aliases from different indexes
  ```javascript
  curl -X POST "http://localhost:9200/_aliases?pretty" -H 'Content-Type: application/json' -d'
  {
      "actions": [
          { "remove": { "index": "indexName_v1", "alias": "aliasName1" }},
          { "remove": { "index": "indexName_v2", "alias": "aliasName1" }},
          { "remove": { "index": "indexName_v1", "alias": "aliasName2" }}
      ]
  }
  '
  ```
 
