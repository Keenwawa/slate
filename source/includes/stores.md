# Stores
> List stores request.

```shell
curl -X GET \
  https://api.eatsa.com/v1/stores \
  -H 'x-authtoken: YOUR_SECRET_KEY'
```

> List stores response.

```json
{
    "count": 1,
    "stores": [
        {
            "id": "storeABC",
            "address": "200 Kansas",
            "locality": "San Francisco",
            "region": "CA",
            "postcode": "94103"
        }
    ]
}
```

