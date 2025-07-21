# Miscellaneous Drupal 8 Tips

## Trusted Host Settings
Add to `settings.php`:
```php
$settings['trusted_host_patterns'] = array(
  '^example\.com$',
  '^www\.example\.com$',
  '^localhost$',
);
```

## Temp Folder Issues
- Set the temp folder path to the server's temp location (e.g. `/var/sentora/temp`).

## TCPDF Cache Directory
- Create `tcpdf/cachecahe` in the temp folder if needed.

## PHP OPcode Caching
- Install opcache and add to `php.ini`:
  ```
  [opcache]
  zend_extension=php_opcache.dll
  opcache.enable=1
  ```

## Update Notifications
- Enable Update Manager module in backend.

## Super User Edit Issue
- If unable to edit super user, check the timezone in `user_field_data` table for user id 1.

## Mismatched Entity/Field Definitions
- Run:
  ```
drush entup
  ```

## Forgot Admin Username/Password
- Get user info:
  ```
drush uinf uid
# Example:
drush uinf 1
  ```
- Reset password:
  ```
drush upwd username --password=newpassword
# Example:
drush upwd admin --password=abc123
  ```

## Missing Module from File System
- Run:
  ```
drush sql-query "DELETE FROM key_value WHERE collection='system.schema' AND name='module_name';"
  ```

## Change Sync Directory
- Add to `settings.local.php` or `settings.php`:
  ```php
  $config_directories['sync'] = '{path to the desired folder}/';
  ```

## Sync UUID Without Drush
- Edit the `system.site` record in the database config table and update the UUID.

## PHPCS and PHPMD
- Install PHPCS:
  ```
  composer global require drupal/coder
  phpcs modules/custom > phpcs-modules.txt
  phpcs modules/custom > phpcs-modules.txt -d memory_limit=512M
  ```
- Install PHPMD:
  ```
  composer global require phpmd/phpmd
  phpmd modules/custom html cleancode --reportfile phpmd.html
  ```

## Site Broken When Aggregation is On
- Ensure `sites/default/files` and temp directory have full write permission.
- If still broken, deactivate all lines in `.htaccess` in `sites/default/files`, clear cache, then reactivate lines.

## CORS Configuration
- Copy `default.services.yml` to `services.yml` and set `cors.config` as needed.

## More Drush/Console Commands
- See official documentation for more commands.
