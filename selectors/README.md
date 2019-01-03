# 选择器(Selectors)

## 缩排(indentation)

Stylus使用缩排和凹排代替花括号{ , }

```stylus
body
  color white

// 可以把冒号加上, 做分隔
body
  color: white
```

等价于

```css
body {
  color: #fff
}
```

## 规则集

Stylus和CSS一样, 允许使用**逗号**为多个选择器同事定义属性.

```stylus
textarea, input
  border 1px solid #eee

// 使用新行是一样的效果
textarea
input
  border 1px solid #eee
```

等同于

```css
textarea,
input {
  border: 1px solid #eee;
}
```

该规则**唯一的例外**就是长的像竖向的选择器. 例如, 下面的foo bar baz可能是个属性或者选择器.

```css
foo bar baz
  > input
    border 1px solid
```

为了解决该问题, 可以在尾部加个逗号:

```css
foo bar baz,
form input,
> a
  border 1px solid
```

## 父级引用

字符 **&** 指向父选择器. 下面示例中, 两个选择器(textarea和input)在:hover伪类选择器上都改变了**color**值

```stylus
textarea
input
  color #A7A7A7
  &:hover
    color #000
```

等同于

```css
textarea
input {
  color: #a7a7a7
}
textarea:hover
input:hover {
  color: #000
}
```

下面示例中, IE浏览器利用了父级引用一级混合书写来实现2px的边框

```stylus
box-shadow()
  -webkit-box-shadow arguments
  -moz-box-shadow arguments
  box-shadow arguments
  html.ie8 &,
  html.ie7 &,
  html.ie6 &
    border 2px solid arguments[length(arguments) - 1]
body
  #login
    box-shadow 1px 1px 3px #eee
```

编译后

```css
body #login {
  -webkit-box-shadow: 1px 1px 3px #eee;
  -moz-box-shadow: 1px 1px 3px #eee;
  box-shadow: 1px 1px 3px #eee;
}

html.ie8 body #login,
html.ie7 body #login,
html.ie6 body #login {
  border: 2px solid #eee;
}
```

## 消除歧义

类似**padding - n**的表达式可能既被解释成减法运算, 也可能被释义成一元负号属性. 为了避免这种歧义, 用括号包裹表达式:

```stylus
pad (n)
  padding (-n)

body
  pad(5px)
```

编译为:

```css
body {
  padding: -5px;
}
```

然鹅, 只有在函数中才会这样(因为函数同事用返回值扮演混合或回调)
比如, 下面这个就是OK的.

```css
body
  padding -5px
```

有stylus无法处理的属性值? **unquote()**

```stylus
filter
unquote(`progid:DXImageTransform.Microsoft.BasicImage(rotation=1)`)
```

生成为

```css
filter
progid: DXImageTransform.Microsoft.BasicImage(rotation=1)
```