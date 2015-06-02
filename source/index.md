---
title: API Reference

language_tabs:
  - shell

search: true
---

# Introduction

The user watch list API allows registered end consumers to save catalog assets to be watched at a later time. Watch list items are saved per provider and associated consumer, and may be organized into multiple watchlists.

You can view examples of calls to the API in the area to the right.

# Authentication

```shell
curl 'http://player.ooyala.com/watchlist/v2/lists?account_token=<acount_token>'
```

> Make sure to replace `<account_token>` with the one provided by the Gigya authentication service.

Our user authentication and identity management is integrated with Gigya.  Gigya is a third party vendor that handles identity management of our clients from all types of social networks such as facebook, linkedin, google plus, etc.

<aside class="warning">
The watch list API expects the <code>account_token</code> URL parameter to be included in all API requests to the server.
</aside>

# Watch Lists

## Get All Watch List Belonging To A Given User

```shell
curl 'http://player.ooyala.com/watchlist/v2/lists?account_token=<acount_token>'
```

> The above command returns JSON structured like this:

```json
{
  "watchlists": [
    {
      "watchlist_id": "0b75e04c-df68-43a5-a825-e2ec5be6be34",
      "name": "default",
      "is_default": true,
      "created_at": "1754-08-30T22:43:41.129Z",
      "updated_at": "2015-06-01T20:03:21.196Z",
      "expire_date": "0001-01-01T00:00:00Z"
    },
    {
      "watchlist_id": "55629686-674d-4737-acb2-c3c3988bf5ff",
      "name": "My list",
      "is_default": false,
      "created_at": "2015-06-01T21:39:52Z",
      "updated_at": "2015-06-01T20:03:21.196Z",
      "expire_date": "0001-01-01T00:00:00Z"
    }
  ]
}
```

This endpoint retrieves all the watch lists that belong to a given user.  The user is identified by the information encoded in the URL parameter `account_pcode`.

### HTTP Request

`GET http://player.ooyala.com/watchlist/v2/lists`

### Query Parameters

Parameter | Description | Type    | Required
--------- | ----------- | ------- | --------
account_token | Authentication token provided by Gigya | String | True

<aside class="success">
Remember — all request to the Watch List API must be authenticated!
</aside>

## Get a Specific Watch List

```shell
curl 'http://player.ooyala.com/watchlist/v2/lists/0b75e04c-df68-43a5-a825-e2ec5be6be34?account_token=<acount_token>'
```

> The above command returns JSON structured like this:

```json
{
  "watchlist_id": "0b75e04c-df68-43a5-a825-e2ec5be6be34",
  "name": "My List",
  "items": [
    {
      "item_id": "BsbjRhbjrfmdMjMQX_dnM6HGFdjH22mA",
      "position": 1,
      "created_at": "2015-05-20T22:55:34.75Z",
      "updated_at": "2015-05-20T22:55:34.75Z",
      "data": { }
    },
    {
      "item_id": "NxczRjbjqGU8DfilgyT-GvFjmdDzbD3W",
      "position": 3,
      "created_at": "2015-05-20T22:55:35.712Z",
      "updated_at": "2015-05-20T22:55:35.712Z",
      "data": { }
    },
    {
      "item_id": "Vkd3BnbjrUpdT5rkiKukzpyUIJu8AVyK",
      "position": 2,
      "created_at": "2015-05-20T22:55:36.028Z",
      "updated_at": "2015-05-20T22:55:36.028Z",
      "data": { }
    }
  ],
  "is_default": true,
  "created_at": "2015-05-20T22:55:34.748Z",
  "updated_at": "2015-06-01T20:38:18.391309792Z",
  "expire_date": "2015-06-01T20:38:18.391309792Z"
}
```

```shell
curl 'http://player.ooyala.com/watchlist/v2/lists/default?account_token=<acount_token>'
```

> The above command returns JSON structured like this:

```json
{
  "watchlist_id": "6ac935b0-ed36-4893-b428-35a02dbcca62",
  "name": "default",
  "items_ids": [
    "BsbjRhbjrfmdMjMQX_dnM6HGFdjH22mA",
    "NxczRjbjqGU8DfilgyT-GvFjmdDzbD3W",
    "Vkd3BnbjrUpdT5rkiKukzpyUIJu8AVyK",
    "VrdzFkbjrn_3g_u6xzAe59FXRazBziXv",
    "dwZHZqbjrqNbVXJNEXIl78SWru0va_WO",
    "lzcDNnbjqDkIuRooK_O-Xvo8xJeh7344",
    "xvN2IzbzqkMhjjupUVz1sBQfGQasUzCY"
  ],
  "is_default": true,
  "created_at": "2015-05-20T22:55:34.748Z",
  "updated_at": "2015-06-01T21:58:42.062186285Z",
  "expire_date": "2015-06-01T21:58:42.062186285Z"
}
```


This endpoint retrieves a specific watch list.

### HTTP Request

