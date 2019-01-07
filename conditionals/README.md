# 条件(Conditionals)

## 条件

条件提供了语言的流控制, 否则就是纯粹的静态语言. 提供的条件有导入, 混入, 函数以及更多.

### if / else if / else

```stylus
overload-padding = true

if overload-padding
  padding(y, x)
    margin y x

body
  padding 5px 10px
```

另外的例子:

```stylus
box(x, y, margin = false)
  padding y x
  if margin
    margin y x

body
  box(5px, 10px, true)
```

另外的`box()`帮手

```stylus
box(x, y, margin-only = false)
  if margin-only
    margin y x
  else
    padding y x
```

## 除非(unless)

与if相反, 本质上是`(!(expr))`

如果`disable-padding-override`是`undefined`或`false`, `padding`将被干掉, 显示`margin`代替. 但是, 如果是true, padding将会继续输出padding 5px 10px

```stylus
disable-padding-override = true

unless disable-padding-override is defined and disable-padding-override
  padding(x, y)
    margin y x

body
  padding 5px 10px
```

## 后缀条件

Stylus支持后缀条件, 这就意味着if和unless可以当做操作符, 当右边表示为真的时候执行左边的操作对象.

例如, 我们定义`negative()`来执行一些基本的检查. 下面使用块式条件:

```stylus
negative(n)
  unless n is a 'unit'
    error('无效数值')
  if n < 0
    yes
  else
    no
```

接下来, 我们使用后缀条件来让方法更简洁.

```stylus
negative(n)
  error('无效数值') unless n is a 'unit'
  return yese if n <0
  no
```

当然, 我们可以更进一步. 如这个n < 0 ? yes : no可以用布尔代替: n < 0

后缀条件适用于大多数的单行语句, 如果@import, @charset 混合书写等. 当然, 下面所示例的属性也是可以的.

```stylus
pad(types = margin padding, n = 5px)
  padding unit(n, px) if padding in types
  margin unit(n, px) if margin in types

body
  pad()

body
  pad(margin)

body
  apply-mixins = true
  pad(padding, 10) if apply-mixins
```

编译为:

```css
body {
  padding: 5px;
  margin: 5px;
}

body {
  margin: 5px;
}

body {
  padding: 10px;
}
```