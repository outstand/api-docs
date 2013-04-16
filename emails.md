# Contact Email Addresses

## Supported Actions

* [Email](#email)
* [Get Emails](#get-emails)
* [Get Email](#get-email)
* [Create Email](#create-email)
* [Update Email](#update-email)
* [Delete Email](#delete-email)

## Email

*Note:* ```address``` is required.

```json
{
  "id": 1,
  "address": "john@aceofsales.com",
  "created_at": 1366133271,
  "updated_at": 1366133271,
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

On success, this returns ```200 OK``` and [JSON representation](#email) in response body.

## Delete Email

* ```DELETE /emails/:id.json``` will delete the specified email and return ```204 No Content``` on success. If the user does not have permission to delete the email, it returns ```403 Forbidden```.
