# Delete Operation Commands
This File consist curl commands of Delete opeation for Elastic search that we mostly used
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
