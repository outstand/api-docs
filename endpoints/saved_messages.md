# Saved Messages

* [Saved Message Attributes](#saved-message)

## Supported Actions

* [Get Saved Messages](#get-saved-messages)
* [Get Saved Message](#get-saved-message)

## Saved Message

```json
{
  "id": "563bbc7c79e68b3351000070",
  "name": "Happy Father's Day",
  "subject": "Happy Father's Day to the....",
  "template_slug": "email-greeting",
  "categories": [
    "Father's Day"
  ],
  "share_code": "21fd6657ef110979",
  "price": null,
  "main_graphic_url": "https://...",
  "areas": {},
  "attachments": [],
  "created_at": "2014-06-05T20:38:55Z",
  "updated_at": "2014-06-05T20:38:55Z",
  "template_thumbnail_url": "https://..."
}
```

## Get Saved Messages

* `GET /saved_messages.json` returns a paginated list of saved messages for the user

Returns a `200 OK` with an array of contacts. (See [Saved Message](#saved-message) for JSON representation.) If you request a page of saved messages that does not exist, a `404 Not Found` will be returned. (See [Pagination](https://github.com/outstand/api-docs#pagination))

### Optional Query Params

* `template` supports the slug of the template: `branded-email`, `email-greeting`, `newsletter-single-column`, `newsletter-two-column`, `greeting-card`, `mini-greeting-card`, `postcard`, `mini-postcard` (`email-greeting` is default.)
* `q` search query
* `category`
* `filter_by` supports one of the following: `all`, `mine`, `buy`. (`all` is default.) `mine` filters saved messages to only saved messages that the user created, belong to the user's white label group, or the user has purchased.
* `sort_by` supports one of the following: `created_at`, `name` (`created_at` is default.)
* `direction` supports one of the following: `desc`, `asc` (`desc` is default.)

## Get Saved Message

* `GET /saved_messages/:id.json` returns specified saved message. (See [Saved Message](#saved-message) for JSON representation.)
