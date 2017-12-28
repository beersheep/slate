---
title: Kabutan API Reference

includes:
  - errors

search: true
---

# Introduction

The API Document for Kabutan OBOE

# FavoriteStocks

## Get FavoriteStocks

> Return value:

```json
{ "favorite_stocks": 
  [ 
    { 
      "id": 1,
      "stock_code": "1301",
      "registered_on": "2017-12-05",
      "price_at_registration": 10.0,
      "name": "Nintendo",
      "prev_close_price": 20.0,
      "note": "first stock",
      "stock_groups": [
        { "name": "group1",
          "id":   1001 },
        { "name": "group2",
          "id":   1002 }
      ],
      "main_order": 1
    }, 

    {
      "id": 2
      "stock_code": "8001",
      "registered_on": "2017-12-04",
      "price_at_registration": 10.0,
      "name": "Shisedo",
      "prev_close_price": 20.0,
      "note": "second stock",
      "stock_groups": [
        { "name": "group3"
          "id":   1003 },
        { "name": "group2",
          "id":   1002 }
       ],
       "main_order": 2
    }
  ]   
}
```

Return all the favorite_stocks belong to current user.
<aside class="notice">Require user login.</aside>

### HTTP Request

`GET api/v1/favorite_stocks/all`

### Query Parameters

None

## Edit FavoriteStock

> Return value:

```json
  {
    "stock_code": "1301",
    "name": "Nintendo",
    "registered_on": "2017-10-10",
    "price_at_registration": 10.0,
    "prev_close_price": 20.0,
    "prev_close_price_updated_on": "2017-12-08",
    "note": "note",
    "stock_group": [
      { "id": 1001, "name": "Gaming" },
      { "id": 1002, "name": "Manufacturer" }
    ]
  }
```

Edit favorite_stock belongs to current_user.
<aside class="notice">Require user login.</aside>

### HTTP Request

`PUT api/v1/favorite_stock`

### Query Parameters

Parameter | Reqiured | Datatype | Description
--------- | -------- | -------- | -----------
stock_code | true | string | 銘柄コード
registered_on | true | date | 登録日
price_at_registration | true | float | 登録時株価
note | false | string | メモ
stock_group_ids | false | array_of_integer | 銘柄グループ

## Edit FavoriteStock Order

> Return value:

```json
{ "favorite_stocks": 
  [ 
    { 
      "id": 1,
      "stock_code": "1301",
      "registered_on": "2017-12-05",
      "price_at_registration": 10.0,
      "name": "Nintendo",
      "prev_close_price": 20.0,
      "note": "first stock",
      "stock_groups": [
        { "name": "group1",
          "id":   1001 },
        { "name": "group2",
          "id":   1002 }
      ],
      "main_order": 1

    }, 

    {
      "id": 2
      "stock_code": "8001",
      "registered_on": "2017-12-04",
      "price_at_registration": 10.0,
      "name": "Shisedo",
      "prev_close_price": 20.0,
      "note": "second stock",
      "stock_groups": [
        { "name": "group3"
          "id":   1003 },
        { "name": "group2",
          "id":   1002 }
       ],
      "main_order": 2
    }
  ]   
}
```

Reorder all favorite_stocks belong to current_user.
<aside class="notice">Require user login.</aside>

### HTTP Request

`PATCH api/v1/favorite_stocks/reorder`

### Query Parameters

Parameter | Reqiured | Datatype | Description
--------- | -------- | -------- | -----------
favorite_stocks | true | array | parameter keys
id | true | integer | お気に入り銘柄 ID 
order | true | integer | お気に入り銘柄順番 

# Authentication

> To authorize, use this code:

```ruby
require 'kittn'
api = Kittn::APIClient.authorize!('meowmeowmeow')
```

> Make sure to replace `meowmeowmeow` with your API key.

Kittn uses API keys to allow access to the API. You can register a new Kittn API key at our [developer portal](http://example.com/developers).

Kittn expects for the API key to be included in all API requests to the server in a header that looks like the following:
`Authorization: meowmeowmeow`

<aside class="notice">
You must replace <code>meowmeowmeow</code> with your personal API key.
</aside>

# Kittens

## Get All Kittens

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get
```

> The above command returns JSON structured like this:

```json
[
  {
    "id": 1,
    "name": "Fluffums",
    "breed": "calico",
    "fluffiness": 6,
    "cuteness": 7
  },
  {
    "id": 2,
    "name": "Max",
    "breed": "unknown",
    "fluffiness": 5,
    "cuteness": 10
  }
]
```

This endpoint retrieves all kittens.

### HTTP Request

`GET http://example.com/api/kittens`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
include_cats | false | If set to true, the result will also include cats.
available | true | If set to false, the result will include kittens that have already been adopted.

<aside class="success">
Remember — a happy kitten is an authenticated kitten!
</aside>

## Get a Specific Kitten

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get(2)
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "name": "Max",
  "breed": "unknown",
  "fluffiness": 5,
  "cuteness": 10
}
```

This endpoint retrieves a specific kitten.

<aside class="warning">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside>

### HTTP Request

`GET http://example.com/kittens/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the kitten to retrieve

## Delete a Specific Kitten

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.delete(2)
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "deleted" : ":("
}
```

This endpoint deletes a specific kitten.

### HTTP Request

`DELETE http://example.com/kittens/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the kitten to delete

