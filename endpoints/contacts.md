# Contacts

* [Contact Attributes](#contact)

## Supported Actions

* [Get Contacts](#get-contacts)
* [Get Contact](#get-contact)
* [Create Contact](#create-contact)
* [Update Contact](#update-contact)
* [Delete Contact](#delete-contact)

## Contact

*Note:* ```first_name``` & ```last_name``` are required.

```json
{
  "id": 1,
  "full_name": "John J. Smith",
  "first_name": "John",
  "middle_initial": "J",
  "last_name": "Smith",
  "title": "Vice President",
  "company_name": "Ace of Sales",
  "primary_phone": "800-865-7496",
  "primary_email": "john@aceofsales.com",
  "primary_address": {
    "full_address": "110 Northwynd Circle, Suite B, Lynchburg, Va, 24502, United States",
    "address_line_1": "110 Northwynd Circle",
    "address_line_2": "Suite B",
    "city": "Lynchburg",
    "region": "Va",
    "postal_code": "24502",
    "country": "United States"
  },
  "description": "Lorem ipsum...",
  "motives": "Lorem ipsum...",
  "questions_ideas_actions": "Lorem ipsum...",
  "favorites": "Lorem ipsum...",
  "friends_and_family": "Lorem ipsum...",
  "created_at": "2013-05-07T17:51:05Z",
  "updated_at": "2013-05-07T17:51:05Z"
}
```

## Get Contacts

* ```GET /contacts.json``` returns all contacts for the account
* ```GET /groups/:group_id/contacts.json``` returns all contacts for specified group

Returns a ```200 OK``` with an array of contacts. (See [Contact](#contact) for JSON representation.) If you request a page of contacts that does not exist, a ```404 Not Found``` will be returned.

When specifying a group, if the group does not exist a ```404 Not Found``` will be returned.

## Get Contact

* ```GET /contacts/:id.json``` returns specified contact (See [Contact](#contact) for JSON representation)

Returns a ```200 OK``` on success and ```404 Not Found``` if contact does not exist.

## Create Contact

* ```POST /contacts.json``` creates a new contact from parameters
* ```POST /groups/:group_id/contacts.json``` creates a new contact from parameters and adds to specified group

```json
{
  "first_name" : "John",
  "last_name" : "Smith"
}
```

On success, this returns ```201 Created```, [JSON representation](#contact) in response body, and ```Location``` header with the location of the new contact. If the request is invalid, a ```422 Unprocessable Entity``` is returned with the error(s) in the response body. (See [422 Unprocessable Entity](https://github.com/aceofsales/api-docs/blob/master/422.md))

You can create a contact, email, phone, and address in one step.  Here's an example POST body

```json
{
  "first_name": "Myers",
  "last_name": "Carpenter",
  "company_name": "Trouble, Inc.",
  "title": "Chief Troublemaker",
  "emails": [
    {
      "address": "john@aceofsales.com",
    },
    {
      "address": "notjohn@aceofsales.com",
    }
  ],
  "phones": [{
    "number": "555 555 1212",
    "location": "Work",
  }],
  "addresses": [{
    "location": "Work",
    "address_line_1": "57 S. Main St, Suite 302",
    "address_line_2": None,
    "city": "Harrisonburg",
    "state_region_province": "VA",
    "postal_code": "22801",
    "country": "United States"
  }]
}
```

## Update Contact

* ```PUT /contacts/:id.json``` updates contact from parameters

```json
{
  "first_name" : "Jack",
  "middle_initial" : "J"
}
```

To update the primaries (email, mailing address, and phone number) for the contact use the following: (where 1 is the id of the email, mailing address or phone number)

```json
{
  "primary_email_id" : 1,
  "primary_address_id" : 1,
  "primary_phone_id" : 1
}
```

On success, this returns ```204 No Content```. If the request is invalid, a ```422 Unprocessable Entity``` is returned with the error(s) in the response body. (See [422 Unprocessable Entity](https://github.com/aceofsales/api-docs/blob/master/422.md))

## Delete Contact

* ```DELETE /contacts/:id.json``` will delete the specified contact and return ```204 No Content``` on success. If the user does not have permission to delete the contact, it returns ```404 Not Found```.
