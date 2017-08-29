# User Endpoints
The following endpoints are only available through OAuth2 Client Credentials Flow with an application with the `provision_users` scope.

_Note: This API is scoped to your organization’s white label._

**User Attributes:**

```javascript
{
  “username”: “user12345”,
  “email”: “joe.smith@example.com”,
  “auth_token”: “abc123”,
  “status”: “active”
}
```

Note: status can be of type: `active`, `dunning`, `disabled`, `suspended`, `canceled`, `incomplete`, `needs_plan`.

When provisioning a user that requires payment information, the user will be created with an initial status of `needs_plan`. When the user logs in for the first time, they will see a page where they will select their plan. Upon selecting a plan, the user will be set to `incomplete`. Once the user adds valid payment information, the user will transition to `active`. If payment information is not required, the user will transition from `needs_plan` to  `active` upon selecting a plan.

## Get Users
`GET /api/v1/users.json` - Returns all users available to the Third Party Service

Returns a 200 OK with an array of users. If you request a page of users that does not exist, a 400 Bad Request will be returned.

## Create User
`POST /api/v1/white_labels/<token>/users` - Creates a user account under your white label

Parameters:

```javascript
{
  “username”: “user12345”,
  “password”: “test123”,
  “time_zone”: “Eastern Time (US & Canada)”,
  “first_name”: “John”,
  “middle_initial”: “L”,
  “last_name”: “Smith”,
  “title”: “Advisor”,
  “address_line_1”: “1st Street”,
  “address_line_2”: “Suite B”,
  “city”: “Richmond”,
  “state_region_province”: “Va”,
  “postal_code”: “23451”,
  “phone_1”: “555-444-1234”,
  “phone_1_location”: “Mobile”,
  “phone_2”: “1-888-123-1234”,
  “phone_2_location”: “Toll-Free”,
  “phone_3”: “123-123-1234”,
  “phone_3_location”: “Work”,
  “email”: “joe.smith@example.com”,
  “website”: “http://www.example.com”,
  “twitter”: “http://twitter.com/username”,
  “linkedin”: “http://linkedin.com/profile”,
  “facebook”: “http://facebook.com”,
  “blog”: “http://blog.example.com”,
  “video_channel”: “http://youtube.com/channel”
}
```

* Required parameters: `username`, `password`, `first_name`, `last_name`, `email`
* Unique parameters: `username`, `email`

_Note: `time_zone` defaults to “Eastern Time (US & Canada)”_

On success, this returns 201 Created, the user attributes in the response body, and the location header of the new user. If the request is invalid a 422 Unprocessable Entity is returned with the error(s) in the response body.

* Possible locations for phone numbers: "Work", "Home", "Mobile", "Skype", "Toll-Free", "Fax", "Other"

## Get User
`GET /api/v1/users/:username.json` - Returns the user attributes of user with specified username.

Returns a 200 OK on success and 404 Not Found if user does not exist.
