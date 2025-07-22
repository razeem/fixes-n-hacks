# Local setup
## Instructions using DDEV

1. Install DDEV
Ensure DDEV is installed on your system. Follow the installation guide for your OS on the DDEV official site.

2. Set Up Your Project Directory
`mkdir drupal11 && cd drupal11`

3. Configure DDEV
Run the DDEV configuration command specifying Drupal and PHP 8.3:
    ```BASH
    ddev config --project-type=drupal --php-version=8.3 --docroot=web
    ```

4. Start DDEV Services
`ddev start`

5. Install Drupal Using Composer
Download the Drupal 11 recommended project:
`ddev composer create drupal/recommended-project:^11`
    **Or for a specific version:**
    ```
    composer create-project drupal/core-recommended:11.x-dev d11_test_project --stability dev --no-interaction
    ```
6. Install Drush (Drupal Shell)
Drush is essential for efficient Drupal management:
`ddev composer require drush/drush`

7. Install and Configure Drupal
Use Drush to install Drupal:
`ddev drush site:install --account-name=admin --account-pass=admin -y`

8. Launch Your Site
Open your site in the browser:
`ddev launch`
Alternatively, auto-login:
`ddev launch $(ddev drush uli)`

## Common Issues

### While Cloning a Live Project
We might encounter issue while config import after installing the site
#### Site UUID mismatch
- Edit the `system.site` record in the database config table and update the UUID.
- `ddev drush cset system.site uuid "$(cat config/sync/system.site.yml | grep uuid | awk '{print $2}')"`
#### Shortcut set mismatch issue
- `ddev drush entity:delete shortcut_set`
### Error in loading site
If error, check `settings.php` Set config path in `settings.php`:
```php
$settings['config_sync_directory'] = '../config/sync';
```

### Import Configuration
```
drush cim
```

## Debugging Configuration

## Setting up Development Environment
- (Optional) Change ownership:
  ```
  sudo chown -R <user-name>:<group-name> *
  ```
- (Optional) Edit permissions for `settings.php`:
  ```
  sudo chmod 755 web/sites/default/settings.php
  ```
- Edit `settings.php` to include:
  ```php
  if (file_exists(__DIR__ . '/settings.local.php')) {
    include __DIR__ . '/settings.local.php';
  }
  ```
- Copy example local settings:
  ```
  cp sites/example.settings.local.php sites/default/settings.local.php
  sudo chmod 755 web/sites/default/settings.local.php
  ```

## Development settings

### Enable Development mode
Add or uncomment these in `settings.php` or `settings.local.php`
  ```php
  $settings['container_yamls'][] = DRUPAL_ROOT . '/sites/development.services.yml';

  $config['system.performance']['css']['preprocess'] = FALSE;
  $config['system.performance']['js']['preprocess'] = FALSE;

  $settings['cache']['bins']['render'] = 'cache.backend.null';
  $settings['cache']['bins']['dynamic_page_cache'] = 'cache.backend.null';
  $settings['cache']['bins']['page'] = 'cache.backend.null';
  ```

### Enable Twig Debugging
- Create `sites/development.services.yml`:
  ```yaml
  parameters:
    http.response.debug_cacheability_headers: true
    twig.config:
      debug: true
      auto_reload: true
      cache: false  
  services:
    cache.backend.null:
      class: Drupal\Core\Cache\NullBackendFactory
  ```
#### Via drush:
  ```
  drush variable-set theme_debug 1
  ```
