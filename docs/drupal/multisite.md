# Drupal Multisite Configuration

## Sample DDEV multisite configuration
Add the additional hostnames and database names in the ddev config yaml file
```YAML
name: <project-name>
type: drupal
docroot: web
php_version: "8.2"
webserver_type: nginx-fpm
xdebug_enabled: false
additional_hostnames:
  - <multisite1>
  - <multisite2>
  - <multisite3>
  - <multisite4>
  - <multisite5>
  - <multisite6>
  - <multisite7>
  - <multisite8>
  - <multisite9>
additional_fqdns: []
database:
  type: mariadb
  version: "10.11"
use_dns_when_possible: true
composer_version: "2"
web_environment: []
corepack_enable: true
hooks:
  post-start:
    - exec: |
        for db in multisite1 multisite2 multisite3 multisite4 multisite5 multisite6 multisite7 multisite8 multisite9; do
          mysql -uroot -proot -e "CREATE DATABASE IF NOT EXISTS $db;"
        done
```
- Check the URLs are live: After `ddev start` see the URLs are live `ddev describe`
- Goto sites.php and add the folder links the right hand side will be the folder names
  ```php
  $sites['multisite1.ddev.site'] = 'multisite1';
  $sites['multisite2.ddev.site'] = 'multisite2';
  $sites['multisite3.ddev.site'] = 'multisite3';
  $sites['multisite4.ddev.site'] = 'multisite4';
  $sites['multisite5.ddev.site'] = 'multisite5';
  $sites['multisite6.ddev.site'] = 'multisite6';
  $sites['multisite7.ddev.site'] = 'multisite7';
  $sites['multisite8.ddev.site'] = 'multisite8';
  $sites['multisite9.ddev.site'] = 'multisite9';
  ```
- Goto settings.php of each multisite folder and add
  ```PHP
  $host = "db";
  $port = 3306;
  $driver = "mysql";

  $databases['default']['default']['database'] = "multisite1";
  $databases['default']['default']['username'] = "root";
  $databases['default']['default']['password'] = "root";
  $databases['default']['default']['host'] = $host;
  $databases['default']['default']['port'] = $port;
  $databases['default']['default']['driver'] = $driver;
  ```
## Multisite Config Export
- Get multisite URI:
  ```sh
  drush debug:multisite
  ```
- Set config path in `settings.php`:
  ```php
  $config_directories['sync'] = '../config/sync/<multisite-foldername>';
  ```
- Export config for a particular site:
  Config files are in `sites/<multisite-foldername>/files/config`.
  ```
  drush --uri=<SITE>.localhost config:export
  ```

## Clear Cache for Multisite
```
drush cr --uri=<multisite-foldername>
```

## Other Useful Commands
- Export config for a specific URI:
  ```
  drush --uri=<multisite-foldername> config:export
  ```
- Clear cache for a specific URI:
  ```
  drush cr all --uri=<SITE>.localhost
  ```
