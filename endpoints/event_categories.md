# Event Categories

* [Event Category](#event-category)

## Supported Actions

* [Get Event Categories](#get-event-categories)

## Event Category

**Required:** ```name```

```json
{
  "id": 1,
  "name": "Birthday",
  "created_at": "2013-05-07T17:51:05Z",
  "updated_at": "2013-05-07T17:51:05Z"
}
```

## Get Event Categories

* ```GET /event_categories.json``` returns all event categories available to the account

Returns a ```200 OK``` with an array of event categories. (See [Event Category](#event-category) for JSON representation.)

