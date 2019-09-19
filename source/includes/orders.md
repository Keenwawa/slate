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
    "service_type": "take_out",
    "special_instructions": "all sauces on the side - thanks!",
    "line_items": [
        {
            "id": "85ad92d7-a0e5-4b97-822c-f2dc67d8c40c",
            "item_id": "bacfda02-2568-4fdf",
            "item_name": "Wrap",
            "customer_name": "John",
            "special_instructions": "Item notes",
            "location_id": null,
            "location_name": null,
            "ref_id": "0eca30b46eb6",
            "total_price": 1129,
            "price": 913,
            "modifications": [
                {
                    "modifier_id": "6bf19680-6898-4bf0-bee7-93e941f5e258",
                    "modifier_name": "Couscous",
                    "ref_id": "bb3c",
                    "price": 125
                }
            ],
            "taxes": [
                {
                    "id": "t-158-04",
                    "name": "sales tax",
                    "amount": 130
                },
                {
                    "id": "t-158-05",
                    "name": "health tax",
                    "amount": 85
                }
            ]
        }
    ]
}
```






Attribute | Description
--------- | -----------
id | Unique ID that identifies the order at eatsa.
ref_id | The reference ID for the order in the partner system. This ID is expected to be unique for every new order.
store_id | Store where the order will be created
pickup_location_id| Pickup station id.
pickup_location_display_name| Pickup station human readable id.
created_at | Time the order was created.
updated_at | Time the order was last updated.
scheduled_time | Optional, The date and time the order is scheduled to be fulfilled, if not present or null the assumptions is an ASAP order
status | Status of the order
human_readable_id | Human readable id for the order
user_id | Unique ID of the user that made the order.
user_ref_id | Reference ID for the user in the partner system.
status_board_display_name | Name that will be displayed on the status board to inform the customer of their order.
special_instructions | Text that indicates any special instructions for the order.
service_type | Optional, indicates the how the order will be packaged. Possible values: ```dine_in```, ```take_out```. Defaults to ```take_out```.
channel | Optional, indicates the channel making the request
total | Order amount in cents
line_items | Collection of Line Item objects

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
is_customized | Determines if there was a modification made to the line item.
modifications | List of modifiers added to the line item
taxes | List of taxes applied to the line item

### Modification object

Attribute | Description
--------- | -----------
modifier_id | LineModifier id
modifier_name | Modifier name unique ID
modifier_price | Amount charged for the modifier in cents

###Taxes Object

Attribute | Description
--------- | -----------
tax_id | Reference id for the tax
tax_name | Name of the tax
total | Total tax charged in cents


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
          "total": 500,
          "payments": [
            {
              "payment_type": "cash",
              "amount": 200
            },
            {
              "payment_type": "credit_card",
              "amount": 300
            }
          ],
          "status_board_display_name": null,
          "special_instructions": "Handle with care",
           "line_items": [
            {
              "item_id": "6a834a14",
              "ref_item_name": "Wrap",
              "ref_id": "0eca30b46eb6",
              "customer_name": "The Jon Doe",
              "special_instructions": "Item notes",
              "price": 913,
              "total_price": 1129,
              "taxes": [
                    {
                      "id": "t-158-04",
                      "name": "sales tax",
                      "amount": 130
                    },
                    {
                      "id": "t-158-05",
                      "name": "health tax",
                      "amount": 85
                    }
                ],
              "modifications": [
                {
                  "modifier_id": "6bf19680",
                  "ref_id": "bb3c",
                  "price": 125
                }
              ]
            }
          ]  
        }'
```

> Create order response.

