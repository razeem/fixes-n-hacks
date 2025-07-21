# Drupal 8 Multisite Configuration

## Install Multisite in Existing Project
```
drush site-install --db-url=mysql://root:spots@localhost/bac009_portal --sites-subdir=portal --yes --account-mail="alameen@4spots.com" --account-name=superadmin --account-pass=123456 --site-mail="tech@4spots.com" --site-name="bac portal"
```

## Multisite Config Export
- Get multisite URI:
  ```
  drupal debug:multisite
  ```
- Set config path in `settings.php`:
  ```php
  $config_directories['sync'] = '../config/sync/portal';
  ```
- Export config for a particular site:
  ```
drupal --uri=portal.localhost config:export
  ```
  Config files are in `sites/multisite_folder/files/config`.

## Clear Cache for Multisite
```
drupal cr all --uri=portal.localhost
```

## Other Useful Commands
- Set config path:
  ```php
  $config_directories['sync'] = '../config/sync/portal';
  ```
- Export config for a specific URI:
  ```
drupal --uri=portal.localhost config:export
  ```
- Clear cache for a specific URI:
  ```
drupal cr all --uri=portal.localhost
  ```
