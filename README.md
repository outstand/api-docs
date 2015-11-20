# Outstand API Documentation

This is a REST-style API that uses JSON for serialization and [API token](#authentication) authentication. You can only access our API over HTTPS at https://app.outstand.com.

## Authentication

### OAuth 2 Authentication

This is our preferred way of allowing users to grant access to their accounts from third party applications. This way our users have complete control over access to their data without giving out their password.

1. [Grab an OAuth 2 library](http://oauth.net/code/)
2. Contact support to register your application and provide us with a `redirect_uri`. You will then be assigned a `client_id` and `client_secret`. (The `redirect_uri` is where we will send the verification code. e.g. `https://example.com/auth/outstand/callback`)
3. Configure your OAuth 2 library with:
  * `client_id`, `client_secret`, and `redirect_uri`
  * `https://app.outstand.com/oauth/authorize` to request authorization
  * `https://app.outstand.com/oauth/token` to get access tokens
4. Try making an authorized request to `https://app.outstand.com/oauth/token/info`

If you are **not** using a library, you will need to request access:

```
https://app.outstand.com/oauth/authorize?client_id=[client_id]&redirect_uri=[redirect_uri]&response_type=code
```

We will then authenticate the user, ask them to authorize your application, and redirect the user back to your application with an authorization code. (This authorization code is good for 10 minutes.)

Your application must then make a request to trade your authorization code for an access token:

```
POST https://app.outstand.com/oauth/token
```

with a body of:
```json
{
  "client_id": [client_id],
  "client_secret": [client_secret],
  "code": [authorization code],
  "grant_type": "authorization_code",
  "redirect_uri": "https://example.com/auth/outstand/callback"
}
```

You'll receive a `200 OK` with the following response body:

```json
{
  "access_token": "...",
  "token_type": "bearer",
  "expires_in": 7200,
  "refresh_token": "...",
  "created_at": 1447820578
}
```

Your application will then use the `access_token` with your API requests by setting the Authorization header:

```
Authorization: Bearer ACCESS_TOKEN
```

Access tokens are valid for 2 hours. Once the access token has expired, use the refresh token to get a new access token. To refresh the access token:

```
POST https://app.outstand.com/oauth/token
```

with body:

```json
{
  "client_id": [client_id],
  "client_secret": [client_secret],
  "code": [refresh token],
  "grant_type": "refresh_token",
  "redirect_uri": "https://example.com/auth/outstand/callback"
}
```

You'll receive a `200 OK` with a new `access_token` and `refresh_token` in the response body.

### Token Authentication (Deprecated)

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
  * [Messages](https://github.com/outstand/api-docs/blob/master/endpoints/contact_messages.md)
  * [Web Addresses](https://github.com/outstand/api-docs/blob/master/endpoints/web_addresses.md)
* [Groups](https://github.com/outstand/api-docs/blob/master/endpoints/groups.md)
* [Orders](https://github.com/outstand/api-docs/blob/master/endpoints/orders.md)
  * [Recipients](https://github.com/outstand/api-docs/blob/master/endpoints/recipients.md)
  * [Clicks](https://github.com/outstand/api-docs/blob/master/endpoints/clicks.md)
* [Notes](https://github.com/outstand/api-docs/blob/master/endpoints/notes.md)
* [Events](https://github.com/outstand/api-docs/blob/master/endpoints/events.md)
* [Event Categories](https://github.com/outstand/api-docs/blob/master/endpoints/event_categories.md)
* [Profiles](https://github.com/outstand/api-docs/blog/master/endpoints/profiles.md)
* [Saved Messages](https://github.com/outstand/api-docs/blog/master/endpoints/saved_messages.md)
* [Quick Messages](https://github.com/outstand/api-docs/blog/master/endpoints/quick_messages.md)
* [Templates](https://github.com/outstand/api-docs/blog/master/endpoints/templates.md)


## Pagination

You can paginate the result set by passing in the following parameters for the request:

```
/api/v1/contacts.json?page=1&per_page=50
```

When you request a page that does not exist you will receive a ```404 Not Found```.

*Note:* ```page``` defaults to 1 and ```per_page``` defaults to the maximum of 100.
