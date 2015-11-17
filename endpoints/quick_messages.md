# Quick Messages

## Supported Actions

* [POST Quick Message](#post-quick-message)

## Create Quick Message

* `POST /quick_messages` creates a new message for a contact using specified saved message and profile.

Required POST body:
```json
{
  "contact_id": 1,
  "profile_id": 2,
  "saved_message_id": "563bbc7c79e68b3351000070"
}
```

On success, this returns `201 Created`, [JSON representation](https://github.com/outstand/api-docs/blob/master/endpoints/orders.md#order) in the response body. If the request is invalid, a `422 Unprocessable Entity` is returned with the error(s) in the response body. (See [422 Unprocessable Entity](https://github.com/outstand/api-docs/blob/master/422.md))
