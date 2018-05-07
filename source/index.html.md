---
title: API Reference

toc_footers:

search: false
---
#   
# Introduction

## API Reference

Welcome to eatsa's API!  You can use this API to access all our API endpoints to integrate with the eatsa platform.

Requests can be made to submit and update orders, get an order ETA status, as well as retrieve information about stores.  All requests should be made over SSL. All request and response bodies, including errors, are encoded in JSON.  Make sure all request bodies have content type `application/json` and are valid JSON.

## API Environments

 Environment | Endpoint
-----------------  | --------------------------------
Production | https://api.eatsa.com
Staging    | https://api.stage.eatsa.com

# Authentication

> Example Request

```shell
curl "https://api.eatsa.com/v1/stores" \
	-X GET -i -H "Content-Type:application/json; charset=utf-8" \
	-H "X-Authtoken:00000000-0000-0000-0000-000000000000"
```

Authenticate your account by including your secret key in every API Request. Please be sure to keep your API key secure, do not share your secret API key in publicly accessible areas such GitHub, client-side code, and so forth.

To authenticate an API request include the following header `-H "X-Authtoken:00000000-0000-0000-0000-000000000000"` in every request.

All API requests must be made over HTTPS. Calls made over plain HTTP will fail. API requests without authentication will also fail.

To request an authentication token for our API please contact your account manager.

# Errors


## HTTP status codes

 Code | Title | Description
--------- | ------- | -----------
200 | OK | Everything worked as expected.
201	| Created	| The resource was successfully created.
400 | Bad Request | The request was unacceptable, often due to missing a required parameter.
401 | Unauthorized | No valid API key provided.
403 | Forbidden | Forbid access regardless of authorization state
404 | Not Found | The requested resource doesn't exist.
409 | Conflict
5xx | Internal Server Error | Something went wrong on our end.


## Eatsa error codes
All error messages will return a `code` and a human readable `message`.

> Different error `code` types can be added and removed over time so you should make sure your application accepts new ones as well.

Id  | Description
--------- | ---------
INVALID_INPUT | Invalid request
FIELD_IS_REQUIRED | Validation Error
ORDER_TIMESLOT_FULL | Invalid order time slot
ORDER_TIMESLOT_PAST | Invalid order time slot
FIRE_ORDER_LOCK_TIMEOUT | Server was unable to change an order's state
STORE_CLOSED | Store closed

# Orders

This section covers our endpoints for creating an order or modifying the state of an order.

## Order object

What is an order and its status

> Example Order object

```json
{
  "id": "00000000-0000-0000-0000-000000000000",
  "ref_id": "00000000-0000-0000-0000-000000000000",  
  "store_id": "00000000-0000-0000-0000-000000000000",
  "pickup_location_id": "00000000-0000-0000-0000-000000000000",
  "pickup_location_display_name": "14",
  "created_at": "2018-04-02T21:29:25.233Z",
  "updated_at": "2018-04-02T21:29:25.681Z",
  "last_cubbied_at": "2018-04-02T21:29:25.233Z",
  "status": "scheduled",
  "user_display_name": "John D"
}
```

Parameter | Description
--------- | -----------
id | Unique ID that identifies the order.
ref_id | Reference ID for the order in the partner system.  This ID is expected to be unique.
store_id | Unique ID that identifies the store where the order was created.
pickup_location_id| Pickup station id.
pickup_location_display_name| Pickup station human readable id.
created_at | Time the order was created.
updated_at | Time the order was last updated.
last_cubbied_at | Timestamp that is updated every time an order is placed in a pickup location.
status | Status of the order, initial state is `in_queue`.
user_display_name | Name that will be displayed on the status board to inform the customer of their order.

## Order State

Status | Description
--------- | -----------
in_queue |  The order is in the active queue.
scheduled | The order is scheduled for a pickup time in the future.
ready_for_pickup | The order has been completed.
delivered_to_customer | The customer has picked up their order.
attendant_canceled | An employee has canceled an order.  

## Create an order

> Example Request

