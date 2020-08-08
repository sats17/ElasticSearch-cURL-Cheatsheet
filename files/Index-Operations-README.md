# Index Commands
This File consist curl commands on Elastic search index that we mostly used
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

### Delete Index
  ```javascript
  curl -X DELETE "http://localhost:9200/indexName?pretty"
  ```
