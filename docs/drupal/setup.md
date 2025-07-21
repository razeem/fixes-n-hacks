# Drupal 8 Setup

## Create a D7 Project using Composer
```
composer create-project drupal-composer/drupal-project:7.x-dev drupal7 --stability dev --no-interaction
```

## Create a D8 Project using Composer

Navigate to your desired project location:
```
cd /var/www/html
```

**Deprecated method (creates project in web folder):**
```
composer create-project drupal-composer/drupal-project:8.x-dev d8_test_project --stability dev --no-interaction
```

**Recommended method:**
```
composer create-project drupal/recommended-project project_dir
```
Or for a specific version:
```
composer create-project drupal/core-recommended:8.x-dev d8_test_project --stability dev --no-interaction
```

**Another deprecated method:**
```
composer create-project drupal/drupal my_site_name 8.1.*@dev --no-dev
```

## Create a Lightning Distribution Site
```
composer create-project acquia/lightning-project MYPROJECT
```

## Cloning a Live Project (Linux)
```
git clone https://[username]@bitbucket.org/[repo_name].git 
cd repo_name
composer install
```

### Install Database
```
drupal si
```
If there is an error, ensure `settings.php` is created. Delete all tables if needed (for Lightning Distribution).

Or use:
```
drush site-install standard --db-url=mysql://[db-user]:[db-pass]@localhost/[db-name] --account-mail="[mail-id]" --account-name=[site-admin] --account-pass=[site-admin-password] --site-mail="[site-mail-id]" --site-name="[name-of-site]"
```

Example:
```
drush site-install standard --db-url=mysql://root:spots@localhost/spm001 --account-mail="alameen@4spots.com" --account-name=superadmin --account-pass=123456 --site-mail="tech@4spots.com" --site-name="SPM001"
```

## Synchronize UUID
```
cat config/sync/system.site.yml | grep uuid
drupal config:override "system.site" uuid "<new-uuid>"
# OR
drush config-set "system.site" uuid "<new-uuid>"
```

## Delete Shortcut Set
```
drupal entity:delete shortcut_set default
# OR (not tested)
drush ev '\Drupal::entityManager()->getStorage("shortcut_set")->load("default")->delete();'
ddev drush entity:delete shortcut_link shortcut_set
```

## Import Configuration
```
drush cim
# OR
drupal ci
```
If error, check `settings.php` and set:
```
$config_directories['sync'] = '../config/sync';
```

## Cloning a Live Project (Windows)
```
git clone https://[username]@bitbucket.org/[repo_name].git 
cd repo_name
composer install
vendor/bin/drupal si
# In CMD
vendor\bin\drupal si
```

Synchronize UUID and import config as above.

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

## Debugging Configuration
- In `settings.local.php`, uncomment:
  ```php
  $config['system.performance']['css']['preprocess'] = FALSE;
  $config['system.performance']['js']['preprocess'] = FALSE;
  $settings['cache']['bins']['render'] = 'cache.backend.null';
  $settings['cache']['bins']['dynamic_page_cache'] = 'cache.backend.null';
  $settings['cache']['bins']['page'] = 'cache.backend.null';
  ```

## Enable Twig Debugging
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

## For Drupal 7
- In `settings.php`:
  ```php
  $conf['theme_debug'] = TRUE;
  ```
- Or via drush:
  ```
  drush variable-set theme_debug 1
  ```
