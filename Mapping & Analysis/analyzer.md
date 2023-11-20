# Analyzer working

## Analyzing a string with the `standard` analyzer
```
POST /_analyze
{
"text": "2 guys walk into the bar , but third one ... DUCKs!!",
"analyzer": "standard"
}
```
# How the `keyword` data type works

## Testing the `keyword` analyzer
```
POST /_analyze
{
  "text": "2 guys walk into   a bar, but the third... DUCKS! :-)",
  "analyzer": "keyword"
}
```

```
POST /_analyze
{
"text": ["string", "will merge internally"],
"analyzer": "standard"
}
```