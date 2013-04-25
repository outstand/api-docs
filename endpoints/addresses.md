# Contact Addresses

## Supported Actions

* [Address](#address)
* [Get Addresses](#get-addresses)
* [Get Address](#get-address)
* [Create Address](#create-address)
* [Update Address](#update-address)
* [Delete Address](#delete-address)

## Address

**Note:** At least one field must be filled in to create an address.
Valid locations are: ```Work```, ```Home```, and ```Other```.

```json
{
  "id": 1,
  "full_address": "110 Northwynd Circle, Suite B, Lynchburg, Va, 24502, United States",
  "address_line_1": "110 Northwynd Circle",
  "address_line_2": "Suite B",
  "city": "Lynchburg",
  "region": "Va",
  "postal_code": "24502",
  "country": "United States",
  "location": "Work",
  "created_at": 1366133271,
  "updated_at": 1366133271,
  "contact": "/contacts/:id.json"
}
```

## Get Addresses

* ```GET /contacts/:contact_id/addresses.json``` returns all addresses for specified contact.

Returns an array of addresses. (See [Address](#address) for JSON representation.)

## Get Address

 * ```GET /addresses/:id.json``` returns specified address. (See [Address](#address) for JSON representation.)

## Create Address

* ```POST /contacts/:contact_id/addresses.json``` creates a new address from parameters belonging to specified contact

```json
{
  "address_line_1": "110 B Northwynd Circle",
  "city": "Lynchburg",
  "region": "Va",
  "postal_code": "24502",
  "location": "Work",
}
```

On success, this returns ```201 Created```, [JSON representation](#address) in response body, and ```Location``` header with the location of the new address.

## Update Address

* ```PUT /addresses/:id.json``` updates address from parameters

```json
{
  "address_line_1": "110 B Northwynd Circle",
  "city": "Lynchburg",
  "region": "Va",
  "postal_code": "24502",
  "location": "Work",
}
```

On success, this returns ```200 OK``` and [JSON representation](#address) in response body.

## Delete Address

* ```DELETE /addresses/:id.json``` will delete the specified address and return ```204 No Content``` on success. If the user does not have permission to delete the address, it returns ```404 Not Found```.


