# Drush Commands and Useful Operations

## Configuration & Maintenance
- Import configuration:
  ```
  drush cim
  ```
- Export configuration:
  ```
  drush config-export --destination="<folder-path>"
  ```
- Import/export config to custom folder:
  ```
  drush config-import --source="<folder-path>"
  drush config-export --destination="<folder-path>"
  ```
- Set config sync directory:
  ```php
  $settings['config_sync_directory'] = '../config/sync';
  $config_directories['sync'] = '../config/sync';
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

## Site Setup & Install
- Example site install:
  ```
  drush site-install standard --db-url=mysql://root:<PASSWORD>@localhost/<SITE_FOLDER> --account-mail="<EMAIL>" --account-name=superadmin --account-pass=123456 --site-mail="<EMAIL>" --site-name="<SITE_NAME>"
  ```

## UUID & Entity Management
- Synchronize UUID:
  ```
  drush config-set "system.site" uuid "<new-uuid>"
  ```
- Generate UUID:
  ```
  ddev drush php-eval 'print(\Drupal::service("uuid")->generate().PHP_EOL);'
  ```
- Delete shortcut set:
  ```
  drush entity:delete shortcut_set default
  ```
- List custom blocks and UUIDs:
  ```
  drush sqlq 'SELECT id,uuid FROM block_content'
  ```

## Content & Data
- Generate sample content:
  ```
  drush genc <number of nodes> <number of comments> --types=<content type>
  # Example:
  drush genc 3 0 --types=bank
  ```

## Database & Files
- Dump database and files:
  ```
  drush sql-dump > "/<COMPANY_DRIVE>/${PWD##*/}/$(date +"%Y-%m-%d")/${PWD##*/}-$(date +"%Y-%m-%d").sql"
  ```
- Import database:
  ```
  drush sql-drop -y; drush sql-cli < path_to_sql.sql
  ```

## Cache, Updates, and Entities
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

## Migration
- Migration commands:
  ```
  ddev drush ms gea_country_migration
  ddev drush mim gea_country_migration --limit=1
  ddev drush mr gea_country_migration
  ```
