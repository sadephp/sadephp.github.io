#### Component

Sade components takes it insperation from other components packages so you may be familiar. A component can have a template, script, style and php data.

Example:

```php
<template>
    <p>{{ greeting }} World!</p>
</template>

<style>
    p {
        font-size: 2em;
        text-align: center;
    }
</style>

<?php
    return [
        'data' => function() {
            return [
                'greeting' => 'Hello'
            ];
        }
    ];
?>
```

Template, script and style tags has a `src` attribute that can include other files instead of having all in the same file. All other attributes will be passed along to div (when scoped), script and style tags, some additional attributes will be added, read more about this below under each tag.

Example:

```html
<template src="accordion.twig" />
<script src="accordion.js" />
<style src="accordion.css" />
```

If combining `src` with a `external` attribute, then `src` attribute will be passed along as a real `src` attribute and no inline content will be added.

```html
<!-- Inline -->
<template src="accordion.twig" />
<!-- Not Inline -->
<script src="accordion.js" external />
<!-- Not inline -->
<style src="accordion.css" external />
```

### Template tag

The template tag contains [Twig](https://twig.symfony.com/doc/2.x/) (2.x) code and are compiled to HTML at runtime and cached if configured.

All attributes will be passed along.

### Script tag

All attributes will be passed along.

### Style tag

All attributes will be passed along (expect scoped attribute) and `data-sade-class` will be added when style is scoped.

The style tag will be rendered by default but can be configured to be rendered as a style tag.

Example:

```php
<style>
    p {
        font-size: 2em;
        text-align: center;
    }
</style>

<?php
    return [
        'scoped' => true
    ];
?>
```

CSS Output:

```css
.sade-8lhpfz p {
    font-size: 2em;
    text-align: center;
}
```

To style scoped div:

```php
<style>
    {
        font-size: 2em;
        text-align: center;
    }
</style>

<?php
    return [
        'scoped' => true
    ];
?>
```

CSS Output:

```css
.sade-8lhpfz {
    font-size: 2em;
    text-align: center;
}
```

### PHP data

PHP data use regulare `<?php ?>` tags. The returned array look like this:

```php
<?php
    return [
        'created'    => function() {
            // Update data with new values when component is being rendered.
            // Example: $this->ip = file_get_contents('https://api.ipify.org');
        },
        'components' => [
            'image.php', // <image />
            'Parent' => 'parent.php' // <Parent />
        ],
        'filters'    => [
            // Twig filters.
        ],
        'data'       => function() {
            return [
                // Data to component.
            ];
        },
        'methods'    => [
            // Twig functions.
        ],
        'props'      => [
            // Request props and data from parent component.
            // Request data from top parent component.
        ],
        // Scoped option.
        'scoped'     => false,
    ];
?>
```

* `components` are a array with key/value of other components to use.
* `filters` are a key/function array for Twig filters. You can access data here `$this->greeting` equals `greetings` from data array.
* `data` are a function that returns a array or array of data.
* `methods` are a key/function array for Twig functions. You can access data here `$this->greeting` equals `greetings` from data array.
* `props` are a array of properties to request from the parent component. Only parent properties is needed to be listed, not properties on a component html tag.
* `scoped` are a bool that's determines if the output css, html and style should be scoped or not.

### Custom functions

You can add custom functions or create plugins and bind them with:

```php
$sade->bind('http', function($sade) {
    return function ($url) {
        return file_get_contents($url);
    };
});
```

Then you can call them in `created, filters and methods` functions.

```php
return [
    'created' => function() {
        $this->ip = $this->http('https://api.ipify.org');
    }
];
```

### Parent components

Example using a parent component with properties:

```html
<template>
    <Parent name="Sade">
        <Child />
    </Parent>
</template>
```

Example of the child component:

```php
<template>
    {{ name }}
</template>

<?php
    return [
        'props' => [
            'name'
        ]
    ];
?>
```

### Children prop

We inject a `children` variable into Twig so you can render children html of a component html tag.

Example of parent and child component html tag:

```html
<template>
    <Parent name="Sade">
        <Child />
    </Parent>
</template>
```

Example of parent component:

```html
<template>
    {{ children }}
</template>
```

### Inherit functions

Instead of a child component add property names to `props` array they can use a inherit function. The inherit function is a custom function you write.

```php
function withParent(array $options) {
    if (!isset($options['props'])) {
        $options['props'] = [];
    }
     $options['props'][] = 'name';
     return $options;
}
```

Example of child component options:

```php
return withParent([]);
```