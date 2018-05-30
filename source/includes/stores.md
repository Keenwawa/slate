# Stores

## Store object

> Example Store object

```json
{
  "id": "518fdc10-5772-11e4",
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
    },
    {
      "day_of_week": "Saturday",
      "open_time": "07:30:00",
      "close_time": "23:00:00"
    },
    {
      "day_of_week": "Sunday",
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
day_of_week | The day of the week.
open_time | The open time of the store based on the timezone for the store.  Represented in the format `HH:MM:SS`.
close_time | The close time of the store based on the timezone for the store.  Represented in the format `HH:MM:SS`.


## Retrieve a store

> Example Request

```curl
curl "https://api.eatsa.com/v1/stores/418fdc10-5881-11e4-8ed6-0800200c9a66" \
    -i -H "Content-Type:application/json; charset=utf-8" \
```

> Example Response

```json
{
  "id": "518fdc10-5772-11e4",
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
    },
    {
      "day_of_week": "Saturday",
      "open_time": "07:30:00",
      "close_time": "23:00:00"
    },
    {
      "day_of_week": "Sunday",
      "open_time": "07:30:00",
      "close_time": "23:00:00"
    }
  ]
}
```
Retrieve a specific store.

### Endpoint

`GET https://api.eatsa.com/v1/orders/stores/:id`

### Request Arguments

Parameter | Description
--------- | ---------------------------
id | Store id


### Response Arguments

Refer to Store object

## List all stores

> Example Request

```curl
curl "https://api.eatsa.com/v1/stores" \
    -i -H "Content-Type:application/json; charset=utf-8"
```

> Example Response

```json
{
  "count": 5,
  "stores": [
    {
      "id": "518fdc10-5772-11e4",
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
    },
    {...},
    {...},
    {...},
    {...}
  ]
}
```

Retrieve all stores where orders can be placed.

### Endpoint

`GET https://api.eatsa.com/v1/stores`


### Response Arguments

Parameter | Description
--------- | ---------------------------
count | Number of existing stores
stores | List of stores, refer to Store object

<!--

## Find store available time slots

> Example Request

```curl
curl "https://api.eatsa.com/v1/stores/518fdc10-5772-11e4/reservable_timeslots" \
    -i -H "Content-Type:application/json; charset=utf-8" \
```

> Example Response

```json
{
  "estimated_time_now": 117,
  "timeslot_duration": 300,
  "reservable_timeslots": [
    {
      "start_time": "2018-04-03T21:00Z",
      "count_available": 6
    },
    {
      "start_time": "2018-04-03T21:05Z",
      "count_available": 6
    },
    {
      "start_time": "2018-04-03T21:10Z",
      "count_available": 6
    },
    {
      "start_time": "2018-04-03T21:15Z",
      "count_available": 6
    },
    {
      "start_time": "2018-04-03T21:20Z",
      "count_available": 6
    },
    {
      "start_time": "2018-04-03T21:25Z",
      "count_available": 6
    },
    {
      "start_time": "2018-04-03T21:30Z",
      "count_available": 6
    },
    {
      "start_time": "2018-04-03T21:35Z",
      "count_available": 6
    }
  ]
}

```

Find all the available times a store has to schedule an order that day.

### Endpoint

`GET https://api.eatsa.com/v1/stores/:storeId/reservable-time-slots`


### Response Arguments

Parameter | Description
--------- | ---------------------------
estimated_time_now | Estimated time for an order to be processed
timeslot_duration | Seconds between each time slot
reservable_timeslots | List of available start times to schedule an order. Start Times are in UTC expressed using the ISO 8601 format of %Y-%m-%dT%H:%M:%SZ. Example: 2018-04-03T16:02:46Z.

-->
