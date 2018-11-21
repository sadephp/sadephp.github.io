#### Counter

Simple counter example.

<iframe src="/examples/html/counter.html" frameBorder="0" width="100%"></iframe>

#### Source code

```php
<template>
        <h3>Count: <span id="count">{{ count }}</span></h3>
        <button id="plusOne">+1</button>
        <button id="minusOne">-1</button>
</template>

<script src="https://unpkg.com/mobx@5.6.0/lib/mobx.umd.js" external />
<script>
    (function () {
        var counter = mobx.observable({
            count: 0,
            update: mobx.action(function (val) {
                this.count += val;
            }),
        });

        mobx.when(function () {
            document.getElementById('count').innerHTML = counter.count;
        });

        mobx.autorun(function () {

        });

        document.getElementById('plusOne').addEventListener('click', function () {
            counter.update(+1);
        });

        document.getElementById('minusOne').addEventListener('click', function () {
            counter.update(-1);
        });
    }());
</script>

<?php

return [
    'data' => [
        'count' => 0,
    ]
];
```