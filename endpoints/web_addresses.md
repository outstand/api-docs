# Contact Web Addresses

* [Web Address](#web-address)

## Supported Actions

* [Get Web Addresses](#get-web-addresses)
* [Get Web Address](#get-web-address)
* [Create Web Address](#create-web-address)
* [Update Web Address](#update-web-address)
* [Delete Web Address](#delete-web-address)

## Web Address

**Required:** ```url``` ```url_type```
Valid ```url_type``` are: ```Website```, ```LinkedIn```, ```Facebook```, ```Twitter```, ```Blog```, and ```YouTube```.

```json
{
  "id": 1,
  "url": "http://www.example.com",
  "url_type": "Website",
  "created_at": "2013-05-07T17:51:05Z",
  "updated_at": "2013-05-07T17:51:05Z",
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

On success, this returns ```201 Created```, [JSON representation](#web-address) in response body, and ```Location``` header with the location of the new web address.

## Update Web Address

* ```PUT /web_addresses/:id.json``` updates web address from parameters

```json
{
  "url" : "http://www.example.com",
  "url_type" : "Website"
}
```

On success, this returns ```204 No Content```. If the request is invalid, a ```422 Unprocessable Entity``` is returned with the error(s) in the response body. (See [422 Unprocessable Entity](https://github.com/outstand/api-docs/blob/master/422.md))

## Delete Web Address

* ```DELETE /web_addresses/:id.json``` will delete the specified web address and return ```204 No Content``` on success. If the user does not have permission to delete the web address, it returns ```404 Not Found```.


