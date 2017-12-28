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

# StockGroup

## Add FavoriteStock Group

> Return value

```json
  { 
    "stock_group_id": 1001
  }
```

Add stock group.
<aside class="notice">Require user login.</aside>

### HTTP Request

`POST api/v1/stock_group/create`

### Query Parameters

Parameter | Reqiured | Datatype | Description
--------- | -------- | -------- | -----------
favorite_stock_id | true | integer | お気に入り銘柄 ID 
name | true | string | グループ名前

## Ungroup StockGroup

> Return value:

```json
  {
    "stock_groups": [
      { "id": 1, "name": "left_group_1" },
      { "id": 2, "name": "left_group_2" }
    ]
  }
```

Remove a group from one of the favorite_stock belongs to current user.
Return value indicates the group remain with the favorite_stock.
<aside class="notice">Require user login.</aside>

### HTTP Requst

`DELETE api/v1/stock_group/:group_id/ungroup`

### Query Parameters

Parameter | Reqiured | Datatype | Description
--------- | -------- | -------- | -----------
favorite_stock_id | true | integer | お気に入り銘柄 ID 
stock_group_id | true | integer | グループ ID

## Search StockGroup

> Return value:

```json
  {
    "results": [
      { "name": "match_group1", "id": 1 },
      { "name": "match_group2", "id": 2 }
    ]
  }
```

Search StockGroups that have been created by current user.
<aside class="notice">Require user login.</aside>

### HTTP Requst

`GET api/v1/stock_group/search`

### Query Parameters

Parameter | Reqiured | Datatype | Description
--------- | -------- | -------- | -----------
term | true | string | 検索キーワード

## Delete StockGroup

Delete a StockGroup that belongs to current user.
<aside class="notice">Require user login.</aside>

> Return value:

```json
  "stock_groups": [
    { "id": 1, "name": "left_group_1" }, 
    { "id": 2, "name": "left_group_2" }
  ]
```

### HTTP Request

`DELETE api/v1/stock_groups/:id`

### Query Parameters

Parameter | Reqiured | Datatype | Description
--------- | -------- | -------- | -----------
id | true | integer | 銘柄グループ ID

