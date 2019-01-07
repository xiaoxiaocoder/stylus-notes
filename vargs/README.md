# 其余参数(Rest Params)

## 其余参数

Stylus支持name...形式的其余参数. 这些参数可以消化传递给混写或函数的参数们. 这在处理浏览器私有属性, 如-moz或-webkit的时候很管用.

下面的这个例子中, 所有的参数们(1px 2px ...)都被一个args参数给点单的消化了:

```stylus
box-shadow(args...)
  -webkit-box-shadow args
  -moz-box-shadow args
  box-shadow args

#login
  box-shadow  1px 2px 5px $eee
```

生成为:

```css
#login {
  -webkit-box-shadow: 1px 2px 5px #eee;
  -moz-box-shadow: 1px 2px 5px #eee;
  box-shadow: 1px 2px 5px #eee;
}
```

我们想指定特定的参数, 如x-offset, 我们可以使用`args[0]`,或者可能西永重新定义混入.

```stylus
box-shadow(offset-x, args...)
  got-offset-x offset-x
  -webkit-box-shadow offset-x args
  -moz-box-shadow offset-x args
  box-shadow  offset args

#login
  box-shadow  1px 2px 5px #eee
```

生成为:

```css
#login {
  got-offset-x: 1px;
  -webkit-box-shadow: 1px 2px 5px #eee;
  -moz-box-shadow: 1px 2px 5px #eee;
  box-shadow: 1px 2px 5px #eee;
}
```

## 参数们

`arguments`变量可以实现表达式的精确传递, 包括逗号等. 这可以弥补`args...`参数的不足. 示例:

```stylus
box-shadow(args...)
  -webkit-box-shadow args
  -moz-box-shadow args
  box-shadow  args

#login
  box-shadow #ddd 1px 2px, #eee 2px 2px
```

编译为:

```css
#login {
  -webkit-box-shadow: #ddd 1px 1px #eee 2px 2px;
  -moz-box-shadow: #ddd 1px 1px #eee 2px 2px;
  box-shadow: #ddd 1px 1px #eee 2px 2px;
}
```

逗号给忽略了, 我们现在使用arguments重新邓毅这个混合书写.

```stylus
box-shadow()
  -webkit-box-shadow arguments
  -moz-box-shadow arguments
  box-shadow arguments

body
  box-shaodw #ddd 1px 2px, #eee 2px 2px
```

编译为:

```css
body {
  box-shadow: #ddd 1px 2px, #eee 2px 2px;
}
```
