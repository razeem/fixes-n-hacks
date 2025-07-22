# Miscellaneous Drupal Tips and Fixes

## 1. Configuration & Environment

### Trusted Host Settings
Add to `settings.php`:
```php
$settings['trusted_host_patterns'] = array(
  '^example\.com$',
  '^www\.example\.com$',
  '^localhost$',
);
```

### Changing the Sync Directory
Add to `settings.local.php` or `settings.php`:
```php
$config_directories['sync'] = '{path to the desired folder}/';
```

### CORS Configuration
- Copy `default.services.yml` to `services.yml` and set `cors.config` as needed.
```yaml
cors.config:
  enabled: true
  allowedHeaders: ['x-csrf-token','authorization','content-type','accept','origin','x-requested-with', 'access-control-allow-origin','x-allowed-header','*']
  allowedMethods: ['*']
  allowedOrigins: ['https://<DOMAIN>','*']
  exposedHeaders: false
  maxAge: false
  supportsCredentials: true
```

### Temp Folder Issues
- Set the temp folder path to the server's temp location (e.g. `/var/sentora/temp`).

### TCPDF Cache Directory
- Create `tcpdf/cachecahe` in the temp folder if needed.

### PHP OPcode Caching
- Install opcache and add to `php.ini`:
```ini
[opcache]
zend_extension=php_opcache.dll
opcache.enable=1
```

## 2. File & Directory Issues

### Site Broken When Aggregation is On
- Ensure `sites/default/files` and temp directory have full write permission.
- If still broken, deactivate all lines in `.htaccess` in `sites/default/files`, clear cache, then reactivate lines.

### Import/Export Database and Files
- Dump database:
```sh
drush sql-dump > "/<COMPANY_DRIVE>/${PWD##*/}/$(date +"%Y-%m-%d")/${PWD##*/}-$(date +"%Y-%m-%d").sql"
```
- Zip files:
```sh
zip -r /<COMPANY_DRIVE>/${PWD##*/}/$(date +"%Y-%m-%d")/${PWD##*/}-$(date +"%Y-%m-%d").zip web/sites/default/files/
```
- Import database and files:
```sh
drush sql-drop -y; drush sql-cli < path_to_sql.sql
sudo mv docroot/sites/default/files docroot/sites/default/files1
unzip files.zip
sudo rm -rf docroot/sites/default/files1
git clean -f
```

## 3. User & Access Issues

### Super User Edit Issue
- If unable to edit super user, check the timezone in `user_field_data` table for user id 1.

### Forgot Admin Username/Password
- Get user info:
```sh
drush uinf uid
# Example: drush uinf 1
```
- Reset password:
```sh
drush upwd username --password=newpassword
# Example: drush upwd admin --password=abc123
```

## 4. Module & Entity Issues

### Mismatched Entity/Field Definitions
- Run:
```sh
drush entup
```

### Missing Module from File System
- Run:
```sh
drush sql-query "DELETE FROM key_value WHERE collection='system.schema' AND name='module_name';"
```

### List Custom Blocks and Their UUIDs
```sh
drush sqlq 'SELECT id,uuid FROM block_content'
```

## 5. Caching & Performance

### PHP OPcode Caching
- See above in Configuration & Environment.

### Update Notifications
- Enable Update Manager module in backend.

## 6. Database & Content Management

### Generate Sample Content for Testing
```sh
drush genc <number of nodes> <number of comments> --types=<content type>
# Example: drush genc 3 0 --types=bank
```

### Import and Export Configuration to a Custom Folder
```sh
drush config-import --source="<folder-path>"
drush config-export --destination="<folder-path>"
```

### Configuration Directory Type 'sync' Does Not Exist
Add one of these to your settings file:
```php
$settings['config_sync_directory'] = '../config/sync';
$config_directories['sync'] = '../config/sync';
```

### Sync UUID When Drush is Not Configured
- Go to the database config table, search for `system.site`, download the data blob, edit the uuid, and replace it with the uuid from the main site.



## 7. PHPCS and PHPMD
- Install PHPCS:
```sh
composer global require drupal/coder
phpcs modules/custom > phpcs-modules.txt
phpcs modules/custom > phpcs-modules.txt -d memory_limit=512M
```
- Install PHPMD:
```sh
composer global require phpmd/phpmd
phpmd modules/custom html cleancode --reportfile phpmd.html
```

## 8. Miscellaneous

- For more Drush and Drupal Console commands, see the official documentation.
