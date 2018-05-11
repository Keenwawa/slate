# Pickup Location

## Monitor
Eatsa exposes the list of pickup locations for a monitoring usage. 

> List pickup locations request.
 
```shell
curl -X GET \
  https://api.eatsa.com/v1/stores/:store_id/pickup-locations \
  -H 'content-type: application/json; charset=utf-8' \
  -H 'x-authtoken: YOUR_SECRET_KEY'
```

> List pickup locations response.

```json
{
    "store_id": "storeABC",
    "pickup_locations": [
        {
            "id": "8a184494-32f0-4a3f-82d2-5c1fb2f2c43e",
            "name": "2",
            "order_id": "891bf5r64-d9d0-4001-a77a-7b73a69213b0",
            "updated_at": "2018-05-10T05:07:08.453Z",
            "disabled": false,
            "state": "assigned"
        }
    ]
}
```

## Manage
> Update pickup location request.

```shell
curl -X PUT \
  https://api.eatsa.com/v1/stores/:store_id/pickup-locations/:pickup_location_id \
  -H 'content-type: application/json; charset=utf-8' \
  -H 'x-authtoken: YOUR_SECRET_KEY' \
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

To update a pickup location it is required to provide the pickup location id.

  
