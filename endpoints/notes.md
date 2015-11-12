# Notes

* [Note](#note)

## Supported Actions

* [Get Notes](#get-notes)
* [Get Note](#get-note)
* [Create Note](#create-note)
* [Update Note](#update-note)
* [Delete Note](#delete-note)

## Note

**Required:** ```title```

```json
{
  "id": 1,
  "title": "Example",
  "text": "Lorem ipsum...",
  "created_at": "2013-05-07T17:51:05Z",
  "updated_at": "2013-05-07T17:51:05Z",
  "parent": "/contacts/:id.json" || "/groups/:id.json"
}
```

## Get Notes

* ```GET /contacts/:contact_id/notes.json``` returns all notes for specified contact.
* ```GET /groups/:group_id/notes.json``` returns all notes for specified group.

Returns an array of notes. (See [Note](#note) for JSON representation.)

## Get Note

 * ```GET /notes/:id.json``` returns specified note. (See [Note](#note) for JSON representation.)

## Create Note

* ```POST /contacts/:contact_id/notes.json``` creates a new note from parameters belonging to specified contact
* ```POST /groups/:group_id/notes.json``` creates a new note from parameters belonging to specified group

```json
{
  "title": "Lunch meeting",
  "text": "Lorem ipsum..."
}
```

On success, this returns ```201 Created```, [JSON representation](#note) in response body, and ```Location``` header with the location of the new note.

## Update Note

* ```PUT /notes/:id.json``` updates note from parameters

```json
{
  "title": "Lunch meeting",
  "text": "Lorem ipsum..."
}
```

On success, this returns ```204 No Content```. If the request is invalid, a ```422 Unprocessable Entity``` is returned with the error(s) in the response body. (See [422 Unprocessable Entity](https://github.com/outstand/api-docs/blob/master/422.md))

## Delete Note

* ```DELETE /notes/:id.json``` will delete the specified note and return ```204 No Content``` on success. If the user does not have permission to delete the note, it returns ```404 Not Found```.

