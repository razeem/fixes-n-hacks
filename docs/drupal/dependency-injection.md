# Drupal 8 Dependency Injection

## Method for Forms
```php
/**
 * Drupal\payment_myfatoorah\MyFatoorahExtensionService definition.
 * @var \Drupal\payment_myfatoorah\MyFatoorahExtensionService
 */
protected $myFatoorahExtension;

/**
 * Class constructor.
 */
public function __construct(MyFatoorahExtensionService $my_fatoorah_extension) {
  $this->myFatoorahExtension = $my_fatoorah_extension;
}

/**
 * {@inheritdoc}
 */
public static function create(ContainerInterface $container) {
  return new static(
    $container->get('payment_myfatoorah.extension')
  );
}
```

## Method for REST Plugins
```php
/**
 * Drupal\zain_jwt\ZainLoginService definition.
 * @var \Drupal\zain_jwt\ZainLoginService
 */
protected $zainLoginService;

/**
 * {@inheritdoc}
 */
public static function create(ContainerInterface $container, array $configuration, $plugin_id, $plugin_definition) {
  $instance = parent::create($container, $configuration, $plugin_id, $plugin_definition);
  $instance->zainLoginService = $container->get('zain_jwt.login');
  return $instance;
}
```

## Method using services.yml
- In `services.yml`:
  ```yaml
  abo_helper_module.helper:
    class: Drupal\abo_helper_module\HelperService
    arguments: ['@config.factory']
  ```
- In `service.php`:
  ```php
  /**
   * @var [Drupal\Core\Config\ConfigFactoryInterface]
   */
  protected $configFactory;

  /**
   * Constructs a new HelperService object.
   */
  public function __construct(
    ConfigFactoryInterface $config_factory
  ) {
    $this->configFactory = $config_factory;
  }
  ```
