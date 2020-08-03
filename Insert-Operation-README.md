# Insert Operation Commands
This File consist curl commands of Insert opeation for Elastic search that we mostly used
***
- Insert Document in index
  ```javascript
  curl -X POST "http://localhost:9200/indexName/typeName?pretty" -H 'Content-Type: application/json' -d'
  {
     "sample":"data"
  }
  '
  ```

- Bulk Insert documents to index from File <br />
  <sub>Note: File structure should be following <br />
  {"index":{"_index":"indexName","_type":"typeName","_id":"123"}}<br/>
  {"id":123, "sample":"data"}
  </sub>
  ```javascript
  curl -X POST "http://localhost:9200/indexName/typeName/_bulk?pretty" -H 'Content-Type: application/x-ndjson' --data-binary @fileName.json
  ```
