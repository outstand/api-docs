# Templates

* [Template Attributes](#template)

## Supported Actions

* [Get Templates](#get-templates)

## Template

```json
{
  "name": "Email Greeting",
  "slug": "email-greeting",
  "format": "electronic"
}
```

## Get Templates

* `GET /templates.json` returns all available templates for the account

Returns a `200 OK` with an array of templates. (See [Template](#template) for JSON representation.)
