# 运算符(Operators)

## 运算符优先级

下表运算符优先级, 从高到低

```txt
[]
! ~ + -
is defined
** * / %
+ -
... ..
<= >= < >
in
== is != is not isnt
is a
&& and || or
?:
= := ?= += -= *= /= %=
not
if unless
```

## 一元运算符

以下一元运算符可用, !, not, -, +, 一级~

```stylus
!0
// => true

!!0
// => false

!1
// => false

!!5px
// => true

-5px
// => -5px

--5px
// => 5px

not true
// => false

not not true
// => true
```

逻辑运算符not的优先级较低, 因此下面的例子可以替换成:

```stylus
a = 0
b = 1

!a and !b
// > false
// 解析为: (!a) and (!b)
```

用:

```stylus
not a or b
// => false
// 解析为: not (a or b)
```

## 二元运算符

**下标运算符[]**允许通过获取表达式内部值. 括号表达式可以充当元组(如 (15px 5px), (1, 2, 3))

下面该例子使用错误处理的元组(并展示了该结构的多功能性)

```stylus
add(a, b)
  if a is a 'unit' and b is a 'unit'
    a + b
  else
    (error 'a 和 b必须是units!')

body
  padding add(1, '5')
  // => padding: error "a 和 b 必须是 units"

  padding add(1, '5')[0]
  // => padding: error

  padding add(1, '5')[0] == error
  // => padding: true

  padding add(1, '5')[1]
  // => padding: 'a'和b必须是units
```

一个更复杂的例子. 我们可以调用内置的`error()`函数, 当标识符(第一个值)等于`error`的时候返回错误信息.

```stylus
if (val = add(1, '5'))[0] == error
  error(val[1])
```

## 范围`.. ...`

同时体统包含接线操作符(`..`)和范围操作符(`...`). 如下:

```stylus
1..5
// => 1 2 3 4 5

1...5
// => 1 2 3 4
```

## 加减: + -

二元加乘运算器单位会转化, 或者使用默认字面量值. 例如, 5s - 2px结果是3s.

```stylus
15px - 5px
// => 10px

5 - 2
// => 3

5in - 50mm
// => 3.031in

5s - 1000ms
// => 4s

20mm + 4in
// => 121.6mm

'foo' + 'bar'
// => 'foo bar'

'num' + 15
// => 'num 15'
```

## 乘除:`/ * %`

```stylus
2000ms + (1s * 2)
// => 4000ms

5s / 2
// => 2.5s

4 % 2
// => 0
```

当在属性值内使用/时, **必须**用括号包住. 否则`/`会根据字面意思处理(支持css的`line-height`)

正常:`font: 14px/1.5`

但是`font: (14px/1.5)` 就等同于**14px ➗ 1.5**

**只有`/`操作符的时候需要这样.**

## 指数 **

指数操作符:

```stylus
2 ** 8
// => 256
```

## 相等与关系运算: == != >= <= > <

相等运算符可以被用来等同单位, 颜色, 字符串甚至标识符. 这个强大的概念, 甚至任意的标识符(如`wahoo`)可以作为原子般使用. 函数可以返回`yes`和`no`代替`true`和`false`(虽然不建议)

```stylus
5 === 5
// => true

10 > 5
// => true

#fff == #fff
// => true

true === false
// => false

wahoo == yay
// => false

wahoo == wahoo
// => true

"test" == "test"
// => true

true is true
// => true

"hey" is not 'bye'
// => true

"hey" isnt "bye"
// => true

(foo bar) == (foo bar)
// => true

(1 2 3) == (1 2 3)
// => true

(1 2 3) == (1 1 3)
// => false
```

只有精确值才匹配. 例如, `0 == false` 和`null == false`均返回false. 别名:

```txt
== is
!= is not
!= isnt
```

## 运算操作符:&& || 和 or

逻辑操作符&& 和 ||别名是and / or. 优先级相同

```stylus
5 && 3
// => 3

0|| 5
// => 5

0 && 5
// => 0

#fff is a 'rgba' and 15 is a 'unit'
// => true
```

## 存在操作符: in

检查左边内容是否在右边的表达式中. 例子:

```stylus
nums = 1 2 3
1 in nums
// => true

5 in nums
// => false
```

一些未定义标识符:

```stylus
words = foo bar baz
bar in words
// => true

HEY in words
// => false
```

