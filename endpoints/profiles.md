# Profiles

The profile contains the contact information as well as the branding information of the sender.

* [Profile Attributes](#profile)

## Supported Actions

* [Get Profiles](#get-profiles)

## Profile

```json
{
  "id": 8,
  "profile_name": "Default Profile",
  "full_name": "John Smith",
  "email": "john@example.com",
  "title": "Regional Manager",
  "photo": "https://...",
  "logo": "https://...",
  "color": "#a20a0a",
  "full_address": "6475 E Johns Xing, Johns Creek, GA, 30097, United States",
  "address_line_1": "6475 E Johns Xing",
  "address_line_2": "Suite B",
  "city": "Johns Creek",
  "state_region_province": "GA",
  "postal_code": "30097",
  "country":"United States",
}
```

## GET Profiles

* ```GET /profiles.json``` returns all profiles for the user

Returns a ```200 OK``` with an array of profiles. (See [Profile](#profile) for JSON representation.)
