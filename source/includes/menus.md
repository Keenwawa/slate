# Menus

## Menu object

> Example Menu object

```json
{
  "menus": [
    {
      "id": "e0f7b14b-d3c1-4df2-998e-13d0fcfa0293",
      "name": "Lunch",
      "description": "Lunch Menu",
      "start_time": "10:30:00",
      "end_time": "18:00:00",
      "items": [
        {
          "id": "59a8bdc2-d937-44bc-94dd-a1008331805c",
          "name": "Bibimbap Bowl",
          "description": "Steamed brown rice topped with a rainbow of veggies and a soft eatsa egg.",
          "base_price": 895,
          "modifiers_groups": [
            {
              "id": "21c740b8-7f8b-4585-aa78-0c66c7c9c398",
              "name": "Proteins",
              "short_name": "Meat",
              "description": "Meat - LUNCH",
              "sort_order": 7,
              "max_per_line_item": null,
              "modifiers": [
                {
                  "id": "f85384a5-260b-4912-8a04-35649270c623",
                  "name": "Turkey Loaf",
                  "modifier_group_id": "21c740b8-7f8b-4585-aa78-0c66c7c9c398",
                  "price": 0
                },
                {
                  "id": "dbf92910-7618-476a-91b1-0a5796d7b8a3",
                  "name": "Bulgogi Beef",
                  "modifier_group_id": "21c740b8-7f8b-4585-aa78-0c66c7c9c398",
                  "price": 0
                },
                {
                  "id": "c41308e1-d364-46a4-8c24-e92e27423d0d",
                  "name": "Citrus Pulled Pork",
                  "modifier_group_id": "21c740b8-7f8b-4585-aa78-0c66c7c9c398",
                  "price": 0
                },
                {
                  "id": "2a6f2ac1-bf67-41ae-8a75-cd169fcf0002",
                  "name": "Rosemary Chicken (Cold)",
                  "modifier_group_id": "21c740b8-7f8b-4585-aa78-0c66c7c9c398",
                  "price": 0
                }
              ]
            },
            {...}
          ]
        },
        {...}
      ]
    },
    {
      "id": "98597742-2086-45d4-bc39-72486c03ee9c",
      "name": "Breakfast",
      "description": "Jan 5th Menu",
      "start_time": "00:00:00",
      "end_time": "10:30:00",
      "items": [
        {...},
      ]
    }
  ]
}
```




Attribute | Description
--------- | -----------
id | Unique ID that identifies the menu.
name | Name of the menu
description | Description of the menu
start_time | Start time when the menu is availble 
end_time | End time when the menu is availble 
items | Collection of Item objects that the menu contains

### Item object

Attribute | Description
--------- | -----------
id | Item unique ID 
name | Item name
description | Item description
base_price | Amount of the item in cents
modifiers_groups | Collection of Modifier Groups

### Modifier Group object

Attribute | Description
--------- | -----------
id | Modifier Group unique ID 
name | Modifier Group name
description | Modifier Group description
max_per_line_item | if defined the max amount of modifiers a line item can have
modifiers | Collection of Modifiers


### Modifier object

Attribute | Description
--------- | -----------
id | Modifier unique ID 
name | Modifier name
modifier_group_id | Modifier Group Id
price | Amount of the modifier in cents


## Find menus by store

> Example Request

```curl
curl "https://api.eatsa.com/v1/stores/518fdc10-5772-11e4-7ed6-0700200c9a11/menus" \
  -i -H "Content-Type:application/json; charset=utf-8"
```

> Example Response

```json
{
  "menus": [
    {
      "id": "e0f7b14b-d3c1-4df2-998e-13d0fcfa0293",
      "name": "Lunch",
      "description": "Lunch Menu",
      "start_time": "10:30:00",
      "end_time": "18:00:00",
      "items": [
        {
          "id": "59a8bdc2-d937-44bc-94dd-a1008331805c",
          "name": "Bibimbap Bowl",
          "description": "Steamed brown rice topped with a rainbow of veggies and a soft eatsa egg.",
          "base_price": 895,
          "modifiers_groups": [
            {
              "id": "21c740b8-7f8b-4585-aa78-0c66c7c9c398",
              "name": "Proteins",
              "short_name": "Meat",
              "description": "Meat - LUNCH",
              "sort_order": 7,
              "max_per_line_item": null,
              "modifiers": [
                {
                  "id": "f85384a5-260b-4912-8a04-35649270c623",
                  "name": "Turkey Loaf",
                  "modifier_group_id": "21c740b8-7f8b-4585-aa78-0c66c7c9c398",
                  "price": 0
                },
                {
                  "id": "dbf92910-7618-476a-91b1-0a5796d7b8a3",
                  "name": "Bulgogi Beef",
                  "modifier_group_id": "21c740b8-7f8b-4585-aa78-0c66c7c9c398",
                  "price": 0
                },
                {
                  "id": "c41308e1-d364-46a4-8c24-e92e27423d0d",
                  "name": "Citrus Pulled Pork",
                  "modifier_group_id": "21c740b8-7f8b-4585-aa78-0c66c7c9c398",
                  "price": 0
                },
                {
                  "id": "2a6f2ac1-bf67-41ae-8a75-cd169fcf0002",
                  "name": "Rosemary Chicken (Cold)",
                  "modifier_group_id": "21c740b8-7f8b-4585-aa78-0c66c7c9c398",
                  "price": 0
                }
              ]
            },
            {...}
          ]
        },
        {...}
      ]
    },
    {
      "id": "98597742-2086-45d4-bc39-72486c03ee9c",
      "name": "Breakfast",
      "description": "Jan 5th Menu",
      "start_time": "00:00:00",
      "end_time": "10:30:00",
      "items": [
        {...},
      ]
    }
  ]
}
```

Retrieve store menus.


### Endpoint

`GET https://api.eatsa.com/v1/stores/:storeId/menus`

### Request Arguments

Parameter | Required | Description
--------- | ------- | -----------
storeId | yes  | Store that contains the menus


### Response Arguments

Refer to menu object

