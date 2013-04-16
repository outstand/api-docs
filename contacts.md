# Contacts

## Supported Actions

* [Get contacts](get-contacts)
* [Get contact](get-contact)

## Get Contacts

* ```/contacts.json``` returns all contacts for the account
* ```/groups/1/contacts.json``` returns all contacts for specified group

```json
[
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
]
```

## Get Contact

* ```GET /contacts/1.json``` returns specified contact

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