`GET http://player.ooyala.com/watchlist/v2/lists/:watchlist_id`

### URL Parameters

Parameter | Description | Type | Required
--------- | ----------- | ------ | --------
watchlist_id | The ID of the watch list to retrieve or the word "default" to retrive the default watch list. | UUIDv4 OR String | True
ids_only | Specify if only the items ids should be returned or all the metadata of the items should be returned along | Boolean | False

<aside class="notice">
The <code>data</code> field of each item in the response can be an arbitry JSON object.
</aside>

<aside class="notice">
When the <code>ids_only</code> URL parameter is set to true then the reponse <strong>do not</strong> contain the <code>items</code> field but the <code>items_ids</code> field.
</aside>


## Delete a Watch List

```shell
curl -XDELETE 'http://player.ooyala.com/watchlist/v2/lists/0b75e04c-df68-43a5-a825-e2ec5be6be34?account_token=<acount_token>'
```

This endpoint deletes a specific watch list.

### HTTP Request

`DELETE http://player.ooyala.com/watchlist/v2/lists/:watchlist_id`

### URL Parameters

Parameter | Description | Type | Required
--------- | ----------- | ------ | --------
watchlist_id | The ID of the watch list to retrieve or the word "default" to retrive the default watch list. | UUIDv4 OR String | True


## Clear a Watch List

```shell
curl -XDELETE 'http://player.ooyala.com/watchlist/v2/lists/0b75e04c-df68-43a5-a825-e2ec5be6be34/items?account_token=<acount_token>'
```

This endpoint deletes all items belonging to a specific watch list.

### HTTP Request

`DELETE http://player.ooyala.com/watchlist/v2/lists/:watchlist_id/items`

### URL Parameters

Parameter | Description | Type | Required
--------- | ----------- | ------ | --------
watchlist_id | The ID of the watch list to retrieve or the word "default" to retrive the default watch list. | UUIDv4 OR String | True


## Update a Watch List

```shell
curl -XPUT -H 'Content-Type: application/json' 'http://player.ooyala.com/watchlist/v2/lists/0b75e04c-df68-43a5-a825-e2ec5be6be34/items?account_token=<acount_token>' -d '
{
  "name": "My List",
  "items": [
    {
      "item_id": "FAKE",
      "position": 1
    }
  ]
}
'
```

> The above command returns JSON structured like this:

```json
{
  "watchlist_id": "55629686-674d-4737-acb2-c3c3988bf5ff",
  "name": "My List",
  "items": [
    {
      "item_id": "FAKE",
      "position": 1,
      "created_at": "2015-06-01T17:25:22.68402471-05:00",
      "updated_at": "2015-06-01T17:25:22.68402471-05:00"
    }
  ],
  "is_default": false,
  "created_at": "2015-06-01T21:39:52Z",
  "updated_at": "2015-06-01T17:25:22.679082991-05:00",
  "expire_date": "2015-06-01T19:05:22.679082991-05:00"
}
```

This endpoint deletes all items belonging to a specific watch list.

### HTTP Request

`PUT http://player.ooyala.com/watchlist/v2/lists/:watchlist_id`

### URL Parameters

Parameter | Description | Type | Required
--------- | ----------- | ------ | --------
watchlist_id | The ID of the watch list to retrieve or the word "default" to retrive the default watch list. | UUIDv4 OR String | True

# Items

## Get All Items Of A Specific Watch List

```shell
curl 'http://player.ooyala.com/watchlist/v2/lists/0b75e04c-df68-43a5-a825-e2ec5be6be34/items?account_token=<acount_token>'
```

> The above command returns JSON structured like this:

```json
{
  "items": [
    {
      "item_id": "BsbjRhbjrfmdMjMQX_dnM6HGFdjH22mA",
      "position": 1,
      "created_at": "2015-05-20T22:55:34.75Z",
      "updated_at": "2015-05-20T22:55:34.75Z"
    },
    {
      "item_id": "NxczRjbjqGU8DfilgyT-GvFjmdDzbD3W",
      "position": 3,
      "created_at": "2015-05-20T22:55:35.712Z",
      "updated_at": "2015-05-20T22:55:35.712Z"
    },
    {
      "item_id": "Vkd3BnbjrUpdT5rkiKukzpyUIJu8AVyK",
      "position": 2,
      "created_at": "2015-05-20T22:55:36.028Z",
      "updated_at": "2015-05-20T22:55:36.028Z"
    }
  ]
}
```

```shell
curl 'http://player.ooyala.com/watchlist/v2/lists/0b75e04c-df68-43a5-a825-e2ec5be6be34/items/BsbjRhbjrfmdMjMQX_dnM6HGFdjH22mA?account_token=<acount_token>&ids_only=true'
```

> The above command returns JSON structured like this:

