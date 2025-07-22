# Drush Commands and Useful Operations

## Common Drush Commands
- Import configuration:
  ```
drush cim
  ```
- Export configuration:
  ```
drush config-export --destination="<folder-path>"
  ```
- Set maintenance mode:
  ```
drush config:set system.maintenance message "Optional message" -y
drush state:set system.maintenance_mode 1 --input-format=integer
drush cr
# To turn off:
drush state:set system.maintenance_mode 0 --input-format=integer
drush cr
  ```
- Synchronize UUID:
  ```
drush config-set "system.site" uuid "<new-uuid>"
  ```
- Delete shortcut set:
  ```
drush entity:delete shortcut_set default
  ```
- Generate UUID:
  ```
lando drush php-eval 'print(\Drupal::service("uuid")->generate().PHP_EOL);'
  ```
- List custom blocks and UUIDs:
  ```
drush sqlq 'SELECT id,uuid FROM block_content'
  ```
- Generate sample content:
  ```
drush genc <number of nodes> <number of comments> --types=<content type>
# Example:
drush genc 3 0 --types=bank
  ```
- Import/export config to custom folder:
  ```
drush config-import --source="<folder-path>"
drush config-export --destination="<folder-path>"
  ```
- Dump database and files:
  ```
drush sql-dump > "/<COMPANY_DRIVE>/${PWD##*/}/$(date +"%Y-%m-%d")/${PWD##*/}-$(date +"%Y-%m-%d").sql"
  ```
- Import database:
  ```
drush sql-drop -y; drush sql-cli < path_to_sql.sql
  ```
- Clear cache:
  ```
drush cr
  ```
- Update database:
  ```
drush updb
  ```
- Update entities:
  ```
drush entup
  ```
- Set config sync directory:
  ```php
  $settings['config_sync_directory'] = '../config/sync';
  $config_directories['sync'] = '../config/sync';
  ```
- Migration commands:
  ```
lando drush ms gea_country_migration
lando drush mim gea_country_migration --limit=1
lando drush mr gea_country_migration
  ```
- Example:
```
drush site-install standard --db-url=mysql://root:<PASSWORD>@localhost/<SITE_FOLDER> --account-mail="<EMAIL>" --account-name=superadmin --account-pass=123456 --site-mail="<EMAIL>" --site-name="<SITE_NAME>"
```
