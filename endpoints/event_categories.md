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
  "created_at": 1366133271,
  "updated_at": 1366133271
}
```

## Get Event Categories

* ```GET /event_categories.json``` returns all event categories available to the account

Returns a ```200 OK``` with an array of event categories. (See [Event Category](#event-category) for JSON representation.)

