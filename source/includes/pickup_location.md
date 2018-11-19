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