元组同样适用:

```stylus
vars = (error 'one') (error 'two')
error in valus
// => false

(error 'one') in vals
// => true

(error 'two') in vals
// => true

(error 'something') in vals
// => false
```

混合是写适用例子:

```stylus
pad(types = padding, n = 5px)
  if padding in tyoes
    padding n
  if margin in types
    margin n

body
  pad()

body
  pad(margin)

body
  pad(padding margin, 10px)
```

对应于:

```css
body {
  padding: 5px;
}

body {
  margin: 5px;
}

body {
  padding: 10px;
  margin: 10px;
}
```

## 条件赋值: ?= :=

条件赋值操作符?=(别名?:)让我们无需破坏旧值(如果存在)定义变量. 该操作符可以扩展成三元内`is defined`的二元操作.

下面的都是等价的

```stylus
color := white
color ?= white
color = color is defined ? color : white
```

如果我们使用等号`=`,就只是简单地赋值.

```stylus
color = white
color = black

color
// => black
```

但当使用`?=`, 第二个并不会赋值成功(因为变量已经定义了):

```stylus
color = white
color ?= black

color
// => white
```

## 实例检查: is a

Stylus提供一个二元运算符叫做`is a`, 用作类型检查

```stylus
15 is a 'unit'
// => true

#fff is a 'rgba'
// => true

15 is a 'rgba'
// => false
```

另外, 我们可以使用`type()`这个内置函数.

```stylus
type(#fff) == 'rgba'
// => true
```

**注意:**color是唯一的特殊情况, 当左边是RGBA或者HSLA节点时,都为true

## 变量定义: is defined

该运算符用来检查变量是否已经分配了值.

```stylus
foo is defined
// => false

foo = 15px
foo is defined
// => true

#fff is defined
// => 'invalid "is defined" check on no-variable #fff'
```

另外, 我们可以使用内置lookup(name)方法做这个活动态查找

```stylus
name = 'blue'
lookup('light-' + name)
// => null

light-blue = #80e2e9
lookup('light-' + name)
// => #80e2e9
```

该操作符不可少, 因为一个未定义的标识符仍是真值. 如:

```stylus
body
  if ohnoes
    padding 5px
```

当未定义的时候, 产生的下面的CSS:

```css
body {
  padding: 5px;
}
```

显然, 这不是我们想要的, 如下书写就安全了:

```stylus
body
  if ohnoes is defined
    padding 5px
```

## 三元

三元运算符的运作正如大部分语言里面的那样. 三个操作对象的操作符(条件表达式, 真表达式及假表达式)

```stylus
num = 15
num ? unit(num, 'px') : 20px
// => 15px
```

## 铸造

作为替代简洁的内置`unit()`函数, 语法`(expr) unit`可用来强制后缀

```stylus
body
  n = 5
  foo: (n)em
  foo: (n)%
  foo: (n + 5)%
  foo: (n * 5)px
  foo: unit(n + 5, '%')
  foo: unit(5 + 180 / 2, deg)
```

## 颜色操作

颜色操作提供了一个简洁, 富有表现力的方式来改变其组成. 例如:

```stylus
#0e0 + #0e0
// => #0f0
```

另外一个例子是通过增加或建设百分值调整颜色亮度. 颜色亮(加), 暗(减)

```stylus
$foo + 50%
// => #c3c3c3

#888 - 50%
// => #444
```

我们可以通过增加或减去色度跳着色调. 例如, 红色增加`65deg`就变成了黄色.

```stylus
$f00 + 50deg
// => #ffd500
```

值适当固定. 例如, 我们可以"旋转"180度的色调, 如果目前的值是320deg, 将变为140deg

我们也可能一次调整几个值(包括alpha), 通过使用`rgb(), rgba(), hsl(), hsla()`

```stylus
#f00 - rgba(100, 0, 0, 0.5)
// => rgba(155, 0, 0, 0.5)
```

## 格式化字符串

格式化字符串模样的字符串%可以用来生成字面量值, 通过传参给内置s()方法.

```stylus
'x::Microsoft::Crap(%s)' % #fc0
// => x::Microsoft:Crap(#fc0)
```

多个值需要括起来:

```stylus
'-webkit-gradient(%s, %s, %s)' % (linear (0 0) (0 100%))
// => -webkit-gradient(linear, 0, 0, 0 100%)
```