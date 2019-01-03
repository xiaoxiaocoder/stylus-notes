# 变量(Variables)

## 变量

可以指定表达式为变量, 然后再样式中贯穿使用:

```stylus
font-size = 14px

body
  font font-size Arial, sans-seri
```

编译为:

```css
body {
  font: 14px Arial, sans-seri;
}
```

变量甚至可以组成一个表达式列表

```stylus
font-size = 14px
font = font-size "lucida Grande", Arial

body
  font font sans-serif
```

编译为:

```css
body {
  font: 14px "lucida Grande", Arial sans-serif;
}
```

标识符(变量名, 函数等), 也可能包括$字符. 例如:

```stylus
$font-size = 14px

body {
  font: $font-size sans-serif
}
```

## 属性查找

Stylus 有另外一个很酷的独特功能, 不需要分配值给变量就可以定义引用属性. 下面例子, 元素水平垂直居中对齐(典型的方法是使用百分比和margin负责). 如:

```stylus
#logo
  position: absolute
  top: 50%
  left: 50%
  width: w = 150px
  height: h = 80px
  margin-left: -(w / 2)
  margin-top: -(h / 2)
```

这里可以不使用变量w和h, 而是简单地前置@字符在属性名前来访问该属性名对应的值:

```stylus
#logo
  position: absolute
  top: 50%
  left: 50%
  width: 150px
  height: 80px
  margin-left: -(@width / 2)
  margin-top: -(@height / 2)
```

另外使用案例基于其他属性有条件的定义属性. 下例中, 我们默认指定z-index为1, 但是, 只有z-index之前未指定的时候才这样:

```stylus
position()
  position: arguments
  z-index 1 unless @z-index

#logo
  z-index: 20
  position: absolute

#logo2
  position: absolute
```

属性会"向上冒泡"查找堆栈知道被发现, 或者返回null(如果属性搞不定). 下个例子, @color被弄成blue

```stlyus
body
  color: red
  ul
    li
      color: blue
      a
        background-color: @color
```