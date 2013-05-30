# Clicks

* [Click Attributes](#click)

## Supported Actions

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
  "url": "http://example.com",
  "created_at": "2013-05-07T17:51:05Z",
  "updated_at": "2013-05-07T17:51:05Z",
  "parent": "/orders/:id.json",
  "recipient": "/recipients/:id.json"
}
```

## Get Clicks

* ```GET /orders/:order_id/clicks.json``` returns all clicks for specified order

Returns an array of clicks. See [Click](#click) for JSON representation.

## Get Click

* ```GET /clicks/:id.json``` returns specified click (See [Click](#click) for JSON representation)

