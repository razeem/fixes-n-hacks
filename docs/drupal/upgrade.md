# Drupal 8 Core Upgrade

## Update Core and Modules
- Fetch all new updated files:
  ```
  composer update
  composer outdated
  composer show -lo
  composer update drupal/modulename --with-dependencies
  ```
- Update database:
  ```
  drush updb
  ```
- Update entities:
  ```
  drush entup
  ```
- Clear caches:
  ```
  drush cr
  ```

## Troubleshooting
- If updates are still available, check `composer.json` and update module versions (e.g. change `"drupal/devel": "1.0-rc2"` to `"drupal/devel": "^1.0"`).
- Run `composer update` again.

### Common Issues
- **Frontend Issues:** jQuery 3 upgrade may break some functions and themes.
- **PHP Version:** Higher PHP version may be required.
- **MySQL Errors (e.g. missing column revision-default):**
  ```
  drush sql-query "ALTER TABLE block_content_revision ADD COLUMN revision_default tinyint(5) AFTER revision_log"
  ```
- **Config errors:**
  ```
drush sql-query "DELETE FROM config WHERE name = 'system.action.comment_delete_action';DELETE FROM config WHERE name = 'views.view.comment';TRUNCATE TABLE cache_config;"
  ```
- **Fields deletion pending error:**
  ```
drush php:eval 'field_purge_batch(50000);'
  ```

## After Upgrade
- Login and check `/admin/reports/updates` for module updates.
- If further updates are needed, adjust `composer.json` as above and repeat the process.
