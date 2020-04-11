#### button 样式


**基本样式**
```css
.button {
  display: inline-block;
  line-height: 1;
  white-space: nowrap;
  cursor: pointer;
  background: #fff;
  border: 1px solid #dcdfe6;
  color: #606266;
  -webkit-appearance: none;
  text-align: center;
  box-sizing: border-box;
  outline: none;
  margin: 0;
  transition: 0.1s;
  font-weight: 500;
  -moz-user-select: none;
  -webkit-user-select: none;
  -ms-user-select: none;
  padding: 12px 20px;
  font-size: 14px;
  border-radius: 4px;
}
```

**定制样式**

```css
/* primary */
.class-name {
    /* 字体 背景 边框 */
    color: #fff;
    background-color: #409eff;
    border-color: #409eff;
}

/* 禁用 */
.class-name {
    cursor: not-allowed;
}

/* 文字样式 */
.class-name {
    border-color: transparent;
    color: #409eff;
    background: transparent;
    padding-left: 0;
    padding-right: 0;
}

/* border round */
.class-name {
    border-radius: 20px;
    padding: 12px 23px;
}
```