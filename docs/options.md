#### Options

Default options:

```php
[
    // Change the config file name.
    'config'   => [
        'file' => 'sade.php',
    ],
    // Will cache output html so if you render same component again with only
    // the html and not script and style tags again.
    'cache'    => true,
    // Global scoped value.
    'scoped'   => false,
    'script'   => [
        // Point to your own script generator class.
        'class'   => \Sade\Component\Script::class,
        // Enable script tag rendering.
        'enabled' => true,
    ],
    'style'    => [
        // Point to your own style generator class.
        'class'   => \Sade\Component\Style::class,
        // Enable style tag rendering.
        'enabled' => true,
        'tag'     => 'script',
    ],
    'template' => [
        // Point to your own template generator class.
        'class'   => \Sade\Component\Template::class,
        // Enable template tag rendering.
        'enabled' => true,
    ],
]

$sade = new \Sade\Sade(__DIR__ . '/path/to/components', $options);
```