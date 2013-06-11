# Ace of Sales API Documentation

This is a REST-style API that uses JSON for serialization and [API token](#authentication) authentication. You can only access our API over HTTPS.

## Authentication

Every request must be made with the account's API token in the parameters of the request. Your account's API token can be found on the "User Settings" page inside of the "Your Account" area. For example, to access the contacts endpoint you would use the following:

```
/api/v1/contacts.json?auth_token=th3t0k3ng035r1ghth3r3
```

## Endpoints

The current version of the API is v1. This is reflected in the URL used to access the endpoint. For example, to access the contacts endpoint you would use the following:

```
/api/v1/contacts.json?auth_token=th3t0k3ng035r1ghth3r3
```


* [Contacts](https://github.com/aceofsales/api-docs/blob/master/endpoints/contacts.md)
  * [Addresses](https://github.com/aceofsales/api-docs/blob/master/endpoints/addresses.md)
  * [Emails](https://github.com/aceofsales/api-docs/blob/master/endpoints/emails.md)
  * [Phones](https://github.com/aceofsales/api-docs/blob/master/endpoints/phones.md)
  * [Web Addresses](https://github.com/aceofsales/api-docs/blob/master/endpoints/web_addresses.md)
* [Groups](https://github.com/aceofsales/api-docs/blob/master/endpoints/groups.md)
* [Orders](https://github.com/aceofsales/api-docs/blob/master/endpoints/orders.md)
  * [Recipients](https://github.com/aceofsales/api-docs/blob/master/endpoints/recipients.md)
  * [Clicks](https://github.com/aceofsales/api-docs/blob/master/endpoints/clicks.md)
* [Notes](https://github.com/aceofsales/api-docs/blob/master/endpoints/notes.md)
* [Events](https://github.com/aceofsales/api-docs/blob/master/endpoints/events.md)
* [Event Categories](https://github.com/aceofsales/api-docs/blob/master/endpoints/event_categories.md)