```json
{
  "items": [
    {
      "item_id": "BsbjRhbjrfmdMjMQX_dnM6HGFdjH22mA"
    },
    {
      "item_id": "NxczRjbjqGU8DfilgyT-GvFjmdDzbD3W"
    },
    {
      "item_id": "Vkd3BnbjrUpdT5rkiKukzpyUIJu8AVyK"
    },
    {
      "item_id": "VrdzFkbjrn_3g_u6xzAe59FXRazBziXv"
    },
    {
      "item_id": "dwZHZqbjrqNbVXJNEXIl78SWru0va_WO"
    },
    {
      "item_id": "lzcDNnbjqDkIuRooK_O-Xvo8xJeh7344"
    },
    {
      "item_id": "xvN2IzbzqkMhjjupUVz1sBQfGQasUzCY"
    }
  ]
}
```

This endpoint retrieves all items belonging to a specific watch list.

### HTTP Request

`GET http://player.ooyala.com/watchlist/v2/lists/:watchlist_id/items`

### URL Parameters

Parameter | Description | Type | Required
--------- | ----------- | ------ | --------
watchlist_id | The ID of the watch list to retrieve or the word "default" to retrive the default watch list. | UUIDv4 OR String | True
ids_only | Specify if only the items ids should be returned or all the metadata of the items should be returned along | Boolean | False


## Get An Specific Item

```shell
curl 'http://player.ooyala.com/watchlist/v2/lists/0b75e04c-df68-43a5-a825-e2ec5be6be34/items/BsbjRhbjrfmdMjMQX_dnM6HGFdjH22mA?account_token=<acount_token>'
```

> The above command returns JSON structured like this:

```json
{
  "item_id": "BsbjRhbjrfmdMjMQX_dnM6HGFdjH22mA",
  "position": 1,
  "created_at": "2015-05-20T22:55:34.75Z",
  "updated_at": "2015-06-02T15:59:29.719492169Z"
}
```

This endpoint retrieves an specific item belonging to a specific watch list.

### HTTP Request

`GET http://player.ooyala.com/watchlist/v2/lists/:watchlist_id/items/:item_id`

### URL Parameters

Parameter | Description | Type | Required
--------- | ----------- | ------ | --------
watchlist_id | The ID of the watch list to retrieve or the word "default" to retrive the default watch list. | UUIDv4 OR String | True
item_id | The ID of the item retrieve | String | True

## Update An Specific Item

```shell
curl -XPUT -H 'Content-Type: application/json' 'http://player.ooyala.com/watchlist/v2/lists/default/items/BsbjRhbjrfmdMjMQX_dnM6HGFdjH22mA?account_token=<acount_token>' -d '
{
  "position": 5
}
'
```

> The above command returns JSON structured like this:

```json
{
  "item_id": "BsbjRhbjrfmdMjMQX_dnM6HGFdjH22mA",
  "position": 5,
  "created_at": "2015-05-20T22:55:34.75Z",
  "updated_at": "2015-06-02T15:59:29.719492169Z"
}
```

This endpoint updates an specific item belonging to a specific watch list.

### HTTP Request

`PUT http://player.ooyala.com/watchlist/v2/lists/:watchlist_id/items/:item_id`

### URL Parameters

Parameter | Description | Type | Required
--------- | ----------- | ------ | --------
watchlist_id | The ID of the watch list to retrieve or the word "default" to retrive the default watch list. | UUIDv4 OR String | True
item_id | The ID of the item retrieve | String | True

## Add Items To A Specific Watch List

```shell
curl -XPOST -H 'Content-Type: application/json' 'http://player.ooyala.com/watchlist/v2/lists/default/items?account_token=<acount_token>' -d '
[
  {
    "item_id": "VrdzFkbjrn_3g_u6xzAe59FXRazBziXv",
    "position": 21
  },
  {
    "item_id": "xvN2IzbzqkMhjjupUVz1sBQfGQasUzCY",
    "position": 20
  }
]
'
```

This endpoint adds a set of items (such set can have just one element) to a specific watch list.

### HTTP Request

`POST http://player.ooyala.com/watchlist/v2/lists/:watchlist_id/items`

### URL Parameters

Parameter | Description | Type | Required
--------- | ----------- | ------ | --------
watchlist_id | The ID of the watch list to retrieve or the word "default" to retrive the default watch list. | UUIDv4 OR String | True

## Delete An Item Belonging To A Specific Watch List

```shell
curl -XDELETE 'http://player.ooyala.com/watchlist/v2/lists/0b75e04c-df68-43a5-a825-e2ec5be6be34/items/BsbjRhbjrfmdMjMQX_dnM6HGFdjH22mA?account_token=<acount_token>'
```

This endpoint deletes an specific item from the watch list indicated.

### HTTP Request

`DELETE http://player.ooyala.com/watchlist/v2/lists/:watchlist_id/items/:item_id`

### URL Parameters

Parameter | Description | Type | Required
--------- | ----------- | ------ | --------
watchlist_id | The ID of the watch list to retrieve or the word "default" to retrive the default watch list. | UUIDv4 OR String | True
item_id | The ID of the item retrieve | String | True
