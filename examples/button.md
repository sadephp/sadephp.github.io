#### Counter

Simple counter example.

<iframe src="/examples/html/button.html" frameBorder="0" width="100%"></iframe>

#### Source code

```php
<template>
    <button>{{ text }}</button>
</template>

<style scoped>
    button {
        background: #e66969;
        color: #fff;
        border: none;
        border-radius: 3px;
        padding: 20px 20px;
    }
</style>

<script>
    document.querySelector('.{{ sade_classname }}').addEventListener('click', function () {
        alert('Hello, Sade!');
    });
</script>

<?php

return [
    'data' => [
        'text' => 'Submit',
    ],
];
```