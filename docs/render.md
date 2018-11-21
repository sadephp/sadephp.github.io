#### Render

To render a Sade component you create a new instanceof the `\Sade\Sade` class with the source directory where you're components exists. If no directory is given then `getcwd()` will be used.

Example:

```php
$sade = new \Sade\Sade(__DIR__ . '/path/to/components');

echo $sade->render('greeting.php');
```

You can also render an array of files:

```php
echo $sade->render(['greeting.php', 'greeting.php']);
```

To only render one of the type tags (template, script or style):

```php
echo $sade->only('script')->render('greeting.php');

// or call magic methods (template, script or style):
echo $sade->script('greeting.php');
```