# Recipients

## Supported Actions

* [Recipient Attributes](#recipient)
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
  "region": "Va",
  "postal_code": "24502",
  "country": "United States",
  "cc": false,
  "bcc": false,
  "clicks": 0,
  "views": 0,
  "viewed_at": 1366133271,
  "bounced": false,
  "unsubscribed_at": 1366133271,
  "sent_at": 1366133271,
  "created_at": 1366133271,
  "updated_at": 1366133271,
  "parent": "/orders/:id.json",
  "contact": "/contacts/:id.json"
}
```

## Get Recipients

* ```/orders/:order_id/recipients.json``` returns all recipients for specified order

Returns an array of recipients. See [Recipient](#recipient) for JSON representation.

## Get Recipient

* ```GET /recipients/:id.json``` returns specified recipient (See [Recipient](#recipient) for JSON representation)
