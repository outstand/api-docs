# Contacts

* [Contact Attributes](#contact)

## Supported Actions

* [Get Contacts](#get-contacts)
* [Get Contact](#get-contact)
* [Create Contact](#create-contact)
* [Batch Create Contacts](#batch-create-contacts)
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
  "company_name": "Outstand",
  "primary_phone": "800-865-7496",
  "primary_email": "john@outstand.com",
  "primary_address": {
    "full_address": "110 Northwynd Circle, Suite B, Lynchburg, Va, 24502, United States",
    "address_line_1": "110 Northwynd Circle",
    "address_line_2": "Suite B",
    "city": "Lynchburg",
    "state_region_province": "Va",
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

* ```GET /contacts.json``` returns a paginated list of contacts for the account
* ```GET /groups/:group_id/contacts.json``` returns a paginated list of contacts for specified group

Returns a ```200 OK``` with an array of contacts. (See [Contact](#contact) for JSON representation.) If you request a page of contacts that does not exist, a ```404 Not Found``` will be returned. (See [Pagination](https://github.com/outstand/api-docs#pagination))

When specifying a group, if the group does not exist a ```404 Not Found``` will be returned.

### Optional Query Params

* `q` full-text search across: `first_name`, `last_name`, `company_name`, `title`, `primary_email`, `primary_address.city`, `primary_address.state_region_province`, `primary_address.postal_code`, `primary_phone`
* `page` & `per_page` see [Pagination](https://github.com/outstand/api-docs#pagination)
* `sort_by` supports the following values: `created_at`, `company_name`, `title`, `first_name`, `last_name`, `primary_email_address`. Default: `last_name`
* `direction` supports the following values: `asc`, `desc`. Default: `asc`

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

On success, this returns ```201 Created```, [JSON representation](#contact) in response body, and ```Location``` header with the location of the new contact. If the request is invalid, a ```422 Unprocessable Entity``` is returned with the error(s) in the response body. (See [422 Unprocessable Entity](https://github.com/outstand/api-docs/blob/master/422.md))

You can create a contact, email, phone, and address in one step.  Here's an example POST body:

```json
{
  "first_name": "John",
  "middle_initial": "P",
  "last_name": "Smith",
  "company_name": "Trouble, Inc.",
  "title": "Chief Troublemaker",
  "emails": [
    {
      "address": "john@outstand.com"
    },
    {
      "address": "notjohn@outstand.com"
    }
  ],
  "phones": [{
    "number": "555 555 1212",
    "location": "Work"
  }],
  "addresses": [{
    "location": "Work",
    "address_line_1": "Suite 302",
    "address_line_2": "57 S. Main St",
    "city": "Harrisonburg",
    "state_region_province": "VA",
    "postal_code": "22801",
    "country": "United States"
  }]
}
```

## Batch Create Contacts

* ```POST /contacts/batch.json``` creates an async contact import from parameters

```json
{
  "contacts": [
    {
      "first_name": "John",
      "middle_initial": "P",
      "last_name": "Smith"
      "company_name": "Trouble, Inc.",
      "title": "Chief Troublemaker",
      "emails": [
        {
          "address": "john@outstand.com"
        },
        {
          "address": "notjohn@outstand.com"
        }
      ],
      "phones": [{
        "number": "555 555 1212",
        "location": "Work"
      }],
      "addresses": [{
        "location": "Work",
        "address_line_1": "Suite 302",
        "address_line_2": "57 S. Main St",
        "city": "Harrisonburg",
        "state_region_province": "VA",
        "postal_code": "22801",
        "country": "United States"
      }],
      "web_addresses": [
        {
          "url": "https://example.com",
          "url_type": "Website"
        }
      ]
    },
    {
      "first_name": "Jane",
      "last_name": "Smith"
    }
  ]
}
```

On success, this returns ```201 Created```, with an unhelpful Import JSON response.


## Update Contact

* ```PUT /contacts/:id.json``` updates contact from parameters

Contacts have four different related types: phones, emails, addresses, and web_addresses.  Additionally, phones, emails, and addresses can have primaries set.
The update contact endpoint supports two modes of operation with regards to those related types: normal and replace. In normal mode, you can add and update existing related types. You can use replace mode to overwrite or delete existing data.

You can invoke replace mode by sending the header `X-Outstand-Replace: true`.  Any other value (or the header's absence) will result in normal mode.

#### Example

Let's assume this contact already has a phone with id `1`, an email with id `10`, an address with id `20`, and a web address with id `30`.  Now let's assume we receive the following update.

```json
{
  "first_name" : "Jack",
  "middle_initial" : "J",
  "phones": [
    {
      "id": 1
    },
    {
      "number": "555 555 1212",
      "location": "Work"
    }
  ],
  "emails": [
    {
      "id": 10,
      "address": "bob@example.com"
    },
    {
      "address": "john@example.com"
    }
  ],
  "addresses": [
    {
      "location": "Work",
      "address_line_1": "Suite 302",
      "address_line_2": "57 S. Main St",
      "city": "Harrisonburg",
      "state_region_province": "VA",
      "postal_code": "22801",
      "country": "United States"
    }
  ],
  "web_addresses": [
    {
      "id": 30
    }
  ]
}
```

In normal mode the following would happen:
- Phone id `1` would be ignored
- A new phone would be added with the number '555 555 1212'
- Email id `10` would have its address updated
- A new email would be added with the address `john@example.com`
- Address id `20` is not included in the payload and would remain
- A new address would be added with the above attributes
- Web address id `30` would be ignored

In replace mode the following would happen:
- Phone id `1` would be retained
- A new phone would be added with the number '555 555 1212'
- Email id `10` would have its address updated
- A new email would be added with the address `john@example.com`
- Address id `20` is not included in the payload and would be deleted
- A new address would be added with the above attributes
- Web address id `30` would be retained

If a related type that is also a primary is deleted (example: phone id `1` is also the primary_phone_id) then the primary is set to `nil` except in cases where there is only one other record which is then promoted to primary (example: we have a second phone number already).


#### Setting Primaries

To update the primaries (email, mailing address, and phone number) for the contact use the following: (where 1 is the id of the email, mailing address or phone number)

```json
{
  "primary_email_id" : 1,
  "primary_address_id" : 1,
  "primary_phone_id" : 1
}
```

#### Response

On success, this returns ```200 OK``` with the updated contact returned in the response body. If the request is invalid, a ```422 Unprocessable Entity``` is returned with the error(s) in the response body. (See [422 Unprocessable Entity](https://github.com/outstand/api-docs/blob/master/422.md))

## Delete Contact

* ```DELETE /contacts/:id.json``` will delete the specified contact and return ```204 No Content``` on success. If the user does not have permission to delete the contact, it returns ```404 Not Found```.
