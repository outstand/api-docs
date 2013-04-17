# Groups

## Supported Actions

* [Group Attributes](#group)
* [Get Groups](#get-groups)
* [Get Group](#get-group)
* [Create Group](#create-group)
* [Update Group](#update-group)
* [Delete Group](#delete-group)

## Group

**Required:** ```name```

```json
{
  "id": 1,
  "name": "Group A",
  "contacts_count": 1,
  "created_at": 1366133271,
  "updated_at": 1366133271,
  "contacts": "/groups/:id/contacts.json"
}
```

## Get Groups

* ```GET /groups.json``` returns all groups for account.
* ```GET /contacts/:contact_id/groups.json``` returns all groups for specified contact.

Returns an array of groups. (See [Group](#group) for JSON representation.)

## Get Group

 * ```GET /groups/:id.json``` returns specified group. (See [Group](#group) for JSON representation.)

## Create Group

* ```POST /groups.json``` creates a new group from parameters

```json
{
  "name" : "Group A"
}
```

On success, this returns ```201 Created```, [JSON representation](#group) in response body, and ```Location``` header with the location of the new group.

## Update Group

* ```PUT /groups/:id.json``` updates group from parameters

```json
{
  "name" : "Group A"
}
```

On success, this returns ```200 OK``` and [JSON representation](#group) in response body.

## Delete Group

* ```DELETE /groups/:id.json``` will delete the specified group and return ```204 No Content``` on success. If the user does not have permission to delete the group, it returns ```403 Forbidden```.
