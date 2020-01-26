# Orders API for Picking App

_Last updated: Jan 26, 2020_

Some guidelines for the **Picking App**.

1. Server randomly assign an order for picking
2. Only one order should be picked at any given time
3. Vendor portal should have feature to recall the order if the picking takes too long, for example after extended period of time. This could happen in case of human negligence or app crash.

## 1. Fetch Order for Picking

```
GET /api/orders?q=get_next_to_pick
```

**Returns:**

- status: NOT_FOUND -> no new order is available
- status: 200 -> Successful

```
{   "_id": 123456789,
    "lines": [
        "product_id": "xxx"
        "name": "xxx"
        "barcode": "12345"
        "quantity": 999
        "wholesale": {
            content_quantity: 99
            quantity: 99
        }
    ],
    "status": "preparing"
}
```

**Notes:**

A new order will be retrieved with status will be changed to pick/started and timestamp recorded.

## 2. Change Item quantity During Picking

During picking, you can change the quantity of the items being picked. Suki automatically recalculates the individual line price and total price.

```
PUT /api/orders/{id}
```

```json
{
    "lines": [ {
        "product_id": "xxx" // item id
        "quantity": 10 // new quantity
      }
    ]
}
```

If you would like to **delete** an item, simply change the quantity to 0.

## 3. Adding Item during Picking

To add an item, you simply introduce the include the new item's id and quantity. Using the same API call PUT.

```
PUT /api/orders/{id}
```

```json
{
    "lines": [ {
        "product_id": "yyy"  // new item id
        "quantity": 10  // new item's quanitty
      }
    ]
}
```

Of course, you may combined multiple lines in a single API call. In this case, you can change one item'q quantity, delete another item, or add a new item.

## 4. Picking Completed

```
PUT /api/orders/{id}/mark_as_picked
```

Body

```
{
  "lines": [
    {
      "product_id": xxx,
      "quantity": xxx
    }
  ]
}
```

**Returns:**

- status: 4xx, 5xx, Error with message
- status: 200, successful

When successful, status will be changed to 'pick/ended' and time will be recorded.

**Notes:**

- Quantities may be edited,
- Zero quantity means lines is to be deleted
- New Items may be added

## 5. Abort Picking

```
PUT /api/orders/{id}/abort_pick
```

## 6. Get New document count

```
GET /api/orders?q=count&status=new
```
