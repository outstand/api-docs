# Events

* [Event](#event)

## Supported Actions

* [Get Events](#get-events)
* [Get Event](#get-event)
* [Create Event](#create-event)
* [Update Event](#update-event)
* [Delete Event](#delete-event)

## Event

**Required:** ```time```, ```category_name``` or ```category_id```

```json
{
  "id": 1,
  "time": "2013-05-07T17:51:05Z",
  "category_name": "Birthday",
  "category_id" : 1,
  "details": "Lorem ipsum...",
  "recurrence": "Yearly",
  "created_at": "2013-05-07T17:51:05Z",
  "updated_at": "2013-05-07T17:51:05Z",
  "parent": "/contacts/:id.json" || "/groups/:id.json"
}
```

The valid values for ```recurrence``` are: Never Daily Weekly Monthly Yearly

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
  "time": "2013-05-07T17:51:05Z",
  "category_name": "Follow-up"
}
```

On success, this returns ```201 Created```, [JSON representation](#event) in response body, and ```Location``` header with the location of the new event. If we are unable to find a category with the ```category_name``` or ```category_id``` a ```422 Unprocessable Entity``` is returned. If you send a ```category_id``` and ```category_name``` to create the event, the ```category_id``` takes precedence.

## Update Event

* ```PUT /events/:id.json``` updates event from parameters

```json
{
  "time": "2013-05-07T17:51:05Z",
  "details": "Lorem ipsum..."
}
```

On success, this returns ```204 No Content```. If the request is invalid, a ```422 Unprocessable Entity``` is returned with the error(s) in the response body. (See [422 Unprocessable Entity](https://github.com/outstand/api-docs/blob/master/422.md))

## Delete Event

* ```DELETE /events/:id.json``` will delete the specified event and return ```204 No Content``` on success. If the user does not have permission to delete the event, it returns ```404 Not Found```.


