# Delete Operation Commands
This File consist curl commands of Delete opeation for Elastic search that we mostly used
***
##### - Note: Below two field you can replace with yours value accordingly <br/>
- indexName = Your Index name that present in your elasticsearch.
- typeName = Your type name associated with that index. From elasticSearch v6 onwards type name is by default "_doc" and <br/>
             &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; from v7 you don't have any mapping type name present in elastic search.
***
### Delete Index
  ```javascript
  curl -X DELETE "http://localhost:9200/indexName?pretty"
  ```
  
### Delete Document By Id
  ```javascript
  curl -X DELETE "http://localhost:9200/indexName/typeName/id?pretty"
  ```

### Delete Documents By Query
  ###### - For root key/field
  ```javascript
  curl -X POST "http://localhost:9200/indexName/typeName/_delete_by_query?pretty" -H 'Content-Type: application/json' -d'
  {
    "query": {
      "match": {
        "rootKey": "value that need to be deleted"
      }
    }
  }
  '
  ```
  
  ###### - For nested key/field
  ```javascript
  curl -X POST "http://localhost:9200/indexName/typeName/_delete_by_query?pretty" -H 'Content-Type: application/json' -d'
  {
    "query": {
      "match": {
        "rootKey.nestedKey": "value that need to be deleted"
      }
    }
  }
  '
  ```
  
### Delete all documents from index.
 ##### - Note: It will delete only documents from index, index and index mapping will be unchanged.
 ```javascript
 curl -X POST "http://localhost:9200/indexName/typeName/_delete_by_query?pretty" -H 'Content-Type: application/json' -d'
 {
   "query": {
       "match_all": {}
   }
 }
 '
 ```
