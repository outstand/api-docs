# Application Endpoints

## Authentication

The following endpoints are only available through OAuth2 Client Credentials Flow with an application with the `provision_users` scope.

The endpoints described here are considered 'application level endpoints' which is why the oauth tokens you obtain through the client credentials flow aren't tied to a user.  These tokens _cannot_ be used to access 'user level endpoints' and regular user oauth tokens cannot be used to access these application level endpoints.


## User Endpoints

_Note: This API is scoped to your organization’s white label._

**User Attributes:**

```json
{
  "username": "user12345",
  "email": "joe.smith@example.com",
  "auth_token": "abc123",
  "status": "active"
}
```

Note: status can be of type: `active`, `dunning`, `disabled`, `suspended`, `canceled`, `incomplete`, `needs_plan`.

When provisioning a user that requires payment information, the user will be created with an initial status of `needs_plan`. When the user logs in for the first time, they will see a page where they will select their plan. Upon selecting a plan, the user will be set to `incomplete`. Once the user adds valid payment information, the user will transition to `active`. If payment information is not required, the user will transition from `needs_plan` to  `active` upon selecting a plan.

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

## Get User
`GET /api/v1/users/:username.json` - Returns the user attributes of user with specified username.

Returns a 200 OK on success and 404 Not Found if user does not exist.

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
