# Channels

* [Channel Attributes](#channel)

## Supported Actions

* [Get Channels](#get-channels)
* [Get Channel](#get-channel)
* [Subscribing to a Channel](#subscribing-to-a-channel)
* [Unsubscribing to a Channel](#unsubscribing-to-a-channel)

## Channel

```json
{
  "id": 1,
  "name": "Channel 1",
  "slug": "channel-1",
  "description": "Short description of channel.",
  "subscribed_at": null | "2018-06-22T12:00:00Z",
  "created_at": "2018-06-22T12:00:00Z",
  "updated_at": "2018-06-22T12:00:00Z"
}
```

*Note:* If the user is not subscribed to the channel, the `subscribed_at` attribute will be `null`. If the user is subscribed to the channel, the `subscribed_at` will be a timestamp of when the user subscribed to that channel.

## Get Channels

* ```GET /channels``` returns a paginated list of channels available to the account.

Returns a `200 OK` with an array of channels. (See [Channel](#channel) for JSON representation.) If you request a page of channels that does not exist, a `404 Not Found` will be returned. (See [Pagination](https://github.com/outstand/api-docs#pagination))

### Optional Query Params

* `page` & `per_page` see [Pagination](https://github.com/outstand/api-docs#pagination)

## Get Channel

* ```GET /channels/:channel-slug``` returns the specified channel based on the channel's slug

Returns a `200 OK` with the channel. (See [Channel](#channel) for JSON representation.) If you request a channel that does not exist or user does not have access to specified channel, a `404 Not Found` will be returned.

## Subscribing to a Channel

* ```POST /channels/:channel-slug/subscription```

Returns a `201 Created`. If the specified channel does not exist or user does not have access to specified channel, a `404 Not Found` will be returned.

## Unsubscribing to a Channel

* ```DELETE /channels/:channel-slug/subscription```

Returns a `204 No Content`. If the user is not subscribed to the channel, a `404 Not Found` will be returned.