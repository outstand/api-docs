# Orders

* [Order Attributes](#order)

## Supported Actions

* [Order Attributes](#order)
* [Get Orders](#get-orders)
* [Get Order](#get-order)

## Order

```json
{
  "id": 1,
  "template_name": "Branded Email",
  "subject": "Lorem ipsum...",
  "copy_self": false,
  "total_price": 0,
  "recipients_count": 0,
  "opens": 0,
  "clicks": 0,
  "bounces": 0,
  "unsubscribes": 0,
  "scheduled_for": "2013-05-07T17:51:05Z",
  "created_at": "2013-05-07T17:51:05Z",
  "updated_at": "2013-05-07T17:51:05Z"
}
```

## Get Orders

* ```GET /orders.json``` returns all orders for the account

Returns an array of orders. See [Order](#order) for JSON representation.

## Get Order

* ```GET /orders/:id.json``` returns specified order (See [Order](#order) for JSON representation)


