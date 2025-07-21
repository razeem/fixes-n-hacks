# Composer: Add Custom Libraries in web Folder

## Add to composer.json

Add to the `repositories` array:
```json
{
  "type": "package",
  "package": {
    "name": "desandro/masonry",
    "version": "3.3.1",
    "type": "drupal-library",
    "dist": {
      "url": "https://github.com/desandro/masonry/archive/v3.3.1.zip",
      "type": "zip"
    }
  }
}
```

Add a custom installation path in the `extra` object:
```json
"extra": {
  "installer-paths": {
    "web/core": ["type:drupal-core"],
    "web/libraries/{$name}": ["type:drupal-library"]
  }
}
```

Install the library:
```
composer require desandro/masonry
```

### Example 2
```json
"repositories": [
  {
    "type": "composer",
    "url": "https://packages.drupal.org/8"
  },
  {
    "type": "package",
    "package": {
      "name": "enyo/dropzone",
      "version": "5.7.1",
      "type": "drupal-library",
      "dist": {
        "url": "https://github.com/enyo/dropzone/archive/v5.7.1.zip",
        "type": "zip"
      }
    }
  }
]
```
Then run:
```
composer require drupal/dropzonejs enyo/dropzone
```
