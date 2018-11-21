#### Config

When using the CLI or the [boilerplate](https://github.com/sadephp/boilerplate) you can configure Sade with a configuration file. When Sade is created it will look for `sade.php` in the directory passed and load it. If a function is returned it will send in the Sade instance as a argument.

Example config file:

```php
<?php

use Sade\Sade;

return function(Sade $sade) {
    // custom configuration.

};
```