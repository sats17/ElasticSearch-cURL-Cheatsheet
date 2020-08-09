# Index Commands
This File consist curl commands on Elastic search index that we mostly used
***
##### - Note: Below two field you can replace with yours value accordingly <br/>
- indexName = Your Index name that present in your elasticsearch.
- typeName = Your type name associated with that index. From elasticSearch v6 onwards type name is by default "_doc" and <br/>
             &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; from v7 you don't have any mapping type name present in elastic search.
***
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
  curl -X POST "localhost:9200/_aliases?pretty" -H 'Content-Type: application/json' -d'
  {
      "actions": [
          { "remove": { "index": "indexName", "alias": "aliasName" }}
      ]
  }
  '
  ```
###### - Remove multiple aliases from different indexes
  ```javascript
  curl -X POST "localhost:9200/_aliases?pretty" -H 'Content-Type: application/json' -d'
  {
      "actions": [
          { "remove": { "index": "indexName_v1", "alias": "aliasName1" }},
          { "remove": { "index": "indexName_v2", "alias": "aliasName1" }},
          { "remove": { "index": "indexName_v1", "alias": "aliasName2" }}
      ]
  }
  '
  ```
 
