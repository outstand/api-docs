# Groups

* [Group Attributes](#group)

## Supported Actions

* [Get Groups](#get-groups)
* [Get Group](#get-group)
* [Create Group](#create-group)
* [Update Group](#update-group)
* [Delete Group](#delete-group)
* [Add Contacts to Group](#add-contacts-to-group)
* [Remove Contacts from Group](#remove-contacts-from-group)

## Group

**Required:** ```name```

```json
{
  "id": 1,
  "name": "Group A",
  "saved_message_id": "abcdefg",
  "campaign_template_id": 1,
  "profile_id": 1,
  "contacts_count": 1,
  "created_at": "2013-05-07T17:51:05Z",
  "updated_at": "2013-05-07T17:51:05Z",
  "contacts": "/groups/:id/contacts.json"
}
```

## Group Automation
When the `saved_message_id` and/or `campaign_template_id` are set, each time a contact is added to
the group they will automatically receive the specified Saved Message and/or Campaign. If the
`profile_id` is not specified, the automated messages will be sent with the user's default profile
that owns the group.

If the user that owns the group does not have access to the Saved Message, Campaign Template, or Profile
referenced, you will not be able to add it to the group; resulting in a 422 response. If the user
loses access to the Saved Message and/or Campaign Template that is bound to a group, the automation
for that group will result in a no-op.


## Get Groups

* ```GET /groups.json``` returns a paginated list of groups for account.
* ```GET /contacts/:contact_id/groups.json``` returns a paginated list of groups for specified contact for account.

Returns a `200 OK` with an array of groups. (See [Group](#group) for JSON representation.) If you request a page of groups that does not exist, a ```404 Not Found``` will be returned. (See [Pagination](https://github.com/outstand/api-docs#pagination))

### Optional Query Params

* `q` full-text search on `name`
* `page` & `per_page` see [Pagination](https://github.com/outstand/api-docs#pagination)

## Get Group

 * ```GET /groups/:id.json``` returns specified group. (See [Group](#group) for JSON representation.)

## Create Group

* ```POST /groups.json``` creates a new group from parameters

```json
{
  "name" : "Group A",
  "saved_message_id" : "abcdefg",
  "campaign_template_id" : 1,
  "profile_id" : 1
}
```

On success, this returns ```201 Created```, [JSON representation](#group) in response body, and ```Location``` header with the location of the new group. If the request is invalid, a ```422 Unprocessable Entity``` is returned with the error(s) in the response body. (See [422 Unprocessable Entity](https://github.com/outstand/api-docs/blob/master/422.md))

## Update Group

* ```PUT /groups/:id.json``` updates group from parameters

```json
{
  "name" : "Group A",
  "saved_message_id" : "abcdefg",
  "campaign_template_id" : 1,
  "profile_id" : 1
}
```

On success, this returns ```204 No Content```. If the request is invalid, a ```422 Unprocessable Entity``` is returned with the error(s) in the response body. (See [422 Unprocessable Entity](https://github.com/outstand/api-docs/blob/master/422.md))

## Delete Group

* ```DELETE /groups/:id.json``` will delete the specified group and return ```204 No Content``` on success. If the user does not have permission to delete the group, it returns ```404 Not Found```.

## Add Contacts to Group

* ```POST /groups/:id/contacts.json``` has two forms:

### Add Existing Contacts by ids

* ```POST /groups/:id/contacts.json``` adds the contacts specified by the `ids` param to the specified group.

```json
{
  "ids": [1, 2, 3]
}
```

On success, this returns ```204 No Content```. If the request is invalid, a ```422 Unprocessable Entity``` is returned with the error(s) in the response body. (See [422 Unprocessable Entity](https://github.com/outstand/api-docs/blob/master/422.md))

### Create New Contact inside Group

* ```POST /groups/:id/contacts.json``` adds the contacts specified by the `ids` param to the specified group.

Full documentation can be found here: [https://github.com/outstand/api-docs/blob/master/endpoints/contacts.md#create-contact](https://github.com/outstand/api-docs/blob/master/endpoints/contacts.md#create-contact)

## Remove Contacts from Group

* ```DELETE /groups/:id/contacts.json``` removes the contacts specified by the `ids` param from the specified group.

```json
{
  "ids": [1, 2, 3]
}
```

On success, this returns ```204 No Content```. If the request is invalid, a ```422 Unprocessable Entity``` is returned with the error(s) in the response body. (See [422 Unprocessable Entity](https://github.com/outstand/api-docs/blob/master/422.md))