```json
{
    "id": "54ebb9f9",
    "ref_id": "o-20190526-534",
    "store_id": "78d9d81a",
    "pickup_location_id": null,
    "pickup_location_display_name": null,
    "status_board_display_location": "",
    "created_at": "2019-06-25T00:06:04.358Z",
    "updated_at": "2019-06-25T00:06:04.371Z",
    "eta": "2019-06-25T00:07:04.621234Z",
    "status": "in_queue",
    "human_readable_id": "900",
    "user_id": "b4f87247",
    "user_ref_id": "u-rd000002",
    "status_board_display_name": "John D.",
    "special_instructions": "Handle with care",
    "service_type": "take_out",
    "total": 500,
    "line_items": [
        {
            "id": "8b84ab2c-2177",
            "item_id": "6a834a14",
            "item_name": "Wrap",
            "status": "unstarted",
            "is_customized": false,
            "customer_name": "John D.",
            "special_instructions": "Item notes",
            "location_id": null,
            "location_name": null,
            "modifications": [
                {
                    "modifier_id": "6bf19680",
                    "modifier_name": "Couscous",
                    "ref_id": "bb3c",
                    "price": 125
                }
            ],
            "ref_id": "0eca30b46eb6",
            "total_price": 1129,
            "price": 913,
            "taxes": [
                {
                    "id": "t-158-04",
                    "name": "sales tax",
                    "amount": 130
                },
                {
                    "id": "t-158-05",
                    "name": "health tax",
                    "amount": 85
                }
            ]
        },
        {
            "id": "d8bcc35c",
            "item_id": "737e0bd8",
            "item_name": "Bag",
            "status": "unstarted",
            "is_customized": false,
            "customer_name": null,
            "special_instructions": null,
            "location_id": null,
            "location_name": null,
            "modifications": []
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
scheduled_time | no | The date and time the order is scheduled to be fulfilled, if not present or null the assumptions is an ASAP order
status_board_display_name | no | Name that will be displayed on the status board to inform the customer of their order. If not supplied the name will be infered from the user's first and last name.
unlock_code | no | An alphanumeric code that will be used to open a pickup device. If present on the order, the pickup device will be locked and require the code entered in order to open
channel | no | Indicates the channel making the request
service_type | no | Indicates the how the order will be packaged. Possible values: ```dine_in```, ```take_out```. Defaults to ```take_out```.
total | no | Total charged after taxes and promotions
payments | no | Collection of Payments (see below)
line_items | yes | Collection of Line Items (see below)

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

### Payment object

Parameter | Required | Description
--------- | ------- | -----------
payment_type | yes | Type of payment method used 
amount | yes | Amount charged in cents

### Line Item object

Parameter | Required | Description
--------- | ------- | -----------
item_id | yes | Item id
Item name | no | Item name
modifications | no | List of modifiers added to the line item
special_instructions | no | Open text field for special instructions

### Modification object

Parameter | Required | Description
--------- | ------- | -----------
modifier_id | yes | Modifier id
modifier_name | no | Modifier name
modifier_price | no | Amount charged for the modifier in cents

### Taxes object

Parameter | Required | Description
--------- | ------- | -----------
id | yes | Reference id for the tax
name | yes | Name of the tax
amount | yes | Total tax charged in cents





## Find an Order

> Example Request

```curl
curl "https://api.eatsa.com/v1/orders/54ebb9f9" \
  -i -H "Content-Type:application/json; charset=utf-8"
