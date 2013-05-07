# Contact Phone Numbers

* [Phone](#phone)

## Supported Actions

* [Get Phones](#get-phones)
* [Get Phone](#get-phone)
* [Create Phone](#create-phone)
* [Update Phone](#update-phone)
* [Delete Phone](#delete-phone)

## Phone

**Required:** ```number``` ```location```
Valid locations are: ```Work```, ```Home```, ```Mobile```, ```Skype```, ```Toll-Free```, ```Fax```, and ```Other```.

```json
{
  "id": 1,
  "number": "800-865-7496",
  "location": "Work",
  "created_at": "2013-05-07T17:51:05Z",
  "updated_at": "2013-05-07T17:51:05Z",
  "contact": "/contacts/:id.json"
}
```

## Get Phones

* ```GET /contacts/:contact_id/phones.json``` returns all phones for specified contact.

Returns an array of phones. (See [Phone](#phone) for JSON representation.)

## Get Phone

 * ```GET /phones/:id.json``` returns specified phone. (See [Phone](#phone) for JSON representation.)

## Create Phone

* ```POST /contacts/:contact_id/phones.json``` creates a new phone from parameters belonging to specified contact

```json
{
  "number" : "800-444-5555",
  "location" : "Work"
}
```

On success, this returns ```201 Created```, [JSON representation](#phone) in response body, and ```Location``` header with the location of the new phone.

## Update Phone

* ```PUT /phones/:id.json``` updates phone from parameters

```json
{
  "number" : "800-444-5555",
  "location" : "Mobile"
}
```

On success, this returns ```200 OK``` and [JSON representation](#phone) in response body.

## Delete Phone

* ```DELETE /phones/:id.json``` will delete the specified phone and return ```204 No Content``` on success. If the user does not have permission to delete the phone, it returns ```404 Not Found```.

