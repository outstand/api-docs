# Contact Email Addresses

* [Email](#email)

## Supported Actions

* [Get Emails](#get-emails)
* [Get Email](#get-email)
* [Create Email](#create-email)
* [Update Email](#update-email)
* [Delete Email](#delete-email)

## Email

**Required:** ```address```

```json
{
  "id": 1,
  "address": "john@aceofsales.com",
  "created_at": "2013-05-07T17:51:05Z",
  "updated_at": "2013-05-07T17:51:05Z",
  "contact": "/contacts/:id.json"
}
```

## Get Emails

* ```GET /contacts/:contact_id/emails.json``` returns all emails for specified contact.

Returns an array of emails. (See [Email](#email) for JSON representation.)

## Get Email

 * ```GET /emails/:id.json``` returns specified email. (See [Email](#email) for JSON representation.)

## Create Email

* ```POST /contacts/:contact_id/emails.json``` creates a new email from parameters belonging to specified contact

```json
{
  "address" : "john@example.com"
}
```

On success, this returns ```201 Created```, [JSON representation](#email) in response body, and ```Location``` header with the location of the new email.

## Update Email

* ```PUT /emails/:id.json``` updates email from parameters

```json
{
  "address" : "john@example.com"
}
```

On success, this returns ```204 No Content```. If the request is invalid, a ```422 Unprocessable Entity``` is returned with the error(s) in the response body. (See [422 Unprocessable Entity](https://github.com/aceofsales/api-docs/blob/master/422.md))

## Delete Email

* ```DELETE /emails/:id.json``` will delete the specified email and return ```204 No Content``` on success. If the user does not have permission to delete the email, it returns ```404 Not Found```.
