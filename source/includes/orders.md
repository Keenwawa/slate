# Orders

## Order object

> Example Order object

```json
{
    "id": "9b38ece8-2abe-4eaa",
    "ref_id": "o-20180808-933",
    "store_id": "cb8c37f2",
    "pickup_location_id": null,
    "pickup_location_display_name": null,
    "created_at": "2018-08-09T18:34:43.728Z",
    "updated_at": "2018-08-09T18:34:43.744Z",
    "status": "in_queue",
    "human_readable_id": "103",
    "user_id": "bbbf9e96-0c85",
    "user_ref_id": "u-rx000002",
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


Attribute | Description
--------- | -----------
id | Unique ID that identifies the order at eatsa.
ref_id | Reference ID for the order in the partner system. This ID is expected to be unique.
store_id | Unique ID that identifies the store where the order was created.
pickup_location_id| Pickup station id.
pickup_location_display_name| Pickup station human readable id.
created_at | Time the order was created.
updated_at | Time the order was last updated.
scheduled_time | Optional, indicates the time an order is scheduled at (if specified when the order was created creation)
status | Status of the order
human_readable_id | Human readable id for the order
user_id | Unique ID of the user that made the order.
user_ref_id | Reference ID for the user in the partner system.
status_board_display_name | Name that will be displayed on the status board to inform the customer of their order.
special_instructions | Text that indicates any special instructions for the order.

### Line Item object

Attribute | Description
--------- | -----------
id | Line Item unique ID 
item_id | Item unique ID
item_name | Item name
customer_name | Customer name for the item.
special_instructions | Text that indicates any special instructions for the item.
location_id | Pickup station id.
location_name | Pickup station human readable id.


<!--- 
  last_cubbied_at | Timestamp that is updated every time an order is placed in a pickup location. 
--->

<aside class="notice">
Read more in the State section.
</aside>


## Create an Order
> Create order request.

```shell
curl -X POST \
  https://api.eatsa.com/v1/orders \
  -H 'content-type: application/json; charset=utf-8' \
  -d '{
        "ref_id": "order123",
        "store_id": "cb8c37f2",
        "user": {
          "ref_id": "user123",
          "first_name": "John",
          "last_name": "Doe",
          "email": "john.doe@somedomain.com"
        },
        "status_board_display_name": "John",
        "line_items": [
          {
            "ref_item_type": "drink"
          }
        ]
      }'

```

> Create order response.

```json
{
    "id": "9b38ece8-2abe-4eaa",
    "ref_id": "order123",
    "store_id": "cb8c37f2",
    "pickup_location_id": null,
    "pickup_location_display_name": null,
    "created_at": "2018-08-09T18:34:43.728Z",
    "updated_at": "2018-08-09T18:34:43.744Z",
    "status": "in_queue",
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

Creates a new order in the eatsa system, a unique id for the order is returned that can be used to track the order and modify its state accordingly.

### Endpoint

`POST https://api.eatsa.com/v1/orders`

### Request Arguments

Parameter | Required | Description
--------- | ------- | -----------
ref_id | yes  | The reference ID for the order in the partner system.  This ID is expected to be unique for every new order.
store_id | yes | Store where the order will be created
user | yes | The user object (see below)
status_board_display_name | no | Name that will be displayed on the status board to inform the customer of their order. If not supplied the name will be infered from the user's first and last name.


<!---
timeslot_start_time| no | Defines a pickup time that enables orders to be scheduled. The available time slots for a store can be retrieved from the 'Find store available time slots' API.
--->

### User object

Parameter | Required | Description
--------- | ------- | -----------
ref_id | yes | The reference ID for the user in the partner system.  This ID is expected to be unique for the specified user.
first_name | yes | The first name of the user.
last_name | yes | The last name of the user.
email | no | Email of the user.


### Line Items

List or items to order

Parameter | Required | Description
--------- | ------- | -----------
ref_item_type | yes | Determines the type of item to order. Possible values "drink" or "food".


## Find an Order

> Example Request

```curl
curl "https://api.eatsa.com/v1/orders/2recef15-c638-23a2-a133-64789f9929b1" \
  -i -H "Content-Type:application/json; charset=utf-8"
```

> Example Response

```json
{
    "id": "9b38ece8-2abe-4eaa",
    "ref_id": "order123",
    "store_id": "cb8c37f2",
    "pickup_location_id": null,
    "pickup_location_display_name": null,
    "created_at": "2018-08-09T18:34:43.728Z",
    "updated_at": "2018-08-09T18:35:56.744Z",
    "status": "ready_for_pickup",
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
            "location_id": "a09c4d73-8802-49fd-b278-5623509948d4",
            "location_name": "1"
        }
    ]
}
```

Retrieve order information.


### Endpoint

`GET https://api.eatsa.com/v1/orders/:id`

### Request Arguments

Parameter | Required | Description
--------- | ------- | -----------
id | yes  | Order id

### Response Arguments

Refer to order object


## Find all Orders by store

> Example Request

```curl
curl "https://api.eatsa.com/v1/stores/518fdc10-5772-11e4-7ed6-0700200c9a11/orders" \
  -i -H "Content-Type:application/json; charset=utf-8"
```

> Example Response

```json
{
    "count": 9,
    "orders": [
        {
            "id": "9b38ece8-2abe-4eaa",
            "ref_id": "order123",
            "store_id": "cb8c37f2",
            "pickup_location_id": null,
            "pickup_location_display_name": null,
            "created_at": "2018-08-09T18:34:43.728Z",
            "updated_at": "2018-08-09T18:35:56.744Z",
            "status": "ready_for_pickup",
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
                    "location_id": "a09c4d73-8802-49fd-b278-5623509948d4",
                    "location_name": "1",
                }
            ]
        },
        {...},
        {...},
        {...}
        ...
    ]
}    
```

Retrieve order information.


### Endpoint

`GET https://api.eatsa.com/v1/stores/:storeId/orders`

### Request Arguments

Parameter | Required | Description
--------- | ------- | -----------
storeId | yes  | Store id

### Response Arguments

Refer to order object

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

## State of an Order
![alt text](order_state_machine2.png)

Status | Description | Pickup Station | Board 
------ | ----------- | -------------- | -----
scheduled | Scheduled for a pickup time in the future. | - | -
in_queue |  In the active queue. | - | -
on_the_line | Assembly claims the order for a line. | - | -
ready_for_pickup | The order has been completed. | Animation | John D.
delivered_to_customer | Customer has picked up the order.| - | -
hold_in_back | Order is being held in the back until customer gets in the store. | - | See Host
ready_to_serve_again | Customer is here, attendant asked the staff to put the order back in a pickup station | - | -
attendant_canceled | An employee has canceled an order.| - | See Host

### Order Ready for pickup
This indicates that the order has been fulfilled by the back of house and is ready to be delivered to the customer. Our system will update the status of an order to be 'ready_for_pickup'. At this point, a pickup location will be assigned to the order. This endpoint should only be called when the full order is completed.

### Order Canceled
The order will be canceled. We support two types of canceled orders, customer or attendant depending on the person that is canceling the order.


