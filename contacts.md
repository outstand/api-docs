# Contacts

## Supported Actions

* [Contact Attributes](contact)
* [Get Contacts](get-contacts)
* [Get Contact](get-contact)
* [Create Contact](create-contact)
* [Update Contact](update-contact)
* [Delete Contact](delete-contact)

## Contact

*Note:* First & last name are required.

```json
{
  "id": 1,
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
  "created_at": 1366133271,
  "updated_at": 1366133271
}
```

## Get Contacts

* ```/contacts.json``` returns all contacts for the account
* ```/groups/:group_id/contacts.json``` returns all contacts for specified group

Returns an array of contacts. See [Contact](contact) for JSON representation.

## Get Contact

* ```GET /contacts/:id.json``` returns specified contact (see [Contact](contact) for JSON representation)


## Create Contact

* ```POST /contacts.json``` creates a new contact from parameters
* ```POST /groups/:group_id/contacts.json``` creates a new contact from parameters and adds to specified group

```json
{
  "first_name" : "John",
  "last_name" : "Smith"
}
```

On success, this returns ```201 Created```, JSON representation in response body, and ```Location``` header of the new contact.

## Update Contact

* ```PUT /contacts/:id.json``` updates contact from parameters

```json
{
  "first_name" : "Jack",
  "middle_initial" : "J"
}
```

On success, this returns ```200 OK``` and JSON representation in response body

## Delete Contact

* ```DELETE /contacts/:id.json``` will delete the specified contact and return ```204 No Content``` on success. If the user does not have permission to delete the contact, it returns ```403 Forbidden```.
