# Orders

## Order object

> Example Order object

```json
{
    "id": "3f01ce65-bfe2-4411-a623-9440c73e40ae",
    "ref_id": "o-20180510-0010",
    "store_id": "518fdc10-5772-11e4-7ed6-0700200c9a11",
    "pickup_location_id": "a08c4d73-8802-48fd-b278-5623508948d4",
    "pickup_location_display_name": "1",
    "created_at": "2018-05-15T22:01:41.115Z",
    "updated_at": "2018-05-15T22:03:57.806Z",
    "scheduled_time": "2018-05-15T22:05:57.806Z",
    "status": "ready_for_pickup",
    "user_ref_id": "u-0002",
    "user_display_name": "John D"
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
user_display_name | Name that will be displayed on the status board to inform the customer of their order.
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
        "store_id": "storeABC",
        "user": {
          "ref_id": "user123",
          "first_name": "John",
          "last_name": "Doe"
        }
      }'
```

> Create order response.

```json
{
    "id": "891bf5r64-d9d0-4001-a77a-7b73a69213b0",
    "ref_id": "order123",
    "store_id": "storeABC",
    "pickup_location_id": null,
    "pickup_location_display_name": null,
    "created_at": "2018-05-10T01:12:32.659Z",
    "updated_at": "2018-05-10T01:12:32.659Z",
    "status": "in_queue",
    "user_ref_id": "user123",
    "user_display_name": "John D"
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

<!---
timeslot_start_time| no | Defines a pickup time that enables orders to be scheduled. The available time slots for a store can be retrieved from the 'Find store available time slots' API.
--->

### User object

Parameter | Required | Description
--------- | ------- | -----------
ref_id | yes | The reference ID for the user in the partner system.  This ID is expected to be unique for the specified user.
first_name | yes | The first name of the user.
last_name | yes | The last name of the user.


## Find an Order

> Example Request

```curl
curl "https://api.eatsa.com/v1/orders/2recef15-c638-23a2-a133-64789f9929b1" \
  -i -H "Content-Type:application/json; charset=utf-8"
```

> Example Response

```json
{
    "id": "2recef15-c638-23a2-a133-64789f9929b1",
    "ref_id": "order123",
    "store_id": "storeABC",
    "pickup_location_id": "a09c4d73-8802-49fd-b278-5623509948d4",
    "pickup_location_display_name": "1",
    "created_at": "2018-05-10T01:12:32.659Z",
    "updated_at": "2018-05-10T01:13:32.659Z",
    "status": "ready_for_pickup",
    "user_ref_id": "user123",
    "user_display_name": "John D"
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
          "id": "2recef15-c638-23a2-a133-64789f9929b1",
          "ref_id": "order123",
          "store_id": "518fdc10-5772-11e4-7ed6-0700200c9a11",
          "pickup_location_id": "a09c4d73-8802-49fd-b278-5623509948d4",
          "pickup_location_display_name": "1",
          "created_at": "2018-05-10T01:12:32.659Z",
          "updated_at": "2018-05-10T01:13:32.659Z",
          "status": "ready_for_pickup",
          "user_ref_id": "user123",
          "user_display_name": "John D"
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


## Update an Order
> Update order request.

```shell
curl -X PUT \
  https://api.eatsa.com/v1/orders/:eatsa_order_id \
  -H 'content-type: application/json; charset=utf-8' \
  -d '{
        "status": "ready_for_pickup"
      }'
```

> Update order response.

```json
{
    "id": "891bf5r64-d9d0-4001-a77a-7b73a69213b0",
    "ref_id": "order123",
    "store_id": "storeABC",
    "pickup_location_id": "780ae4q53-c8c9-3990-f669-7a62f58102a9",
    "pickup_location_display_name": "2",
    "created_at": "2018-05-10T01:12:32.659Z",
    "updated_at": "2018-05-10T01:12:32.659Z",
    "status": "ready_for_pickup",
    "user_ref_id": "user123",
    "user_display_name": "John D"
}
```

Upate an order state

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


