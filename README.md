# app-template-registry

Simple app template registry.

Records are in the form (tentative schema):
```json
{
  "name" // String
  "scope" // String
  "url" // String (http, https link to a git repo)
  "version": // String (semver)
  "description" // String
  "keywords", // Array of Strings
  "date" // String ISO-8601 Date
  "links" // Array of other links
  "author" // String
}
```

The registry is a json file [registry.json](./registry.json) that contains all the records and can be downloaded via this link:
https://raw.githubusercontent.com/shazron/app-template-registry/main/registry.json


