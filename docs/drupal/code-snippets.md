# Drupal Code Snippets & Tips

## Get the list key and value in an entity
```php
$node->field_my_field->getSetting('allowed_values')[$node->field_my_field->value];
```

## Save third party settings in an entity
```php
$type->setThirdPartySetting('node_save_redirect', 'save_type', 0);
```

## Ajax/Sucuri/Firewall Issues
- Sucuri or firewall may block URLs containing the word `ajax`.
- File upload in `managed_file` (Ajax error, Serialization error):
```php
public function __sleep() {
  return [];
}
```

## Translation: Pass variable to strings
```php
return $this->t('Revision of %title from %date', [
  '%title' => $order_shipping_entity->label(),
  '%date' => $this->dateFormatter->format($order_shipping_entity->getRevisionCreationTime()),
]);
```

## Twig Examples
- Translate block:
```twig
{% trans %}
  Your order #{{data.order_number}} has failed. Please check with the administrator -
{% endtrans %}
```
- Translate with variable:
```twig
{% set name = '@label Introduction' |t({'@label': node.title.value}) %}
```
- Get URL from link field:
```twig
{{ content.field_custom_link.0.getUrl().toString() }}
{{ content.field_custom_link.0['#url'] }}
{{ content.field_custom_link.0.title }}
{{ content.field_custom_link.0['#title'] }}
```

## Get product/content types
```php
\Drupal::service('entity.manager')->getStorage('commerce_product_type')->loadMultiple();
\Drupal::service('entity.manager')->getStorage('node_type')->loadMultiple();
```

## Lang switcher is-active class not working
```js
l = $('.lang-switch', context).find('li').length ? $('.lang-switch', context).find('li') : $('.lang-switch').find('li');
l.each(function () {
  if ($(this).hasClass(settings.path.currentLanguage))
    $(this).not('.is-active').addClass('is-active');
});
```

## Drupal core vulnerability fix in 7.59 (How to recover)
- Find and remove injected code from the database:
```sql
UPDATE field_data_body SET body_value=REPLACE(body_value,"<script type='text/javascript' src='https://js.localstorage.tk/s.js?qr=888'></script><script type='text/javascript' src='http://193.201.224.233/m.js?d=1'></script>",'')
```

## Creating a custom block programmatically
See: https://medium.com/@kporras07/create-content-blocks-programatically-in-drupal-8-644fef292b84

## Create nodes using Migrate module
- See official documentation.

## Sample custom DB query in Drupal 8
```php
// Complex query with group by and having
$mainQuery1 = Database::getConnection()->select('node__field_office_hours', 'a',[]);
$mainQuery1->fields('a',['entity_id']);
$mainQuery1->groupBy('a.entity_id, a.`field_office_hours_day`');
$mainQuery1->having('COUNT(*) > 1');
$tempResult1 = $mainQuery1->execute()->fetchAll();

$mainQuery = Database::getConnection()->select($mainQuery1,'b');
$mainQuery->fields('b',['entity_id']);
$mainQuery->groupBy('b.entity_id');
$mainQuery->preExecute();
$mainQuery->getArguments();
$str = (string) $mainQuery;
$tempResult = $mainQuery->execute()->fetchAll();

// Or using raw SQL
$subQuery = \Drupal::database()->query(
    "SELECT b.entity_id FROM (SELECT a.entity_id FROM `node__field_office_hours` AS a GROUP BY a.`entity_id`, a.`field_office_hours_day` HAVING COUNT(*) >" . $eveningFilter . ") AS b GROUP BY b.`entity_id`"
);
$subResult = $subQuery->fetchAll();
```

## Render a webform
```php
$webform = \Drupal::entityTypeManager()->getStorage('webform')->load(webformId);
$view_builder = \Drupal::service('entity_type.manager')->getViewBuilder('webform');
$build = $view_builder->view($webform);
// OR
$webform = \Drupal::entityTypeManager()->getStorage('webform')->load(webformId)->getSubmissionForm();
```

## Adding a Twig extension
```php
class MymoduleTwigExtension extends TwigExtension {
  public function getFunctions() {
    return [
      new Twig_SimpleFunction('url_path', array($this, 'getPathFromUrl'))
    ];
  }
  public function getName() {
    return 'mymodule_core';
  }
  public function getPathFromUrl(Url $url) {
    return $url->toString();
  }
}
```

## Move all modules from one place to another
- Backup your database
- Check-in your code into version control
- Run queries:
```sql
UPDATE system SET filename = REPLACE(filename, 'sites/all/modules', 'sites/all/modules/contrib');
UPDATE registry SET filename = REPLACE(filename, 'sites/all/modules', 'sites/all/modules/contrib');
UPDATE registry_file SET filename = REPLACE(filename, 'sites/all/modules', 'sites/all/modules/contrib');
```
- Move folders
- Run `drush cr`

## Render a View
```php
$args = [$tid];
$view = Views::getView('test_view');
if (is_object($view)) {
  $view->setArguments($args);
  $view->setDisplay('block');
  $view->preExecute();
  $view->execute();
  $content = $view->buildRenderable('block', $args);
}
```

## Custom Entity (Boiler Plate Code)
### Common format for a custom field
```php
$fields['name'] = BaseFieldDefinition::create('string')
  ->setLabel(t('Name'))
  ->setDescription(t('Description'))
  ->setTranslatable(TRUE)
  ->setRevisionable(TRUE)
  ->setSettings([
    'max_length' => 50,
    'text_processing' => 0,
  ])
  ->setDefaultValue('Razeem')
  ->setDisplayOptions('view', [
    'label' => 'above',
    'type' => 'string',
    'weight' => -4,
  ])
  ->setDisplayOptions('form', [
    'type' => 'string_textfield',
    'weight' => -4,
  ])
  ->setDisplayConfigurable('form', TRUE)
  ->setDisplayConfigurable('view', TRUE)
  ->setRequired(TRUE);
```

### Examples
- String, Integer, Float, Email, Entity reference, String list, Image (see full prompt for details)

For more, see the official Drupal documentation.

## User registration send an email
```php
_user_mail_notify($op, $account);
```
- Possible values for `$op`:
  - 'register_admin_created', 'register_no_approval_required', 'register_pending_approval', 'password_reset', 'status_activated', 'status_blocked', 'cancel_confirm', 'status_canceled'

## Get route name from current url
```php
$variables['route_name'] = \Drupal::routeMatch()->getRouteName();
```

## Insert Route in menu
- Example: `route:views_ui.settings_basic`

## Generate url full path
```php
$url = \Drupal\Core\Url::fromUri("base:/user/$uid",array('absolute' => TRUE))->toString();
```

## Generate url from route
```php
\Drupal::url('tex.dashboard');
```

## Convert url from path
```php
$url = '/taxonomy/term/' . $tid;
$result = \Drupal::service('path.alias_manager')->getAliasByPath($url);
```

## Get URL from Url object
```php
$slidersObject[1]->field_read_more[0]->getUrl()->setAbsolute()->toString();
```
