# Contact Web Addresses

## Supported Actions

* [Web Address](#web-address)
* [Get Web Addresses](#get-web-addresses)
* [Get Web Address](#get-web-address)
* [Create Web Address](#create-web-address)
* [Update Web Address](#update-web-address)
* [Delete Web Address](#delete-web-address)

## Web Address

*Note:* ```url``` & ```url_type``` are required. Valid ```url_type``` are: ```Website```, ```LinkedIn```, ```Facebook```, ```Twitter```, ```Blog```, and ```YouTube```.

```json
{
  "id": 1,
  "url": "http://www.example.com",
  "url_type": "Website",
  "created_at": 1366133271,
  "updated_at": 1366133271,
  "contact": "/contacts/:id.json"
}
```

## Get Web Addresses

* ```GET /contacts/:contact_id/web_addresses.json``` returns all web addresses for specified contact.

Returns an array of web addresses. (See [Web Address](#web-address) for JSON representation.)

## Get Web Address

 * ```GET /web_addresses/:id.json``` returns specified web address. (See [Web Address](#web-address) for JSON representation.)

## Create Web Address

* ```POST /contacts/:contact_id/web_addresses.json``` creates a new web address from parameters belonging to specified contact

```json
{
  "url" : "http://www.example.com",
  "url_type" : "Website"
}
```

On success, this returns ```201 Created```, JSON representation in response body, and ```Location``` header with the location of the new web address.

## Update Web Address

* ```PUT /web_addresses/:id.json``` updates web address from parameters

```json
{
  "url" : "http://www.example.com",
  "url_type" : "Website"
}
```

On success, this returns ```200 OK``` and JSON representation in response body.

## Delete Web Address

* ```DELETE /web_addresses/:id.json``` will delete the specified web address and return ```204 No Content``` on success. If the user does not have permission to delete the web address, it returns ```403 Forbidden```.


