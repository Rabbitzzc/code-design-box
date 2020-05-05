> 利用动画实现 donut-spin


```html run
<template>
    <div class="donut"></div>
</template>

<style>
    body {
        display: flex;
        justify-content: center;
    }
    .donut {
        display: inline-block;
        width: 30px;
        height: 30px;
        border: 4px solid #f1d1d1;
        border-radius:50%;

        border-left-color: #ff5200;

        animation: donut-spin 0.6s linear infinite;
    }

    @keyframes donut-spin {
        from {
            transform: rotate(0);
        }
        to {
            transform: rotate(360deg);
        }
    }
</style>
```