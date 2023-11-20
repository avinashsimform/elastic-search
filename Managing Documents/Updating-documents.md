# Updating documents

## Updating an existing field ( document replces with new of same index)

```
POST /products/_update/100
{
  "doc": {
    "in_stock": 3
  }
}
```

## Adding a new field

_Yes, the syntax is the same as the above. ;-)_

```
POST /products/_update/100
{
  "doc": {
    "tags": ["electronics"]
  }
}
```

# Scripted updates

## Reducing the current value of `in_stock` by one

```
POST /products/_update/100
{
  "script": {
    "source": "ctx._source.in_stock--"
  }
}
```

## Assigning an arbitrary value to `in_stock`

```
POST /products/_update/100
{
  "script": {
    "source": "ctx._source.in_stock = 10"
  }
}
```

## Using parameters within scripts

```
POST /products/_update/100
{
  "script": {
    "source": "ctx._source.in_stock -= params.quantity",
    "params": {
      "quantity": 5
    }
  }
}
```

## Conditionally setting the operation to `noop`

```
POST /products/_update/100
{
  "script": {
    "source": """
      if (ctx._source.in_stock == 0) {
        ctx.op = 'noop';
      }
      
      ctx._source.in_stock--;
    """
  }
}
```

## Conditionally update a field value

```
POST /products/_update/100
{
  "script": {
    "source": """
      if (ctx._source.in_stock > 0) {
        ctx._source.in_stock--;
      }
    """
  }
}
```

## Conditionally delete a document

```
POST /products/_update/100
{
  "script": {
    "source": """
      if (ctx._source.in_stock < 0) {
        ctx.op = 'delete';
      }
      
      ctx._source.in_stock--;
    """
  }
}
```