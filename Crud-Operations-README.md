# CRUD Operations Commands
This File consist curl commands of crud opeations for Elastic search that we mostly used
***
- Get list of indices from Elastic Search.
  ```javascript
  curl -X GET "http://localhost:9200/_cat/indices?pretty"
  ```
  
- Get mappings for given indices
  ```javascript
  curl -X GET "http://localhost:9200/indexName/_mapping?pretty"
  ```
  
- Get Count of documents that present in given index
  ```javascript
  curl -X GET "http://localhost:9200/indexName/_count?pretty"
  ```
  
- Get all data from all Elastic Search Index.
  ```javascript
  curl -X GET "http://localhost:9200/_search?pretty" -H 'Content-Type: application/json' -d'
  {
      "query": {
          "match_all": {}
      }
  }
  '
  ```
  
- Get all data from all Elastic Search Index with given Document size.
  ```javascript
  curl -X GET "http://localhost:9200/_search?size=10&pretty" -H 'Content-Type: application/json' -d'
  {
      "query": {
          "match_all": {}
      }
  }
  '
  ```
  
- Get all data from Elastic Search for given Index and type.
   ```javascript
    curl -X GET "http://localhost:9200/indexName/typeName/_search?pretty" -H 'Content-Type: application/json' -d'
    {
        "query": {
            "match_all": {}
        }
    }
    '
    ```
    
 - Get all data from Elastic Search for given Index, type and size.
    ```javascript
    curl -X GET "http://localhost:9200/indexName/typeName/_search?size=10&pretty" -H 'Content-Type: application/json' -d'
    {
        "query": {
            "match_all": {}
        }
    }
    '
    ```
    
- Get records from Elastic Search where field name is matches given value(Query parameter search)
  ```javascript
  curl -X GET "http://localhost:9200/indexName/typeName/_search?size=100&q=fieldName:fieldValue&pretty"
  ```
