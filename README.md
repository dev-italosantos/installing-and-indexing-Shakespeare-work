
# Installing and indexing Shakespeare's work


This guide provides instructions on how to install and index the complete works of William Shakespeare on your local system for convenient access and search. By following the steps below, you will be able to have quick and efficient access to all the works of the renowned English playwright.
## Prerequisites

- [Elasticsearch](https://www.elastic.co/guide/en/elasticsearch/reference/current/index.html) installed and running on your local machine.
- `wget` and `curl` commands available in your terminal.


## Step 1: Download Mapping JSON File
Run the following command to download the mapping JSON file:
```javascript
wget http://media.sundog-soft.com/es7/shakes-mapping.json
```

## Step 2: Create Index Mapping
Use `curl` to create an index in Elasticsearch with the mapping specified in the downloaded JSON file:
```javascript
curl -H 'Content-Type: application/json' -XPUT 127.0.0.1:9200/shakespeare --data-binary @shakes-mapping.json
```

## Step 3: Download Data JSON File
Now, download the Shakespearean data JSON file:
```javascript
wget http://media.sundog-soft.com/es7/shakespeare_7.0.json
```

## Step 4: Index Shakespeare Texts
Index the Shakespearean texts into Elasticsearch using the bulk API:
```javascript
curl -H 'Content-Type: application/json' -XPOST '127.0.0.1:9200/shakespeare/_bulk?pretty' --data-binary @shakespeare_7.0.json
```

## Step 5: Search Shakespearean Texts
You can now search the indexed texts. For example, to search for the famous phrase "to be or not to be", run the following `curl` command:
```javascript
curl -H 'Content-Type: application/json' -XGET '127.0.0.1:9200/shakespeare/_search?pretty' -d '
{
  "query": {
    "match_phrase": {
      "text_entry": "to be or not to be"
    }
  }
}'
```
## Reference

 - [Udemy Course Elasticsearch](https://www.udemy.com/share/103TRe3@XxOpTnRxrccx7aOU9mtXq0gSnINwHq3DvYExSjxGbmg4gmML3H8Fjpg9BUFDk8rT/)
