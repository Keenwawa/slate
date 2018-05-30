# Pickup Locations

## Pickup Location object

> Example Pickup Location object

```json
{
  "id": "a09c4d73-8802-49fd-b278-5623509948d4",
  "name": "1",
  "order_id": "3f01ce65-bfe2-4411-a623-9440c73e40ae",
  "updated_at": "2018-05-15T22:03:57.783Z",
  "disabled": false,
  "state": "order_unassigned"
}
```

Attribute | Description
--------- | -----------
id | Unique ID that identifies the pickup location
name | Label of the pickup location that will be displayed to the user 
order_id | Determines at a given point in time the order that the pickup location will process.
updated_at| Last time the pickup location was updated
disabled| Determines if a pickup location is in service or not
state | State of the pickup location

## Find Pickup Locations by store

> Example Request

```curl
curl "https://api.eatsa.com/v1/stores/518fdc10-5772-11e4-7ed6-0700200c9a11/pickup-locations" \
  -i -H "Content-Type:application/json; charset=utf-8"
```

> Example Response

```json
{
    "store_id": "518fdc10-5772-11e4-7ed6-0700200c9a11",
    "pickup_locations": [
        {
            "id": "a09c4d73-8802-49fd-b278-5623509948d4",
            "name": "1",
            "order_id": "3f01ce65-bfe2-4411-a623-9440c73e40ae",
            "updated_at": "2018-05-15T22:03:57.783Z",
            "disabled": false,
            "state": "order_unassigned"
        },
        {
            "id": "29978afa-9b01-4d45-bfca-abd390f79483",
            "name": "2",
            "order_id": null,
            "updated_at": "2018-05-13T22:20:35.804Z",
            "disabled": false,
            "state": "order_unassigned"
        },
        {
            "id": "6bbef153-3e6b-472a-8466-e9b680bfec02",
            "name": "3",
            "order_id": null,
            "updated_at": "2018-04-16T23:40:11.549Z",
            "disabled": true,
            "state": "order_unassigned"
        },
        {...},
        {...}
    ]
}
```

Retrieve store pickup locations, this allows to determine the state at any given time of pickup locations for a store. 


### Endpoint

`GET https://api.eatsa.com/v1/stores/:storeId/pickup-locations`

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
  https://api.eatsa.com/v1/stores/:store_id/pickup-locations/:pickupLocationId \
  -H 'content-type: application/json; charset=utf-8' \
  -d '{
        "disabled": true
      }'
```

> Update pickup location response.

```json
{
    "id": "8a184494-32f0-4a3f-82d2-5c1fb2f2c43e",
    "name": "2",
    "order_id": null,
    "updated_at": "2018-05-10T05:07:08.453Z",
    "disabled": true,
    "state": "not_assigned"
}
```

Eatsa allows partner to enable or disable a pickup location.

### Endpoint

`PUT https://api.eatsa.com/v1/stores/:storeId/pickup-locations/:pickupLocationId`

### Request Arguments

Parameter | Required | Description
--------- | ------- | -----------
pickupLocationId | yes  | Id of the pickup location to update
disabled | yes  | Boolean flag that determines if a pickup location is in or out of service.

### Response Arguments

Refer to pickup location object