```shell
curl "https://api.eatsa.com/v1/orders" \
  -X POST -i -H "Content-Type:application/json; charset=utf-8" \
  -d '{
        "ref_id": "00000000-0000-0000-0000-000000000000",
        "user": {
          "first_name": "John",
          "last_name": "Doe"
        }
      }'
```

> Example Response

```json
{
  "id": "00000000-0000-0000-0000-000000000000",
  "ref_id": "00000000-0000-0000-0000-000000000000",  
  "store_id": "00000000-0000-0000-0000-000000000000",
  "pickup_location_id": "00000000-0000-0000-0000-000000000000",
  "pickup_location_display_name": "14",
  "created_at": "2018-04-02T21:29:25.233Z",
  "updated_at": "2018-04-02T21:29:25.681Z",
  "last_cubbied_at": "2018-04-02T21:29:25.233Z",
  "status": "scheduled",
  "user_display_name": "John D"
}
```

Creates a new order in the eatsa system. Orders have an initial status of `scheduled` if a `requested_timeslot` is provided.  If no `requested_timeslot` is provided then it is assumed the order should be delivered as soon as possible and the status will `in_queue`.  A unique id for the order is returned that can be used to track the order and modify its state accordingly.


### Endpoint

`POST https://api.eatsa.com/v1/orders`

### Request Arguments

Parameter | Required | Description
--------- | ------- | -----------
ref_id | yes  | The reference ID for the order in the partner system.  This ID is expected to be unique.
store_id | yes | Store where the order will be created
user | yes | The user object (see below)

### User object
The caller must pass `first_name` and `last_name`.

Parameter | Required | Description
--------- | ------- | -----------
first_name | yes | The first name of the user.
last_name | yes | The last name of the user.



### Response Arguments

Refer to order object


## Find an order

> Example Request

```shell
curl "https://api.eatsa.com/v1/orders/{order_id}" \
	-i -H "Content-Type:application/json; charset=utf-8"
```

> Example Response

```json
{
  "id": "00000000-0000-0000-0000-000000000000",
  "ref_id": "00000000-0000-0000-0000-000000000000",  
  "store_id": "00000000-0000-0000-0000-000000000000",
  "pickup_location_id": "00000000-0000-0000-0000-000000000000",
  "pickup_location_display_name": "14",
  "created_at": "2018-04-02T21:29:25.233Z",
  "updated_at": "2018-04-02T21:29:25.681Z",
  "last_cubbied_at": "2018-04-02T21:29:25.233Z",
  "status": "scheduled",
  "user_display_name": "John D"
}
```

Retrieve order information.


### Endpoint

`GET https://api.eatsa.com/v1/orders/:order_id`


### Response Arguments

Refer to order object


## Order Ready

> Example Request

```shell
curl -X PUT \
  http://api.eatsa.com/v1/orders/{order_id} \  
  -H "Content-Type:application/json; charset=utf-8" \
  -d '{
        "status": "ready_for_pickup"
      }'
```

> Example Response

```json
{
  "id": "00000000-0000-0000-0000-000000000000",
  "ref_id": "00000000-0000-0000-0000-000000000000",  
  "store_id": "00000000-0000-0000-0000-000000000000",
  "pickup_location_id": "00000000-0000-0000-0000-000000000000",
  "pickup_location_display_name": "14",
  "created_at": "2018-04-02T21:29:25.233Z",
  "updated_at": "2018-04-02T21:29:25.681Z",
  "last_cubbied_at": "2018-04-02T21:29:25.233Z",
  "status": "ready_for_pickup",
  "user_display_name": "John D"
}
```

This indicates that the order has been fulfilled by the back of house and is ready to be delivered to the customer.  Our system will update the status of an order to be 'ready_for_pickup'.  At this point a pickup location will be assigned to the order.  This endpoint should only be called when the full order is completed.

### HTTP Request

`PUT https://api.eatsa.com/v1/orders/:order_id`

### Response Arguments

Refer to order object


## Cancel order

> Example Request

```shell
curl -X PUT \
  http://api.eatsa.com/v1/orders/{order_id} \  
  -H "Content-Type:application/json; charset=utf-8" \
  -d '{
        "status": "attendant_canceled"
      }'
```

> Example Response

