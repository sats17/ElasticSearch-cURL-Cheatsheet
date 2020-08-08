# Select Operation Commands
This File consist curl commands of select opeation for Elastic search that we mostly used
***
##### - Note: Below two field you can replace with yours value accordingly <br/>
- indexName = Your Index name that present in your elasticsearch.
- typeName = Your type name associated with that index. From elasticSearch v6 onwards type name is by default "_doc" and <br/>
             &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; from v7 you don't have any mapping type name present in elastic search.
***
### Get list of indices from Elastic Search.
  ```javascript
  curl -X GET "http://localhost:9200/_cat/indices?pretty"
  ```
  
### Get mappings for given indices
  ```javascript
  curl -X GET "http://localhost:9200/indexName/_mapping?pretty"
  ```
  
### Get Count of documents that present in given index
  ```javascript
  curl -X GET "http://localhost:9200/indexName/_count?pretty"
  ```
  
### Get record with id
  ```javascript
  curl -X GET "http://localhost:9200/indexName/typeName/id?_source=true&pretty"
  ```
  
### Get records from Elastic Search where field name is matches given value(Query parameter search)
  ```javascript
  curl -X GET "http://localhost:9200/indexName/typeName/_search?size=100&q=fieldName:fieldValue&pretty"
  ```
  
### Get all data from all Elastic Search Index.
  ```javascript
  curl -X GET "http://localhost:9200/_search?pretty" -H 'Content-Type: application/json' -d'
  {
     "query": {
         "match_all": {}
     }
  }
  '
  ```
  
### Get all data from all Elastic Search Index with given Document size.
  ```javascript
  curl -X GET "http://localhost:9200/_search?size=10&pretty" -H 'Content-Type: application/json' -d'
  {
     "query": {
         "match_all": {}
     }
  }
  '
  ```
  
### Get all data from Elastic Search for given Index and type.
   ```javascript
   curl -X GET "http://localhost:9200/indexName/typeName/_search?pretty" -H 'Content-Type: application/json' -d'
   {
       "query": {
         "match_all": {}
      }
   }
   '
   ```
    
### Get all data from Elastic Search for given Index, type and size.
   ```javascript
   curl -X GET "http://localhost:9200/indexName/typeName/_search?size=10&pretty" -H 'Content-Type: application/json' -d'
   {
      "query": {
        "match_all": {}
     }
   }
   '
   ```
 
### Check and Return if given field is exist in index, return null if it is not present. <br />
  ##### - Note: append (.keyword) in fieldName if below example not works. i.e: (rootKey.keyword).
  ###### - For root key/field
  ```javascript
  curl -X GET "http://localhost:9200/indexName/typeName/_search?pretty" -H 'Content-Type: application/json' -d'
  {
    "query": {
      "constant_score": {
        "filter": {
          "exists": {
            "field": "rootKey"
          }
        }
      }
    }
  }
  '
  ```
  
  ###### - For nested key/field
   ```javascript
  curl -X GET "http://localhost:9200/indexName/typeName/_search?pretty" -H 'Content-Type: application/json' -d'
  {
    "query": {
      "constant_score": {
        "filter": {
          "exists": {
            "field": "rootKey.nestedKey"
          }
        }
      }
    }
  }
  '
  ```
  
### Get fields from index having more than 1 value in index <br />
  ###### - Note: append (.keyword) on fieldName if below example not works. i.e: (fieldName.keyword).
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
  
### Get given fields from index document having more than 1 value in index <br />
  ###### - Note: append (.keyword) on fieldName if below example not works. i.e: (fieldName.keyword).
  ```javascript
  curl -X GET "http://localhost:9200/indexName/typeName/_search?pretty" -H 'Content-Type: application/json' -d'
  {
    "size": 0,
    "aggs": {
      "duplicateNames": {
        "terms": {
          "field": "fieldName",
          "min_doc_count": 2,
          "size": 8415
        },
        "aggs": {
          "hits": {
            "top_hits": {
              "_source": [
                "fieldName1",
                "fieldName2"
              ],
              "size": 6
            }
          }
        }
      }
    }
  }
  '
