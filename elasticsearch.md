## To check the cluster health
curl 'localhost:9200/_cat/health?v'

## get a list of nodes in our cluster
curl 'localhost:9200/_cat/nodes?v'

## List All Indices
curl 'localhost:9200/_cat/indices?v'

## create an index named "customer"
curl -XPUT 'localhost:9200/customer?pretty'

## Close
curl -XPOST http://127.0.0.1:9200/myindex/_close

## Open
curl -XPOST http://127.0.0.1:9200/myindex/_open

## put something into our customer index
curl -XPUT 'localhost:9200/customer/external/1?pretty' -d '{  "name": "John Doe" }'

## retrieve that document
curl -XGET 'localhost:9200/customer/external/1?pretty'

## Delete an Index
curl -XDELETE 'localhost:9200/customer?pretty'

## Modifying Your Data
curl -XPUT 'localhost:9200/customer/external/1?pretty' -d '{  "name": "Oscar Daniel" }'

## index a document without an explicit ID
curl -XPOST 'localhost:9200/customer/external?pretty' -d ' {  "name": "Arrianne" }'

## Updating Documents
curl -XPOST 'localhost:9200/customer/external/1/_update?pretty' -d '{  "doc": { "name": "Daniel" }}'

## Deleting Documents
curl -XDELETE 'localhost:9200/customer/external/2?pretty'



##Batch Processing

curl -XPOST 'localhost:9200/customer/external/_bulk?pretty' -d '
{"index":{"_id":"1"}}
{"name": "John Doe" }
{"index":{"_id":"2"}}
{"name": "Jane Doe" }
'
curl -XPOST 'localhost:9200/customer/external/_bulk?pretty' -d '
{"update":{"_id":"1"}}
{"doc": { "name": "John Doe becomes Jane Doe" } }
{"delete":{"_id":"2"}}
'

## Loading the Sample Dataset
curl -XPOST 'localhost:9200/bank/account/_bulk?pretty' --data-binary "@accounts.json"




## The Search API
curl 'localhost:9200/bank/_search?q=*&pretty'

curl -XPOST 'localhost:9200/bank/_search?pretty' -d '
{
  "query": { "match_all": {} }
}'

### match_all and returns only the first document Note that if size is not specified, it defaults to 10.
curl -XPOST 'localhost:9200/bank/_search?pretty' -d '
{
  "query": { "match_all": {} },
  "size": 1
}'

### match_all and returns documents 11 through 20:
curl -XPOST 'localhost:9200/bank/_search?pretty' -d '
{
  "query": { "match_all": {} },
  "from": 10,
  "size": 10
}'

### match_all and sorts the results by account balance in descending order and returns the top 10 (default size) documents.
curl -XPOST 'localhost:9200/bank/_search?pretty' -d '
{
  "query": { "match_all": {} },
  "sort": { "balance": { "order": "desc" } }
}'

###  return two fields, account_number and balance (inside of _source), from the search:
curl -XPOST 'localhost:9200/bank/_search?pretty' -d '
{
  "query": { "match_all": {} },
  "_source": ["account_number", "balance"]
}'

###  returns the account numbered 20
curl -XPOST 'localhost:9200/bank/_search?pretty' -d '
{
  "query": { "match": { "account_number": 20 } }
}'

### returns all accounts containing the term "mill" in the address
curl -XPOST 'localhost:9200/bank/_search?pretty' -d '
{
  "query": { "match": { "address": "mill" } }
}'

### returns all accounts containing the term "mill" or "lane" in the address
curl -XPOST 'localhost:9200/bank/_search?pretty' -d '
{
  "query": { "match": { "address": "mill lane" } }
}'

### a variant of match (match_phrase) that returns all accounts containing the phrase "mill lane" in the address
curl -XPOST 'localhost:9200/bank/_search?pretty' -d '
{
  "query": { "match_phrase": { "address": "mill lane" } }
}'

### two match queries and returns all accounts containing "mill" or "lane" in the address
curl -XPOST 'localhost:9200/bank/_search?pretty' -d '
{
  "query": {
    "bool": {
      "should": [
        { "match": { "address": "mill" } },
        { "match": { "address": "lane" } }
      ]
    }
  }
}'

### composes two match queries and returns all accounts that contain neither "mill" nor "lane" in the address
curl -XPOST 'localhost:9200/bank/_search?pretty' -d '
{
  "query": {
    "bool": {
      "must_not": [
        { "match": { "address": "mill" } },
        { "match": { "address": "lane" } }
      ]
    }
  }
}'

### returns all accounts of anybody who is 40 years old but don’t live in ID(aho)
curl -XPOST 'localhost:9200/bank/_search?pretty' -d '
{
  "query": {
    "bool": {
      "must": [
        { "match": { "age": "40" } }
      ],
      "must_not": [
        { "match": { "state": "ID" } }
      ]
    }
  }
}'





## Executing Filters
curl -XPOST 'localhost:9200/bank/_search?pretty' -d '
{
  "query": {
    "bool": {
      "must": { "match_all": {} },
      "filter": {
        "range": {
          "balance": {
            "gte": 20000,
            "lte": 30000
          }
        }
      }
    }
  }
}'





## Executing Aggregations
curl -XPOST 'localhost:9200/bank/_search?pretty' -d '
{
  "size": 0,
  "aggs": {
    "group_by_state": {
      "terms": {
        "field": "state"
      }
    }
  }
}'

### calculates the average account balance by state
curl -XPOST 'localhost:9200/bank/_search?pretty' -d '
{
  "size": 0,
  "aggs": {
    "group_by_state": {
      "terms": {
        "field": "state"
      },
      "aggs": {
        "average_balance": {
          "avg": {
            "field": "balance"
          }
        }
      }
    }
  }
}'

### Building on the previous aggregation, let’s now sort on the average balance in descending order:
curl -XPOST 'localhost:9200/bank/_search?pretty' -d '
{
  "size": 0,
  "aggs": {
    "group_by_state": {
      "terms": {
        "field": "state",
        "order": {
          "average_balance": "desc"
        }
      },
      "aggs": {
        "average_balance": {
          "avg": {
            "field": "balance"
          }
        }
      }
    }
  }
}'

### This example demonstrates how we can group by age brackets (ages 20-29, 30-39, and 40-49), then by gender, and then finally get the average account balance, per age bracket, per gender:
curl -XPOST 'localhost:9200/bank/_search?pretty' -d '
{
  "size": 0,
  "aggs": {
    "group_by_age": {
      "range": {
        "field": "age",
        "ranges": [
          {
            "from": 20,
            "to": 30
          },
          {
            "from": 30,
            "to": 40
          },
          {
            "from": 40,
            "to": 50
          }
        ]
      },
      "aggs": {
        "group_by_gender": {
          "terms": {
            "field": "gender"
          },
          "aggs": {
            "average_balance": {
              "avg": {
                "field": "balance"
              }
            }
          }
        }
      }
    }
  }
}'




{query: {match: {      title: {        query: 'about'      }    }  }}

{"mappings": { "properties": { "date_published": { "type":   "date", "format": "MM-dd-yyyy"  } } } }

# removing by query
POST twitter/_delete_by_query
{
  "query": { 
    "match": {
      "message": "some message"
    }
  }
}