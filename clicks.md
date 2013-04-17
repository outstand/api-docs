# Clicks

## Supported Actions

* [Click Attributes](#click)
* [Get Clicks](#get-clicks)
* [Get Click](#get-click)

## Click

```json
{
  "id": 1,
  "first_name": "John",
  "middle_initial": "J",
  "last_name": "Smith",
  "title": "Vice President",
  "company_name": "Ace of Sales",
  "email": "john@aceofsales.com",
  "clicks": 0,
  "url": 0,
  "created_at": 1366133271,
  "updated_at": 1366133271,
  "parent": "/orders/:id.json",
  "recipient": "/recipients/:id.json"
}
```

## Get Clicks

* ```/orders/:order_id/clicks.json``` returns all clicks for specified order

Returns an array of clicks. See [Click](#click) for JSON representation.

## Get Click

* ```GET /clicks/:id.json``` returns specified click (See [Click](#click) for JSON representation)

