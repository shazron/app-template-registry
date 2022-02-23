# app-template-registry

Simple app template registry.

## Usage

1. Download the [metadata.json](https://raw.githubusercontent.com/shazron/app-template-registry/main/metadata.json)
2. Look at the `registry` property
3. Download the file pointed to by the `registry` property


## Schema of metadata.json

This is the metadata of the registry.

```jsonc
{
  "name" // String
  "registry" // String (http, https link to the initial registry json file)
}
```

## Schema of a registry json

This is just an array of RegistryRecords under the `data` key, with optional links to the previous and next pages.
Each payload will have a limit of 50 records.

```jsonc
{
  "data": [ 
      { ... }, // RegistryRecord
      { ... }, // RegistryRecord
      { ... }, // RegistryRecord
      { ... } // RegistryRecord
  ],
  "links": {
    "prev" // String, url to prev page
    "next" // String, url to next page
  }
}
```

## Schema of a RegistryRecord

This is similar to an npm package record.

Records are in the form (tentative schema):
```jsonc
{
  "name" // String (equivalent to the package name without scope)
  "scope" // String (equivalent to the scope of an npm package)
  "url" // String (http, https link to a git repo - for download/clone)
  "version" // String (semver) (equivalent to the package version)
  "description" // String
  "keywords", // Array of Strings (essentially 'tags')
  "date" // String ISO-8601 Date (record last updated date)
  "links" // Array of other links
  "author" // String (equivalent to the package author)
  "type" // String (this is an App Builder thing: the template type TBD)
}
```

# How to Generate the Registry Json

This can be accomplished by an App Builder app that has a front-end SPA that can gather input, then update the registry json via the Github API - there can also be a Runtime endpoint that serves the `metadata.json`. 

Think of the app template registry like a static website, it is re-generated each time without needing to be dynamic.

This can be similar to Azure Quickstart Templates: <https://azure.microsoft.com/en-us/resources/templates/>

1. Download the template package from its url 
2. Parse the `package.json` of the package
3. Map the `package.json` properties to a RegistryRecord
4. Add in additional properties to the RegistryRecord
5. Save the RegistryRecord to the registry json (paginated into multiple files, sorted descending by date)