```json
{
  "id": "00000000-0000-0000-0000-000000000000",
  "ref_id": "00000000-0000-0000-0000-000000000000",  
  "store_id": "00000000-0000-0000-0000-000000000000",
  "pickup_location_id": "00000000-0000-0000-0000-000000000000",
  "pickup_location_display_name": "14",
  "created_at": "2018-04-02T21:29:25.233Z",
  "updated_at": "2018-04-02T21:29:25.681Z",
  "last_cubbied_at": "2018-04-02T21:29:25.233Z",
  "status": "attendant_canceled",
  "user_display_name": "John D"
}
```

The order will be canceled.  We support two types of canceled orders, `customer` or `attendant` depending on the person that is canceling the order.

### HTTP Request

`PUT https://api.eatsa.com/v1/orders/:order_id`


### Response Arguments

Refer to order object


## Retrieve order ETA

> Example Request

```shell
curl "https://api.eatsa.com/v1/orders/{order_id}/eta" \
	-i -H "Content-Type:application/json; charset=utf-8" \
```


> Example Response

```json
 {
    "estimated_time_remaining": 732
 }
```

Retrieve Order ETA in seconds.

### HTTP Request

`GET https://api.eatsa.com/v1/orders/:order_id/eta`

### Response

Parameter | Description
--------- | -----------
estimated_time_remaining | Estimated time in seconds before the order is processed.



## Retrieve all orders by store

> Example Request

```shell
curl "https://api.eatsa.com/v1/stores/{store_id}/orders" \
	-i -H "Content-Type:application/json; charset=utf-8" \
```


> Example Response

```json
{
    "count": 1,
    "orders": [
        {
            "id": "00000000-0000-0000-0000-000000000000",
            "ref_id": "00000000-0000-0000-0000-000000000000",
            "store_id": "00000000-0000-0000-0000-000000000000",
            "pickup_location_id": "00000000-0000-0000-0000-000000000000",
            "pickup_location_display_name": "14",
            "created_at": "2018-05-03T04:42:19.883Z",
            "updated_at": "2018-05-03T04:43:33.760Z",
            "last_cubbied_at": "2018-05-03T04:43:33.759Z",
            "status": "ready_for_pickup",
            "user_display_name": "John D"
        }
    ]
}
```

Retrieve all orders based on the given store.

### HTTP Request

`GET https://api.eatsa.com/v1/stores/:store_id/orders`


# Stores

## Store object

> Example Store object

```json
{
  "id": "00000000-0000-0000-0000-000000000000",
  "created_at": "2016-09-06T14:24:23.996Z",
  "updated_at": "2018-01-08T18:36:38.135Z",
  "status": "open",
  "phone_number": "4158138841",
  "address": "121 Spear St.",
  "locality": "San Francisco",
  "region": "CA",
  "postcode": "94105",
  "country": "US",
  "latitude": "37.791848",
  "longitude": "-122.392973",
  "timezone": "America/Los_Angeles",
  "mobile_orders_disabled": false,
  "business_page_url": "https://goo.gl/maps/Awz8xPMx1EH2",
  "store_hours": [
    {
      "day_of_week": "Monday",
      "open_time": "07:30:00",
      "close_time": "23:00:00"
    },
    {
      "day_of_week": "Tuesday",
      "open_time": "07:30:00",
      "close_time": "23:00:00"
    },
    {
      "day_of_week": "Wednesday",
      "open_time": "07:30:00",
      "close_time": "23:00:00"
    },
    {
      "day_of_week": "Thursday",
      "open_time": "07:30:00",
      "close_time": "23:00:00"
    },
    {
      "day_of_week": "Friday",
      "open_time": "07:30:00",
      "close_time": "23:00:00"
    }
  ]
}
```

Parameter | Description
--------- | -----------
id | Unique ID of the store.
created_at | Time the store was created.
updated_at | Time the store was last updated.
status | The current state of the store, `open` or `closed`.
phone_number | The phone number of the store.
address | The street address of the store.
locality | The location of the store, usually the city in the US.
region | The geographic region of the store, usually the state in the US.
postcode | The postcode for the store, in the US also referred to as the zip code.
country | The country where the store is located.  This follows the [ISO 3166-1 alpha-2](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2) standard.
latitude | The latitude of the store location.
longitude | The longitude of the store location.
timezone | The timezone that the store follows.  This is used to determine the store hours.
mobile_orders_disabled | A boolean value, used to determine if the store is accepting mobile orders.
business_page_url | The url for this store.
store_hours | An array of the hours that a store will be open.

