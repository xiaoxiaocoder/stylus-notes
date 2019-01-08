# CSS样式解析(CSS Style Syntax)

## CSS样式

Stylus完全支持常规的CSS样式解析, 这意味着无需寻求其他解析器, 或指定特别的文件使用特别的样式.

## 例子

```stylus
border-radius()
  -webkit-border-radius arguments
  -moz-border-radius  arguments
  border-radius arguments

body a
  font 12px/1.4 "lucida Grande", Arial, sans-serif
  background black
  color #ccc

form input
  padding 5px
  border 1px solid
  border-radius 5px
```

因为括号, 冒号及分号都是可选的, 因此上面的例子我们可以按照征程的CSS书写:

```stylus
border-radius()
  -webkit-border-radius: arguments
  -moz-border-radius: arguments
  border-radius: arguments

body a {
  font: 12px/1.4 "Lucida Grande", Arial, sans-serif
  background: black
  color: #ccc;
}

form input {
  padding: 5px;
  border: 1px solid
  border-radius: 5px
}
```

因为我们可以混合和匹配的两个辩题, 因此下面也是有效的:

```stylys
border-radius()
  -webkit-border-radius: arguments
  -moz-border-radius: arguments
  border-radius: arguments

body a {
  padding: 5px
  border: 1px solid;
  border-radius: 5px;
}

form input {
  padding: 5px;
  border: 1px solid
  border-radius: 5px
}
```

Stylus支持的变量, 函数, 混写以及其他特征也可以使之按预期工作:

```stylus
main-color = white
main-hover-color = black

body a {
  color: main-color
  &:hover {
    color: main-hover-color
  }
}

body a {
  color: main-color;
  &:hover {
    color: main-hover-color;
  }
}
```

此规则有一些注意事项; 因为这两种风格可以混合和匹配, 一些锁紧规则仍然适用. 所以, 虽然不是每一个普通的CSS样式零修改都起作用, 此功能仍然允许那些喜欢CSS语法的同学们继续这样做, 同时又可以利用Stylus的强大功能.
