# Orders

## Model
Attribute | Description
--------- | -----------
id | Unique ID that identifies the order at eatsa.
ref_id | Reference ID for the order in the partner system. This ID is expected to be unique.
store_id | Unique ID that identifies the store where the order was created.
pickup_location_id| Pickup station id.
pickup_location_display_name| Pickup station human readable id.
created_at | Time the order was created.
updated_at | Time the order was last updated.
last_cubbied_at | Timestamp that is updated every time an order is placed in a pickup location.
status | Status of the order.
user_display_name | Name that will be displayed on the status board to inform the customer of their order.

<aside class="notice">
Read more in the State section.
</aside>


## Create
> Create order request.

```shell
curl -X POST \
  https://api.eatsa.com/v1/orders \
  -H 'content-type: application/json; charset=utf-8' \
  -H 'x-authtoken: YOUR_SECRET_KEY' \
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

To create a new order in the eatsa system it is required to provide:  

  * ref_id: A unique identifier in the partner system for the order.
  * store_id: A unique identifier in the partner system for the store.
  * user:
    * ref_id: A unique identifier in the partner system for this user.
    * first_name: First name to display in the pickup station and the boards.
    * last_name: Last name to display in the pickup station and the boards.
      
A unique id for the order is returned that can be used to track the order and modify its state accordingly.


## Update
> Update order request.

```shell
curl -X PUT \
  https://api.eatsa.com/v1/orders/:eatsa_order_id \
  -H 'content-type: application/json; charset=utf-8' \
  -H 'x-authtoken: YOUR_SECRET_KEY' \
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

To update an order it is required to provide the eatsa order id.

If an attempt to set a status results in an error related with a violation of the state machine or no pickup locations available then an error will be returned with:

* http_status_code: 409 (Conflict) 
* http_response_body:
  * code: INVALID_REQUEST | NO_PICKUP_LOCATIONS_AVAILABLE
  * message: Related with the violation. 

<aside class="warning">
If an attempt to set the order to “ready_for_pickup” results in an error related with no pickup location available 
then the order is set to “ready_to_serve_again” automatically.
</aside>

## State
![alt text](order_state_machine.png)

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