### Store hours

Parameter | Description
--------- | -----------
day_of_week | The day of the week for the hours.
open_time | The open time of the store based on the timezone for this store.  Represented in the format `HH:MM:SS`.
close_time | The close time of the store based on the timezone for this store.  Represented in the format `HH:MM:SS`.


## List all stores

> Example Request

```shell
curl "https://api.eatsa.com/v1/stores" \
	-i -H "Content-Type:application/json; charset=utf-8"  
```

> Example Response

```json
{
  "count": 1,
  "stores": [
    {
      "id": "00000000-0000-0000-0000-000000000000",
      "created_at": "2016-09-06T14:24:23.996Z",
      "updated_at": "2018-01-08T18:36:38.135Z",
      "status": "open",
      "phone_number": "4158138841",
      "address": "121 Spear St.",
      "locality": "San Francisco",
      "region": "CA",
      "postcode": "94105",
      "country": "US",
      "latitude": "37.791848",
      "longitude": "-122.392973",
      "timezone": "America/Los_Angeles",
      "mobile_orders_disabled": false,
      "business_page_url": "https://goo.gl/maps/Awz8xPMx1EH2",
      "store_hours": [
        {
          "day_of_week": "Monday",
          "open_time": "07:30:00",
          "close_time": "23:00:00"
        },
        {
          "day_of_week": "Tuesday",
          "open_time": "07:30:00",
          "close_time": "23:00:00"
        },
        {
          "day_of_week": "Wednesday",
          "open_time": "07:30:00",
          "close_time": "23:00:00"
        },
        {
          "day_of_week": "Thursday",
          "open_time": "07:30:00",
          "close_time": "23:00:00"
        },
        {
          "day_of_week": "Friday",
          "open_time": "07:30:00",
          "close_time": "23:00:00"
        }
      ]
    }
  ]
}
```

Retrieve all stores where orders can be placed.

### Response Arguments

Parameter | Description
--------- | ---------------------------
count | Number of existing stores
stores | List of stores, refer to Store object


### HTTP Request

`GET https://api.eatsa.com/v1/stores`

## Retrieve a store

> Example Request

```shell
curl "https://api.eatsa.com/v1/stores/{store_id}" \
	-i -H "Content-Type:application/json; charset=utf-8" \
```

> Example Response

```json
{
  "id": "00000000-0000-0000-0000-000000000000",
  "created_at": "2016-09-06T14:24:23.996Z",
  "updated_at": "2018-01-08T18:36:38.135Z",
  "status": "open",
  "phone_number": "4158138841",
  "address": "121 Spear St.",
  "locality": "San Francisco",
  "region": "CA",
  "postcode": "94105",
  "country": "US",
  "latitude": "37.791848",
  "longitude": "-122.392973",
  "timezone": "America/Los_Angeles",
  "mobile_orders_disabled": false,
  "business_page_url": "https://goo.gl/maps/Awz8xPMx1EH2",
  "store_hours": [
    {
      "day_of_week": "Monday",
      "open_time": "07:30:00",
      "close_time": "23:00:00"
    },
    {
      "day_of_week": "Tuesday",
      "open_time": "07:30:00",
      "close_time": "23:00:00"
    },
    {
      "day_of_week": "Wednesday",
      "open_time": "07:30:00",
      "close_time": "23:00:00"
    },
    {
      "day_of_week": "Thursday",
      "open_time": "07:30:00",
      "close_time": "23:00:00"
    },
    {
      "day_of_week": "Friday",
      "open_time": "07:30:00",
      "close_time": "23:00:00"
    }
  ]
}
```
Retrieve a specific store.

### HTTP Request

`GET https://api.eatsa.com/v1/stores/:store_id`


### Response Arguments

Refer to Store object


