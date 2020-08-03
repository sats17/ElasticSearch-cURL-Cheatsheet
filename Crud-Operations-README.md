# ElasticSearch Curl CRUD Operations Commands
This Repository consist curl commands of Elastic search that we mostly used
***
- Get list of indices from Elastic Search.
  ```
  curl -X GET "http://localhost:9200/_cat/indices?pretty"
  ```
- Get mappings for given indices
  ```
  curl -X GET "http://localhost:9200/_indexName/_mapping?pretty"
  ```
- Get all data from all Elastic Search Index.
  ```
  curl -X GET "http://localhost:9200/_search?pretty" -H 'Content-Type: application/json' -d'
  {
      "query": {
          "match_all": {}
      }
  }
  '
  ```
- Get all data from all Elastic Search Index with given Document size.
  ```
  curl -X GET "http://localhost:9200/_search?size=10&pretty" -H 'Content-Type: application/json' -d'
  {
      "query": {
          "match_all": {}
      }
  }
  '
  ```
 - Get all data from Elastic Search for given Index and type.
   ```
    curl -X GET "http://localhost:9200/_indexName/_typeName/_search?pretty" -H 'Content-Type: application/json' -d'
    {
        "query": {
            "match_all": {}
        }
    }
    '
    ```
 - Get all data from Elastic Search for given Index, type and size.
    ```
    curl -X GET "http://localhost:9200/_indexName/_typeName/_search?size=10&pretty" -H 'Content-Type: application/json' -d'
    {
        "query": {
            "match_all": {}
        }
    }
    '
    ```
- Get records from Elastic Search where field name is matches given value(Query parameter search)
  ```
  curl -X GET "http://localhost:9200/_indexName/_typeName/_search?size=100&q=fieldName:fieldValue&pretty"
  ```
