# API Design Exercise - Coffee
======

## How to access the resource

### Introduction

You are going to build a front-end for the coffee-api backend. Coffees have three attributes: name, notes, and origin (all three are strings.)

### Accessing the resource

Coffee-API does NOT follow RESTful conventions. The endpoint for retrieving an index of all available coffees is <http://localhost:3000/coffee>. The expected result from a GET request to this address is a JSON object, with this structure:
```
[
  {
    "id": 1,
    "name": "Summer Cowboy",
    "notes": "mild, slick, kiwi, clove, carbon",
    "origin": "Aceh, Sumatra",
    "created_at": "2019-07-15T17:46:32.265Z",
    "updated_at": "2019-07-15T17:46:32.265Z"
  }, …
{
    "id": 10,
    "name": "Heart Java",
    "notes": "unbalanced, creamy, toast, medicinal, leathery",
    "origin": "Mbeya Region, Tanzania",
    "created_at": "2019-07-15T17:46:32.329Z",
    "updated_at": "2019-07-15T17:46:32.329Z"
  }
]
```


## How to filter by origin

In order to filter the results, the coffee controller will take in a parameter of origin. Note: there are no validations for this parameter. The default value is “”, so without passing in a parameter all results will be provided.

In the URL below, params[:origin]=”Gimbi”. 

<http://localhost:3000/coffee?origin=Gimbi>
```
[
  {
    "id": 166,
    "name": "Thanksgiving America",
    "notes": "balanced, full, golden raisin, walnut, meyer lemon",
    "origin": "Gimbi, Ethiopia",
    "created_at": "2019-07-15T17:47:39.217Z",
    "updated_at": "2019-07-15T17:47:39.217Z"
  },
  {
    "id": 179,
    "name": "Dark America",
    "notes": "faint, slick, carmel, orange creamsicle, liquorice",
    "origin": "Gimbi, Ethiopia",
    "created_at": "2019-07-15T17:47:39.282Z",
    "updated_at": "2019-07-15T17:47:39.282Z"
  }
]
```

In the URL below, params[:origin]=”Ethiopia”. 

<http://localhost:3000/coffee?origin=Ethiopia>

```
[
  {
    "id": 41,
    "name": "Spilt Pie",
    "notes": "clean, round, meyer lemon, graham cracker, hazelnut",
    "origin": "Wellega, Ethiopia",
    "created_at": "2019-07-15T17:47:38.464Z",
    "updated_at": "2019-07-15T17:47:38.464Z"
  },
  {
    "id": 58,
    "name": "Huggy Treat",
    "notes": "structured, coating, papaya, black currant, tamarind",
    "origin": "Wellega, Ethiopia",
    "created_at": "2019-07-15T17:47:38.543Z",
    "updated_at": "2019-07-15T17:47:38.543Z"
  },
  {
    "id": 95,
    "name": "KrebStar Nuts",
    "notes": "dense, coating, sugar cane, marshmallow, burnt sugar",
    "origin": "Ojimmah, Ethiopia",
    "created_at": "2019-07-15T17:47:38.714Z",
    "updated_at": "2019-07-15T17:47:38.714Z"
  },

… more results
```

## How to limit some number of results

In order to limit the number of results, the coffee controller will take in a parameter of limit. Note: there are no validations for this parameter. The default value is 10, so 10 results will be provided without a limit.

In the URL below, params[:limit]=2

<http://localhost:3000/coffee?limit=2>

The above GET request should provide the following:

```
[
  {
    "id": 1,
    "name": "Dark Pie",
    "notes": "faint, juicy, walnut, leafy greens, tomato",
    "origin": "El Paraiso, Honduras",
    "created_at": "2019-07-15T17:47:38.213Z",
    "updated_at": "2019-07-15T17:47:38.213Z"
  },
  {
    "id": 2,
    "name": "Veranda Solstice",
    "notes": "bright, smooth, leafy greens, cherry, fresh bread",
    "origin": "Boquete, Panama",
    "created_at": "2019-07-15T17:47:38.219Z",
    "updated_at": "2019-07-15T17:47:38.219Z"
  }
]

```

## How to specify which page of results

<http://localhost:3000/coffee?offset=8>
(gives the next 10 results from the database)

[note that the “id” begins at 81, not 1]
```
[
  {
    "id": 81,
    "name": "Café Been",
    "notes": "clean, coating, cedar, peanut, peanut",
    "origin": "Kibale, Uganda",
    "created_at": "2019-07-15T17:47:38.647Z",
    "updated_at": "2019-07-15T17:47:38.647Z"
  },
  {
    "id": 82,
    "name": "Evening Level",
    "notes": "bright, tea-like, peanut, black cherry, grassy",
    "origin": "Coban, Guatemala",
    "created_at": "2019-07-15T17:47:38.652Z",
    "updated_at": "2019-07-15T17:47:38.652Z"
  },
… and more results
```

### How to make an API query with multiple parameters

You can pass multiple parameters using the “&” in between different parameters.

For example, in order to return coffees from Ethiopia beginning on the second page of results, you would use the following URL request.
 
<http://localhost:3000/coffee?origin=Ethiopia&offset=1>

```
[
  {
    "id": 183,
    "name": "Café ",
    "notes": "dense, tea-like, milk chocolate, leathery, soy sauce",
    "origin": "Sidama, Ethiopia",
    "created_at": "2019-07-15T17:46:32.841Z",
    "updated_at": "2019-07-15T17:46:32.841Z"
  },
  {
    "id": 200,
    "name": "Evening Bean",
    "notes": "bright, velvety, burnt sugar, toast, honey",
    "origin": "Sidama, Ethiopia",
    "created_at": "2019-07-15T17:46:32.894Z",
    "updated_at": "2019-07-15T17:46:32.894Z"
  }
]
```

[Note: there are only two more results from Ethiopia on the second page, hence only two objects.]

Another example can be found here:

<http://localhost:3000/coffee?origin=Colombia&limit=1>

```
[
  {
    "id": 13,
    "name": "Kreb-Full-o Symphony",
    "notes": "mild, big, mushroom, meyer lemon, green apple",
    "origin": "Tolima, Colombia",
    "created_at": "2019-07-15T17:46:32.341Z",
    "updated_at": "2019-07-15T17:46:32.341Z"
  }
]

```
