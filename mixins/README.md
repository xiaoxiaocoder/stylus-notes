# 混合书写(Mixins)

## 混入

混入和函数定义方法一致, 但是应用却大相径庭.

例如, 下面的`border-radius(n)`方法, 其却作为一个mixin(如, 作为状态调用, 而非表达式)调用.

当`border-radius()`选择器中调用时候, 属性会被扩展并复制在选择器中.

```stylus
border-radius(n)
  -webkit-border-radius n
  --moz-border-radius n
  border-radius n

form input[type=button]
  border-radius(5px)
```

编译成:

```css
form input[type=button] {
  -webkit-border-radius: 5px;
  -moz-border-radius: 5px;
  border-radius: 5px;
}
```

使用**混入**书写, 可以完全忽略**括号**. 即:

```stylus
form input[type=button]
  border-radius 5px
```

注意我们混合书写中的`border-radius`当做了属性, 而不是一个递归函数调用.

更进一步, 我们可以利用`arguments`这个局部变量, 传递可以包含多值得表达式.

```stylus
border-radius()
  -webkit-border-radius arguments
  -moz-border-radius arguments
  border-radius arguments
```

现在, 我们可以这样传值`border-radius 1px 2px / 3px 4px`

另一个很赞的应用的是特定的私有前缀属性--例如IE浏览器的透明度

```stylus
support-for-ie ?= true

opacity(n)
  opacity n
  if support-for-ie
    filter unquote('progid:DXImageTransform.Microsift.Alpha(Opacity-' + round(n * 100) +')')

#logo
  &:hover
    opacity 0.5
```

渲染为:

```css
#logo:hover {
  opacity: 0.5;
  filter: progid:DXImageTransform.Microsoft.Alpha(Opacity=50)
}
```

## 父级引用

混合书写可以利用父级引用字符`&`

例如, 我们要用`stripe(even, odd)`创建一个条纹表格. `even`和`odd`均提供了默认颜色值. 每行也指定了`background-color`属性. 我们可以在`tr`嵌套中使用`&`来引用`tr`. 已提供`even`颜色

```stylus
stripe(even = #fff, odd = #eee)
  tr
    background-color  odd
    &.even
    &:nth-child(even)
      background-color even
```

然后, 利用混合书写, 如下:

```stylus
table
  stripe()
  td
    padding 4px 10px

table#users
  stripe(#303030, #494848)
  td
    color white
```

另外, `stripe()`的定义无需父引用:

```stylus
stripe(even = #fff, odd = #eee)
  tr
    background-color odd
  td.even
  tr:nth-child(even)
    background-color even
```

也可以把`stripe()`当做属性调用

```stylus
stripe #fff #000
```

## 混合书写中的混合书写

混合书写可以利用其它混合书写, 建立在他们自己的属性和选择器上.

例如, 下面创建内联`comma-list()`(通过inline-list())以及逗号分隔的无序列表.

```stylus
inline-list()
  li
    display inline
  
comma-list()
  inline-list()
  li
    &:after
      conent ','
    &:laster-child:after
      content ''
ul
  comma-list()
```

渲染为:

```css
ul li:after{
  content: ',';
}

ul li:last-child:after {
  content: '';
}

ul li {
  display: inline;
}
```