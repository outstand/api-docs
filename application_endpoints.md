# Application Endpoints

## Authentication

The following endpoints are only available through OAuth2 Client Credentials Flow with an application with the `provision_users` scope.

The endpoints described here are considered 'application level endpoints' which is why the oauth tokens you obtain through the client credentials flow aren't tied to a user.  These tokens _cannot_ be used to access 'user level endpoints' and regular user oauth tokens cannot be used to access these application level endpoints.

### OAuth 2 Authentication

1. [Grab an OAuth 2 library](http://oauth.net/code/)
2. Contact support to register your application. You will then be assigned a `client_id` and `client_secret`.
3. Configure your OAuth 2 library with:
  * `client_id`, `client_secret`
  * `grant_type` should be `client_credentials`
  * `https://app.outstand.com/oauth/token` to get access tokens
4. Try making an authorized request to `https://app.outstand.com/oauth/token/info`

## User Endpoints

_Note: This API is scoped to your organization’s white label._

**User Attributes:**

```json
{
  "username": "user12345",
  "oauth2_token": {
    "access_token": "<access token>",
    "token_type": "Bearer",
    "expires_in": 7200,
    "refresh_token": "<refresh token>",
    "scope": "identity read write",
    "created_at": <created at time in seconds>
  },
  "authentication_token": "<legacy auth token>",
  "email": "joe.smith@example.com",
  "status": "active"
}
```

Note: status can be of type: `active`, `dunning`, `disabled`, `suspended`, `canceled`, `incomplete`, `needs_plan`.

When provisioning a user that requires payment information, the user will be created with an initial status of `needs_plan`. When the user logs in for the first time, they will see a page where they will select their plan. Upon selecting a plan, the user will be set to `incomplete`. Once the user adds valid payment information, the user will transition to `active`. If payment information is not required, the user will transition from `needs_plan` to  `active` upon selecting a plan.

The `oauth2_token` part of the response matches the format of our normal token endpoint.  Note that requests for the user's token information will return the last valid token and refresh token.  If your access token is expired, you should use the refresh token to obtain a new one.

## Get Users
`GET /api/v1/users.json` - Returns all users available to the Third Party Service

Returns a 200 OK with a [paginated](https://github.com/outstand/api-docs#pagination) array of users. If you request a page of users that does not exist, a 400 Bad Request will be returned.

## Create User
`POST /api/v1/white_labels/<token>/users` - Creates a user account under your white label

Parameters:

```json
{
  "username": "user12345",
  "password": "test123",
  "time_zone": "Eastern Time (US & Canada)",
  "first_name": "John",
  "middle_initial": "L",
  "last_name": "Smith",
  "title": "Advisor",
  "address_line_1": "1st Street",
  "address_line_2": "Suite B",
  "city": "Richmond",
  "state_region_province": "Va",
  "postal_code": "23451",
  "phone_1": "555-444-1234",
  "phone_1_location": "Mobile",
  "phone_2": "1-888-123-1234",
  "phone_2_location": "Toll-Free",
  "phone_3": "123-123-1234",
  "phone_3_location": "Work",
  "email": "joe.smith@example.com",
  "website": "http://www.example.com",
  "twitter": "http://twitter.com/username",
  "linkedin": "http://linkedin.com/profile",
  "facebook": "http://facebook.com",
  "blog": "http://blog.example.com",
  "video_channel": "http://youtube.com/channel"
}
```

* Required parameters: `username`, `password`, `first_name`, `last_name`, `email`
* Unique parameters: `username`, `email`

_Note: `time_zone` defaults to "Eastern Time (US & Canada)"_

On success, this returns 201 Created, the user attributes in the response body, and the location header of the new user. If the request is invalid a 422 Unprocessable Entity is returned with the error(s) in the response body.

* Possible locations for phone numbers: "Work", "Home", "Mobile", "Skype", "Toll-Free", "Fax", "Other"

_See the User Attributes section above for information on the response body._

## Get User
`GET /api/v1/users/:username.json` - Returns the user attributes of user with specified username.

Returns a 200 OK on success and 404 Not Found if user does not exist.

## Update User
`PATCH /api/v1/users/:username.json` - Updates the user attributes

Parameters:
```json
{
  "status": "disabled" | "active"
}
```

_Note: At this time, this endpoint can only be used to disable & activate accounts._

Returns 204 No Content on success. If an invalid status is requested, a 400 Bad Request will be returned. If the user cannot be updated for another reason a 422 Unprocessable Entity is returned with the error(s) in the response body.

## Delete User
`DELETE /api/v1/users/:username.json` - Terminates the given user's account. The user's account will be maintained in a deleted state for up to 30 days.

Returns a 204 No Content on success and a 404 Not Found if the user does not exist.

## Webhooks

We provide webhook events for integrators.  Contact us with your target URL for setup.

Webhooks are asynchronous events and as such may arrive after a delay.  Also keep in mind that webhooks may arrive out of order.
When you receive a webhook, you should reply with a `200 OK` response as quickly as possible.  Any other response or a failure to respond within 15 seconds will result in a failed delivery and automatic retries.  Outstand will attempt to send each webhook up to 5 times before permanently failing the webhook delivery.  The retries will follow a backoff schedule:

Attempt | Timing
--------|-------
1 | As soon as possible after the trigger
2 | 10 seconds after the most recent failure
3 | 15 seconds after the most recent failure
4 | 90 seconds after the most recent failure
5 | 180 seconds after the most recent failure

Webhooks are signed with a signature which is the HMAC hexdigest of the webhook body and the shared secret that we supply.  The digest used is indicated by the beginning of the signature.  You may validate a webhook with something similar to the following ruby code:
```ruby
def valid_signature?(headers, body)
  digest = headers['X-Outstand-Signature'].split('=').first
  raise 'Invalid digest' unless ['sha256', 'sha512'].include? digest
  signature = "#{digest}=" + OpenSSL::HMAC.hexdigest(OpenSSL::Digest.new(digest), ENV['SECRET_TOKEN'], body)
  Rack::Utils.secure_compare(signature, headers['X-Outstand-Signature'])
end
```
_Note: Be sure to use a constant time comparison method like `secure_compare`_

### Events

Name | Description
-----|------------
user_status | Triggered when a user's status changes.
create_contact | Triggered on contact create
update_contact | Triggered on contact update
delete_contact | Triggered on contact delete

### Payloads

Each event type has a specific payload that is included in the webhook body.

#### Headers

Header | Description
-------|------------
`X-Outstand-Event` | Name of the event that triggered this webhook
`X-Outstand-Id` | Unique ID for this webhook event
`X-Outstand-Signature` | HMAC hexdigest of the body with the secret key

#### Example
```
POST /payload HTTP/1.1

Host: yourserver.com
User-Agent: Outstand-Webhook
Content-Type: application/json
Content-Length: <length>
X-Outstand-Event: user_status
X-Outstand-Id: 123
X-Outstand-Signature: sha256=<signature>

{
  "username": "user12345",
  "status": "active"
}
```

### Detailed Events

#### `user_status`

Triggered when a user's status changes.

Payload:

Key | Type | Description
----|------|------------
`username` | `string` | The unique username of the user.
`status` | `string` | The user's status.

#### Resource Events (Contact, etc)

Payload:

Key | Type | Description
----|------|------------
`resource_type` | `string` | "Contact", etc
`resource_id` | `string` | The id of the resource that caused the event.
`event` | `string` | The short form of the resource event.
`username` | `string` | The unique username of the user. **Will be deprecated.**
`user_id` | `string` | The unique id of the user. **Will be deprecated.**
`account_id` | `string` | The unique id of the account.

An example contact creation:

```
POST /payload HTTP/1.1

Host: yourserver.com
User-Agent: Outstand-Webhook
Content-Type: application/json
Content-Length: <length>
X-Outstand-Event: create_contact
X-Outstand-Id: 123
X-Outstand-Signature: sha256=<signature>

{
  "resource_type": "Contact",
  "resource_id": "21",
  "event": "create",
  "username": "user12345",
  "user_id": "4862",
  "account_id": "7829"
}
```
