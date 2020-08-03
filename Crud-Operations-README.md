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
 
- Check and Return if given field is exist in index, return null if it is not present.(This will work for only outside json keys) <br />
  <sub>Note: append (.keyword) in fieldName if not works i.e(fieldName.keyword).</sub>
  ```javascript
  curl -X GET "http://localhost:9200/indexName/typeName/_search?pretty" -H 'Content-Type: application/json' -d'
  {
    "query": {
      "constant_score": {
        "filter": {
          "exists": {
            "field": "fieldName"
          }
        }
      }
    }
  }
  '
  ```
  
- Get fields from index having more than 1 value in index <br />
  <sub>Note: append (.keyword) in fieldName if not works i.e(fieldName.keyword).</sub>
  ```javascript
  curl -X GET "http://localhost:9200/indexName/typeName/_search?pretty" -H 'Content-Type: application/json' -d'
  {
    "size": 0,
    "aggs": {
      "duplicateNames": {
        "terms": {
          "field": "fieldName",
          "min_doc_count": 2,
          "size": 1000000
        }
      }
    }
  }
  '
  ```
