# Insert Operation Commands
This File consist curl commands of Insert opeation for Elastic search that we mostly used
***
##### - Note: Below two field you can replace with yours value accordingly <br/>
- indexName = Your Index name that present in your elasticsearch.
- typeName = Your type name associated with that index. From elasticSearch v6 onwards type name is by default "_doc" and <br/>
             &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; from v7 you don't have any mapping type name present in elastic search.
***
### Insert Document in index
  ```javascript
  curl -X POST "http://localhost:9200/indexName/typeName?pretty" -H 'Content-Type: application/json' -d'
  {
     "sample":"data"
  }
  '
  ```

### Bulk Insert documents from File
#####  - Sample JSON file structure.
  ```json
  {"index":{"_index":"indexName","_type":"typeName","_id":"123"}}
  {"id":123, "name":"sats17", "city":"Mumbai", "state":"Maharashtra", "country":"India" }
  ```
##### - Query
  ```javascript
  curl -X POST "http://localhost:9200/indexName/typeName/_bulk?pretty" -H 'Content-Type: application/x-ndjson' --data-binary @fileName.json
  ```
