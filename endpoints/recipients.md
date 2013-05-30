# Recipients

* [Recipient Attributes](#recipient)

## Supported Actions

* [Get Recipients](#get-recipients)
* [Get Recipient](#get-recipient)

## Recipient

```json
{
  "id": 1,
  "first_name": "John",
  "middle_initial": "J",
  "last_name": "Smith",
  "title": "Vice President",
  "company_name": "Ace of Sales",
  "email": "john@aceofsales.com",
  "address_line_1": "110 Northwynd Circle",
  "address_line_2": "Suite B",
  "city": "Lynchburg",
  "state_region_province": "Va",
  "postal_code": "24502",
  "country": "United States",
  "cc": false,
  "bcc": false,
  "clicks": 0,
  "views": 0,
  "bounced": false,
  "viewed_at": "2013-05-07T17:51:05Z",
  "unsubscribed_at": "2013-05-07T17:51:05Z",
  "sent_at": "2013-05-07T17:51:05Z",
  "created_at": "2013-05-07T17:51:05Z",
  "updated_at": "2013-05-07T17:51:05Z",
  "parent": "/orders/:id.json",
  "contact": "/contacts/:id.json"
}
```

## Get Recipients

* ```GET /orders/:order_id/recipients.json``` returns all recipients for specified order

Returns an array of recipients. See [Recipient](#recipient) for JSON representation.

## Get Recipient

* ```GET /recipients/:id.json``` returns specified recipient (See [Recipient](#recipient) for JSON representation)
