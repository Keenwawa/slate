# Pickup Locations

## Pickup Location object

> Example Pickup Location object

```json
{
    "id": "a09c4d73-8802-49fd-b278-5623509948d4",
    "store_id": "518fdc10-5772-11e4-7ed6-0700200c9a11",
    "name": "1F",
    "enabled": true,
    "line_items": [
        {
            "id": "d01c055c-b7eb-42a8-9f1a-f68c2caa75a4"
        }
    ]
}
```

Attribute | Description
--------- | -----------
id | Unique ID that identifies the pickup location
store_id | Unique ID that identifies the store the location belongs to
name | Label of the pickup location that will be displayed to the user 
disabled| Determines if a pickup location is in service or not
line_items | List of item IDs that are currently assigned or placed on a location

## Find Pickup Locations by store

> Example Request

```curl
curl "https://api.eatsa.com/v1/stores/518fdc10-5772-11e4-7ed6-0700200c9a11/locations" \
  -i -H "Content-Type:application/json; charset=utf-8"
```

> Example Response

```json
{
    "store_id": "518fdc10-5772-11e4-7ed6-0700200c9a11",
    "locations": [
        {
            "id": "50c754f2-56e4-40dd-b490-464d3cf22dc8",
            "store_id": "518fdc10-5772-11e4-7ed6-0700200c9a11",
            "name": "1F",
            "enabled": true,
            "line_items": [
                {
                    "id": "d01c055c-b7eb-42a8-9f1a-f68c2caa75a4"
                }
            ]
        },
        {
            "id": "52b0e613-073e-4e5d-86ed-2fbd49e7a19f",
            "store_id": "518fdc10-5772-11e4-7ed6-0700200c9a11",
            "name": "1R",
            "enabled": true,
            "line_items": []
        },
        {...},
        {...}
    ]
}
```

Retrieve store pickup locations, this allows to determine the state at any given time of pickup locations for a store. 


### Endpoint

`GET https://api.eatsa.com/v1/stores/:storeId/locations`

### Request Arguments

Parameter | Required | Description
--------- | ------- | -----------
storeId | yes  | Store id

### Response Arguments

Refer to pickup location object


## Enable/Disable Pickup Location

> Update pickup location request.

```shell
curl -X PUT \
  https://api.eatsa.com/v1/stores/:store_id/locations/enable \
  -H 'content-type: application/json; charset=utf-8' \
  -d '{
        "location": "e7b3fb20-349c-4876-b5b1-e9c971a83e2e",
        "enabled": false
      }'
```

> Update pickup location response.

```json
{
    "id": "e7b3fb20-349c-4876-b5b1-e9c971a83e2e",
    "store_id": "518fdc10-5772-11e4-7ed6-0700200c9a11",
    "name": "2F",
    "enabled": false,
    "line_items": []
}
```

Eatsa allows partner to enable or disable a pickup location.

### Endpoint

`PUT https://api.eatsa.com/v1/stores/:storeId/locations/:pickupLocationId`

### Request Arguments

Parameter | Required | Description
--------- | ------- | -----------
pickupLocationId | yes  | Id of the pickup location to update
disabled | yes  | Boolean flag that determines if a pickup location is in or out of service.

### Response Arguments

Refer to pickup location object

## Assign an item to a location

> Example Request

```curl
curl -X POST \
  https://api.eatsa.eatsa.com/v1/location/assign \
  -H 'Content-Type: application/json; charset=utf-8' \
  -d '{
      "line_item_id": "85ad92d7-a0e5-4b97-822c-f2dc67d8c40c"
   }'

```

> Example Response

```json
{
    "location_id": "a09c4d73-8802-49fd-b278-5623509948d4",
    "location_name": "1F",
    "enabled": true,
    "line_items": [
        {
            "id": "85ad92d7-a0e5-4b97-822c-f2dc67d8c40c"
        }
    ]
}
```

This action reserves a location where the item can be placed.


### Endpoint

`POST https://api.eatsa.eatsa.com/v1/location/assign`

### Request Arguments

Parameter | Required | Description
--------- | ------- | -----------
line_item_id | yes  | Line item id to request a pickup location

### Response Arguments

Parameter | Description
--------- | ------- | -----------
location_id | Location Id
location_name | Human readable location name
enabled | Determines if a location is enabled
line_items | List of items assigned to a location 


## Update an Order
> Update order request.

```shell
curl -X PUT \
  https://api.eatsa.com/v1/orders/:order_id \
  -H 'content-type: application/json; charset=utf-8' \
  -d '{
        "status": "on_the_line"
      }'
```

> Update order response.

```json
{
    "id": "9b38ece8-2abe-4eaa",
    "ref_id": "order123",
    "store_id": "cb8c37f2",
    "pickup_location_id": null,
    "pickup_location_display_name": null,
    "created_at": "2018-08-09T18:34:43.728Z",
    "updated_at": "2018-08-09T18:35:19.744Z",
    "status": "on_the_line",
    "human_readable_id": "103",
    "user_id": "bbbf9e96-0c85",
    "user_ref_id": "user123",
    "status_board_display_name": "John",
    "special_instructions": "",
    "line_items": [
        {
            "id": "85ad92d7-a0e5-4b97-822c-f2dc67d8c40c",
            "item_id": "bacfda02-2568-4fdf",
            "item_name": "drink",
            "customer_name": "John",
            "special_instructions": "",
            "location_id": null,
            "location_name": null
        }
    ]
}
```

Update the state of an order.

### Endpoint

`PUT https://api.eatsa.com/v1/orders/:orderId`

### Request Arguments

Parameter | Required | Description
--------- | ------- | -----------
orderId | yes  | Order Id to update
status | yes  | Valid order status

### Response Arguments

Refer to order object


### Possible errors

* http_status_code: 409 (Conflict) 
* http_response_body:
  * code: INVALID_REQUEST | NO_PICKUP_LOCATIONS_AVAILABLE
  * message: Related with the violation. 

<aside class="warning">
If an attempt to set the order to “ready_for_pickup” results in an error related with no pickup location available 
then the order is set to “ready_to_serve_again” automatically.
</aside>




