# Events

## Supported Actions

* [Event](#event)
* [Get Events](#get-events)
* [Get Event](#get-event)
* [Create Event](#create-event)
* [Update Event](#update-event)
* [Delete Event](#delete-event)

## Event

**Required:** ```time``` ```category```

```json
{
  "id": 1,
  "time": 1366133271,
  "category": "Birthday",
  "details": "Lorem ipsum...",
  "created_at": 1366133271,
  "updated_at": 1366133271,
  "parent": "/contacts/:id.json" || "/groups/:id.json"
}
```

## Get Events

* ```GET /contacts/:contact_id/events.json``` returns all events for specified contact.
* ```GET /groups/:group_id/events.json``` returns all events for specified group.

Returns an array of events. (See [Event](#event) for JSON representation.)

## Get Event

 * ```GET /events/:id.json``` returns specified event. (See [Event](#event) for JSON representation.)

## Create Event

* ```POST /contacts/:contact_id/events.json``` creates a new event from parameters belonging to specified contact
* ```POST /groups/:group_id/events.json``` creates a new event from parameters belonging to specified group

```json
{
  "time": 1366133271,
  "category": "Follow-up"
}
```

On success, this returns ```201 Created```, [JSON representation](#event) in response body, and ```Location``` header with the location of the new event.

## Update Event

* ```PUT /events/:id.json``` updates event from parameters

```json
{
  "time": 1366133271,
  "details": "Lorem ipsum..."
}
```

On success, this returns ```200 OK``` and [JSON representation](#event) in response body.

## Delete Event

* ```DELETE /events/:id.json``` will delete the specified event and return ```204 No Content``` on success. If the user does not have permission to delete the event, it returns ```403 Forbidden```.


