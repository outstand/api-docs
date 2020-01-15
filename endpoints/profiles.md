# Profiles

The profile contains the contact information as well as the branding information of the sender.

* [Profile Attributes](#profile)

## Supported Actions

* [Get Profiles](#get-profiles)
* [Get Profile](#get-profile)
* [Create Profile](#create-profile)
* [Update Profile](#update-profile)
* [Delete Profile](#delete-profile)

## Profile

*Note:* ```first_name``` , ```last_name```, and ```email``` are required.

```json
{
  "id": 1,
  "profile_name": "Default Profile",
  "photo": "https://d21y27je7ptf17.cloudfront.net/image/upload/c_thumb,dpr_2.0,g_faces,h_120,w_120,z_0.7/rplxklponamcoy3ao99c.png",
  "email": "john@example.com",
  "first_name": "John",
  "last_name": "Smith",
  "middle_initial": "J",
  "full_name": "John J Smith",
  "title": "Regional Manager",
  "company_name": "ABC Supply",
  "address_line_1": "6475 East Johns Xing",
  "address_line_2": "Apt. 202",
  "city": "Johns Creek",
  "state_region_province": "GA",
  "postal_code": "30097",
  "country": "United States",
  "country_code": "US",
  "phone_1": "123-123-1234",
  "phone_1_location": "Mobile",
  "phone_2": "223-223-2234",
  "phone_2_location": "Work",
  "phone_3": "323-323-3234",
  "phone_3_location": "Other",
  "website": "https://john-smith.com",
  "twitter": "https://twitter.com/example_user",
  "linkedin": "https://linkedin.com/example_user",
  "facebook": "https://facebook.com/example_user",
  "blog": "https://blog.example.com",
  "video_channel": "https://youtube.com/example_user",
  "salutation": "Dear,",
  "valediction": "Best wishes,",
  "legal_footer": "Legal footer text",
  "logo": "https://d2qnc9lf0j59c3.cloudfront.net/accounts/63220/brand_identities/101570/size_320x140/new_logo.jpg?1550612260",
  "color": "#4B7B47",
  "default": true
}
```

## GET Profiles

* ```GET /profiles.json``` returns all profiles for the user

Returns a ```200 OK``` with an array of profiles. (See [Profile](#profile) for JSON representation.)

## Get Profile

* ```GET /profiles/:id.json``` returns specified profile (See [Profile](#profile) for JSON representation)

Returns a ```200 OK``` on success and ```404 Not Found``` if profile does not exist.

## Create Profile

* ```POST /profiles.json``` creates a new profile from parameters

```json
  "profile_name": "New Profile Name",
  "photo": "file upload object",
  "email": "john@example.com",
  "first_name": "John",
  "last_name": "Smith",
  "middle_initial": "J",
  "title": "Regional Manager",
  "company_name": "ABC Supply",
  "address_line_1": "6475 East Johns Xing",
  "address_line_2": "Apt. 202",
  "city": "Johns Creek",
  "state_region_province": "GA",
  "postal_code": "30097",
  "country": "United States",
  "country_code": "US",
  "phone_1": "123-123-1234",
  "phone_1_location": "Mobile",
  "phone_2": "223-223-2234",
  "phone_2_location": "Work",
  "phone_3": "323-323-3234",
  "phone_3_location": "Other",
  "website": "https://john-smith.com",
  "twitter": "https://twitter.com/example_user",
  "linkedin": "https://linkedin.com/example_user",
  "facebook": "https://facebook.com/example_user",
  "blog": "https://blog.example.com",
  "video_channel": "https://youtube.com/example_user",
  "salutation": "Dear,",
  "valediction": "Best wishes,",
  "legal_footer": "Legal footer text",
  "logo": "file upload object",
  "color": "#4B7B47"
}
```

### Optional Params
Alternatively you can supply ```remote_photo_url``` instead of photo.
```json
{
  "remote_photo_url": "https://files.amazonaws.com/photos/photo.jpg"
}
```

On success, this returns ```201 Created```, [JSON representation](#profile) in response body. If the request is invalid, a ```422 Unprocessable Entity``` is returned with the error(s) in the response body. (See [422 Unprocessable Entity](https://github.com/outstand/api-docs/blob/master/422.md))

## Update Profile

* ```PUT /profiles/:id.json``` updates profile from parameters

```json
  "id": 67324
  "profile_name": "Updated Profile Name",
  "photo": "file upload object",
  "email": "john@example.com",
  "first_name": "John",
  "last_name": "Smith",
  "middle_initial": "J",
  "title": "Regional Manager",
  "company_name": "ABC Supply",
  "address_line_1": "6475 East Johns Xing",
  "address_line_2": "Apt. 202",
  "city": "Johns Creek",
  "state_region_province": "GA",
  "postal_code": "30097",
  "country": "United States",
  "country_code": "US",
  "phone_1": "123-123-1234",
  "phone_1_location": "Mobile",
  "phone_2": "223-223-2234",
  "phone_2_location": "Work",
  "phone_3": "323-323-3234",
  "phone_3_location": "Other",
  "website": "https://john-smith.com",
  "twitter": "https://twitter.com/example_user",
  "linkedin": "https://linkedin.com/example_user",
  "facebook": "https://facebook.com/example_user",
  "blog": "https://blog.example.com",
  "video_channel": "https://youtube.com/example_user",
  "salutation": "Dear,",
  "valediction": "Best wishes,",
  "legal_footer": "Legal footer text",
  "logo": "file upload object",
  "color": "#4B7B47"
}
```

### Optional Params
You can supply ```delete_photo``` to remove the photo from the profile.
```json
{
  "delete_photo": 1
}
```
Alternatively you can supply ```remote_photo_url``` to update the photo instead of photo.
```json
{
  "remote_photo_url": "https://files.amazonaws.com/photos/photo.jpg"
}
```

## Delete Profile

* ```DELETE /profiles/:id.json``` will delete the specified profile and return ```204 No Content``` on success. If the user does not have permission to delete the profile, it returns ```404 Not Found```. If the request is invalid, a ```422 Unprocessable Entity``` is returned with the error(s) in the response body. (See [422 Unprocessable Entity](https://github.com/outstand/api-docs/blob/master/422.md))
