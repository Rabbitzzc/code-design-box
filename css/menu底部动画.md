> 通常对于一些 tab || menu 字体下面都会有悬浮的小动画

### 侧边
```html run
<template>
<ul>
    <li>首页</li>
    <li>关于</li>
    <li>博客</li>
    <li>其他</li>
</ul>
</template>
<script></script>
<style>

ul {
    /* position:relative; */
}
li {
    color: #909399;
    background-color: #fff;
    list-style: none;
    display:inline-block;
    position:relative;
    left: 0;
    padding: 5px;
}

li:after {
    position:absolute;
    content:"";
    width:0;
    height:2px;
    left: 100%;
    bottom:0;
    background-color: #00adb5;
    transition: all .4s;
}

li:hover {
    color: #00adb5;
}

li:hover:after { 
    width: 100%;
    left: 0;
    transition-delay: 0.1s;
}

li:hover:~ li::after {
    left: 0;
}
</style>

```


### 中间
```html run
<template>
<ul class="tabs">
    <li>首页</li>
    <li>关于</li>
    <li>博客</li>
    <li>其他</li>
</ul>
</template>
<style>
li {
    color: #909399;
    background-color: #fff;
    list-style: none;
    display:inline-block;
    position:relative;
    left: 0;
    padding: 5px;
}

li:after {
    cursor: pointer;
    position:absolute;
    content:"";
    width:0;
    height:2px;
    left: 0;
    right: 0;
    bottom:0;
    margin: auto;
    background-color: #00adb5;
    transition: all .4s;
}

li:hover {
    color: #00adb5;
}

li:hover:after { 
    width: 100%;
    transition-delay: 0.1s;
}

</style>
```