# Contact Messages

* [Message Attributes](#message)

## Supported Actions

* [GET Messages](#get-messages)

## Message

```json
{
  "id": 12913984,
  "order_id": 1949204,
  "subject": "3KIM-TFA – 95% of women fall into this category...",
  "template_name": "Email Greeting",
  "message_url": "https://...",
  "scheduled_for": "2015-11-12T21:21:24Z",
  "sent_at": "2015-11-12T21:21:33Z",
  "opened_at": "2015-11-12T21:24:30Z",
  "opens": 1,
  "clicks": 1,
  "bounce_code": "100",
  "unsubscribed_at": "2015-11-12T21:21:33Z",
  "spam_report_at": "2015-11-12T21:21:33Z"
}
```

## GET Messages

* ```GET /contacts/:contact_id/messages.json``` returns a paginated list of messages for the contact. (See [Pagination](https://github.com/outstand/api-docs#pagination))
