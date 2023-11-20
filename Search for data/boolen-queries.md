# Querying with boolean logic

## `must`

Query clauses added within the `must` occurrence type are required to match.

```
GET /products/_search
{
  "query": {
    "bool": {
      "must": [
        {
          "term": {
            "tags.keyword": "Alcohol"
          }
        }
      ]
    }
  }
}
```

**SQL:** `SELECT * FROM products  WHERE tags IN ("Alcohol")`

## `must_not`

Query clauses added within the `must_not` occurrence type are required to _not_ match.

```
GET /products/_search
{
  "query": {
    "bool": {
      "must": [
        {
          "term": {
            "tags.keyword": "Alcohol"
          }
        }
      ],
      "must_not": [
        {
          "term": {
            "tags.keyword": "Wine"
          }
        }
      ]
    }
  }
}
```

**SQL:** `SELECT * FROM products WHERE tags IN ("Alcohol") AND tags NOT IN ("Wine")`

## `should`

Matching query clauses within the `should` occurrence type boost a matching document's relevance score.

```
GET /products/_search
{
  "query": {
    "bool": {
      "must": [
        {
          "term": {
            "tags.keyword": "Alcohol"
          }
        }
      ],
      "must_not": [
        {
          "term": {
            "tags.keyword": "Wine"
          }
        }
      ],
      "should": [
        {
          "term": {
            "tags.keyword": "Beer"
          }
        }
      ]
    }
  }
}
```
## `minimum_should_match`

Since only `should` query clauses are specified, at least one of them must match.

```
GET /products/_search
{
  "query": {
    "bool": {
      "should": [
        {
          "term": {
            "tags.keyword": "Beer"
          }
        },
        {
          "match": {
            "name": "beer"
          }
        }
      ]
    }
  }
}

```
## `filter`

Query clauses defined within the `filter` occurrence type must match.
This is similar to the `must` occurrence type. The difference is that
`filter` query clauses do not affect relevance scores and may be cached.

```
GET /products/_search
{
  "query": {
    "bool": {
      "filter": [
        {
          "term": {
            "tags.keyword": "Alcohol"
          }
        }
      ]
    }
  }
}
```