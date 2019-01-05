# 插值(Interpolation)

## 插值

Stylus支持通过{}字符包围表达式来插入值, 其会变成标识符的一部分, 例如, `-webkit-{'border' + '-radius'}` 等同于`-webkit-border-radius`

以私有前缀属性扩展为例:

```stylus
vendor(prop, args)
  -webkit-{prop} args
  -moz-{prop} args
  {prop} args

border-radius()
  vendor('border-radius', arguments)

box-shadow()
  vendor('box-shadow', arguments)

button
  border-radius 1px 2px / 3px 4px
```

编译为:

```css
button {
  -webkit-border-radius: 1px 2px / 3px 4px;
  -moz-border-radius: 1px 2px / 3px 4px;
  border-radius: 1px 2px / 3px 4px;
}
```

## 选择器插值

插值也可以在选择器上起作用, 例如, 可以指定表格前5行的高度. 如下:

```stylus
table
  for row in 1 2 3 4 5
    tr:nth-child({row})
      height: 1px * row
```

也就是:

```css
table tr:nth-child(1) {
  height: 10px;
}

table tr:nth-child(2) {
  height: 20px;
}

table tr:nth-child(3) {
  height: 30px;
}

table tr:nth-child(4) {
  height: 40px;
}

table tr:nth-child(5) {
  height: 50px;
}
```