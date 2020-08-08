# Insert Operation Commands
This File consist curl commands of Insert opeation for Elastic search that we mostly used
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
