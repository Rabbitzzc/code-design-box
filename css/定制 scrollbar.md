**定制 scrollbar**
 
<div style="text-align:center">
    <img src="https://segmentfault.com/img/bV1RSv?w=700&h=443" style="width:200px">
</div>

浏览器的 `scrollbar` 具有以下几种属性

```
::-webkit-scrollbar — 整个滚动条.
::-webkit-scrollbar-button — 滚动条上的按钮 (上下箭头).
::-webkit-scrollbar-thumb — 滚动条上的滚动滑块.
::-webkit-scrollbar-track — 滚动条轨道.
::-webkit-scrollbar-track-piece — 滚动条没有滑块的轨道部分.
::-webkit-scrollbar-corner — 当同时有垂直滚动条和水平滚动条时交汇的部分.
::-webkit-resizer — 某些元素的corner部分的部分样式(例:textarea的可拖动按钮).
```

**几种常见的样式**

<div style="text-align:center">
    <img src="https://i.ibb.co/Pxp5Rrt/image.png" style="width:200px">
</div>

```js
#style-1::-webkit-scrollbar-track
{
	box-shadow: inset 0 0 6px rgba(0,0,0,0.3);
	border-radius: 10px;
	background-color: #F5F5F5;
}


#style-1::-webkit-scrollbar
{
	width: 12px;
	background-color: #F5F5F5;
}

#style-1::-webkit-scrollbar-thumb
{
	border-radius: 10px;
	box-shadow: inset 0 0 6px rgba(0,0,0,.3);
	background-color: #555;
}

#style-2::-webkit-scrollbar-track
{
	box-shadow: inset 0 0 6px rgba(0,0,0,0.3);
	border-radius: 10px;
	background-color: #F5F5F5;
}


#style-2::-webkit-scrollbar
{
	width: 12px;
	background-color: #F5F5F5;
}

#style-2::-webkit-scrollbar-thumb
{
	border-radius: 10px;
	box-shadow: inset 0 0 6px rgba(0,0,0,.3);
	background-color: #D62929;
}


#style-3::-webkit-scrollbar-track
{
	-webkit-box-shadow: inset 0 0 6px rgba(0,0,0,0.3);
	background-color: #F5F5F5;
}

#style-3::-webkit-scrollbar
{
	width: 6px;
	background-color: #F5F5F5;
}

#style-3::-webkit-scrollbar-thumb
{
	background-color: #000000;
}

#style-4::-webkit-scrollbar-track
{
	-webkit-box-shadow: inset 0 0 6px rgba(0,0,0,0.3);
	background-color: #F5F5F5;
}

#style-4::-webkit-scrollbar
{
	width: 10px;
	background-color: #F5F5F5;
}

#style-4::-webkit-scrollbar-thumb
{
	background-color: #000000;
	border: 2px solid #555555;
}
```