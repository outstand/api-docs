# Outstand API Documentation

This is a REST-style API that uses JSON for serialization and [API token](#authentication) authentication. You can only access our API over HTTPS at https://app.outstand.com.

## Authentication

Every request must be made with the account's API token in the parameters of the request. Your account's API token can be found on the "User Settings" page inside of the "Your Account" area. For example, to access the contacts endpoint you would use the following:

```
https://app.outstand.com/api/v1/contacts.json?auth_token=th3t0k3ng035r1ghth3r3
```

## Endpoints

The current version of the API is v1. This is reflected in the URL used to access the endpoint. For example, to access the contacts endpoint you would use the following:

```
/api/v1/contacts.json?auth_token=th3t0k3ng035r1ghth3r3
```


* [Contacts](https://github.com/outstand/api-docs/blob/master/endpoints/contacts.md)
  * [Addresses](https://github.com/outstand/api-docs/blob/master/endpoints/addresses.md)
  * [Emails](https://github.com/outstand/api-docs/blob/master/endpoints/emails.md)
  * [Phones](https://github.com/outstand/api-docs/blob/master/endpoints/phones.md)
  * [Web Addresses](https://github.com/outstand/api-docs/blob/master/endpoints/web_addresses.md)
* [Groups](https://github.com/outstand/api-docs/blob/master/endpoints/groups.md)
* [Orders](https://github.com/outstand/api-docs/blob/master/endpoints/orders.md)
  * [Recipients](https://github.com/outstand/api-docs/blob/master/endpoints/recipients.md)
  * [Clicks](https://github.com/outstand/api-docs/blob/master/endpoints/clicks.md)
* [Notes](https://github.com/outstand/api-docs/blob/master/endpoints/notes.md)
* [Events](https://github.com/outstand/api-docs/blob/master/endpoints/events.md)
* [Event Categories](https://github.com/outstand/api-docs/blob/master/endpoints/event_categories.md)


## Pagination

You can paginate the result set by passing in the following parameters for the request:

```
/api/v1/contacts.json?page=1&per_page=50
```

When you request a page that does not exist you will receive a ```404 Not Found```.

*Note:* ```page``` defaults to 1 and ```per_page``` defaults to the maximum of 100.