```

> Example Response

```json
{
    "id": "54ebb9f9",
    "ref_id": "o-20190526-534",
    "store_id": "78d9d81a-2c2a-4881-8dcd-d57062ebac28",
    "pickup_location_id": null,
    "pickup_location_display_name": null,
    "status_board_display_location": "",
    "created_at": "2019-06-25T00:06:04.358Z",
    "updated_at": "2019-06-25T08:19:42.268Z",
    "eta": "2019-06-25T21:51:51.943949Z",
    "status": "attendant_canceled",
    "human_readable_id": "900",
    "unlock_code": "1234",
    "user_id": "b4f87247-c812-4f19-b60b-58bebcb0309c",
    "user_ref_id": "u-rd000002",
    "status_board_display_name": "John D.",
    "special_instructions": "Handle with care",
    "service_type": "take_out",
    "total": 500,
    "line_items": [
        {
            "id": "8b84ab2c",
            "item_id": "6a834a14",
            "item_name": "Wrap",
            "status": "unstarted",
            "is_customized": false,
            "customer_name": "The Jon Doe",
            "special_instructions": "Item notes",
            "location_id": null,
            "location_name": null,
            "modifications": [
                {
                    "modifier_id": "6bf19680",
                    "modifier_name": "Couscous",
                    "ref_id": "bb3c",
                    "price": 125
                }
            ],
            "ref_id": "0eca30b46eb6",
            "total_price": 1129,
            "price": 913,
            "taxes": [
                {
                    "id": "t-158-04",
                    "name": "sales tax",
                    "amount": 130
                },
                {
                    "id": "t-158-05",
                    "name": "health tax",
                    "amount": 85
                }
            ]
        },
        {
            "id": "d8bcc35c",
            "item_id": "737e0bd8",
            "item_name": "Bag",
            "status": "unstarted",
            "is_customized": false,
            "customer_name": null,
            "special_instructions": null,
            "location_id": null,
            "location_name": null,
            "modifications": []
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

## Order Analytics

> Example Request

```curl
curl "https://api.eatsa.com/v1/order-analytics?created_at_after=2019-06-23&page=1&per_page=200" \
  -i -H "Content-Type:application/json; charset=utf-8"
```

> Example Response

```json
{
  "total_count": 996,
  "total_pages": 5,
  "page_number": 1,
  "size": 200,
  "orders": [
    {
      "id": "b31f4d12",
      "ref_id": null,
      "customer": {
        "id": "6d7ffdc7",
        "user_ref_id": null,
        "first_name": "J",
        "last_name": "Y",
        "marketing_opt_out": false,
        "in_store_receipt_email": null,
        "created_at": "2019-06-23T00:04:47.446Z"
      },
      "store": {
        "id": "8dee9a76",
        "address": "300 Michigan Ave",
        "timezone": "America/Chicago"
      },
      "created_at": "2019-06-23T00:05:19.659Z",
      "updated_at": "2019-06-23T00:07:48.786Z",
      "started_at": "2019-06-23T00:05:46.090Z",
      "delivered_at": "2019-06-23T00:07:48.782Z",
      "served_at": "2019-06-23T00:06:08.100Z",
      "scheduled_time": null,
      "currency": "USD",
      "status": "delivered_to_customer",
      "special_instructions": null,
      "line_items": [
        {
          "id": "b2225252",
          "item_id": "e2a07d9a",
          "item_name": "Chicken Teriyaki",
          "item_analytics_name": "Bao",
          "line_item_total": 579,
          "line_item_total_taxes": 67,
          "line_item_gross_total": 579,
          "is_comped": false,
          "reorder_id": null,
          "customer_name": null,
          "special_instructions": null,
          "location_reserved_at": "2019-06-23T00:05:59.854Z",
          "location_placed_at": "2019-06-23T00:06:08.090Z",
          "location_cleared_at": "2019-06-23T00:07:48.618Z",
          "modifications": []
        }
      ],
      "promo": null,
      "total": 646,
      "gross_total": 579,
      "applied_taxes": [
        {
          "id": "0dcbf361",
          "name": "County Sales Tax",
          "amount": 67
        }
      ],
      "is_refunded": null,
      "refunds": null,
      "channel": "kiosk",
      "payment_transactions": [
        {
          "payment_type": "sale",
          "transaction_amount": 646,
          "created_at": "2019-06-23T00:05:19.695Z",
          "currency": "USD"
        }
      ]
    }, 
    {...},
    {...}
  ]
}
```

Retrieve order information.


### Endpoint

`GET https://api.eatsa.com/v1/order-analytics`

### Request Parameters

Parameter | Required | Description
--------- | ------- | -----------
store_id | no | Store Id
created_at_before | no | Find orders that were created before date
created_at_after | no | Find orders that were created after date
updated_at_before | no | Find orders that were updated before date
updated_at_after | no | Find orders that were updated after date
channel | no | Channel to filter by
per_page | no | Number or result per page
page | no | Page Number

### Response Arguments

Refer to order object




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


