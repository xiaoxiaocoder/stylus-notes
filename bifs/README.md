# 内置方法(Built-in Functions)

## red(color)

返回`color`中红色比重.

```stylus
red(#c00)
// => 204
```

## green(color)

返回`color`中绿色比重

```stylus
green(#0c0)
```

## blue(color)

返回`color`中蓝色比重

```stylus
blue(#00c)
// => 204
```

## alpha(color)

返回`color`中透明度比重.

```stylus
alpha(#fff)
// => 1

alpha(rgba(0, 0, 0, 0.3))
// => 0.3
```

## dark(color)

检查`color`是否是暗色

```stylus
dark(black)
// => true

dark(#005716)
// => true

dark(white)
// => false
```

## light(color)

检查`color`是否是亮色.

```stylus
light(black)
// => false

light(white)
// => true

light(#00FF40)
// => true
```

## hue(color)

返回给定`color`的色调.

```stylus
hue(hsla(50deg, 100%, 80%))
// => 50deg
```

## saturation(color)

返回给定`color`的饱和度

```stylus
saturation(hsla(50deg, 100%, 80%))
```

## lightness(color)

返回给定`color`的亮度

```stylus
lightness(hsla(50deg, 100%, 80%))
// => 80%
```

## push(expr, args...) 别名append()

后面推送给定的`args`给`expr`

```stylus
nums = 1 2
push(nums, 3, 4, 5)

nums
// => 1 2 3 4 5
```

## unshift(expr, args...) 别名 prepend()

起始位置插入给定的args给expr

```stylus
nums = 4 5
unshift(nums, 3, 2, 1)

nums
// => 1 2 3 4 5
```

## keys(pairs)

返回给定pairs中的键

```stylus
pairs = (one 1) (two 2) (three 3)
keys(pairs)

// => one two three
```

## values(pairs)

返回给的pairs中的值.

```stylus
pairs = (one 1) (two 2) (three 3)
values(pairs)
// => 1 2 3
```

## typeof(node) 别名type-of, type

字符串形式返回`node`类型

```stylus
type(12)
// => 'unit'

typeof(12)
// => 'unit'

typeof(#fff)
// => 'rgba'

typeof(#fff)
// => 'rgba'
```

## unit(unit[, type])

返回`unit`类似的字符串或空字符串, 或者赋予`type`值而无需单位转换.

```stylus
unit(10)
// => ''

unit(15in)
// => 'in'

unit(15%, 'px')
// => 15px

unit(15%, px)
// => 15px
```

## match(pattern, string)

检测`string`是否匹配给定的`pattern`

```stylus
match('^foo(bar)?', foo)
match('^foo(bar)?', foobar)
// => true

match('^foo(bar)?', 'foo')
match('^foo(bar)?', 'foobar')
// => true

match('^foo(bar)?', 'bar')
// => false
```

## abs(unit)

绝对值

```stylus
abs(-5px)
// => 5px

abs(5px)
// => 5px
```

## ceil(unit)

向上取整

```stylus
ceil(5.5in)
// => 6in
```

## floor(unit)

向下取整

```stylus
floor(5.6px)
// => 5px
```

## round(unit)

四舍五入取整

```stylus
round(5.5px)
// => 6px

round(5.4px)
// => 5px
```

## min(a, b)

取较小值

```stylus
min(1, 5)
// => 1
```

## max(a, b)

取较大值

```stylus
max(1, 4)
// => 4
```

## even(unit)

是否为偶数

```stylus
even(6px)
// => true
```

## odd(unit)

是否为奇数

```stylus
odd(5em)
// => true
```

## sum(nums)

求和

```stylus
sum(1 3 4)
// => 8
```

## avg(nums)

求平均数

```stylus
avg(1 2 3)
// => 2
```

## join(delim, vals...)

给定`vals`使用`delim`连接

```stylus
join('', 1 2 3)
// => "1 2 3"

join(',', 1 2 3)
// => "1,2,3"

join(', ', foo bar baz)
/ => "foo, bar, baz"

join(", ", foo, bar, baz)
// => "foo, bar, baz"

join(", ", 1 2, 3 4, 5 6)
// => "1 2, 3 4, 5 6"
```

## hslaa(color|h,s,l,a)

转换给定`color`为HSLA节点, 或h,s,l,a比重值.

```stylus
hslaa(1odeg, 50%, 30%, 0.5)
// => HSLA

hslaa(#ffcc00)
// => HSLA
```

## hsla(color|h,s,l)

转换给定`color`为HSLA节点,或h,s,l比重值.

```stylus
hsla(10, 50, 30)
// => HSLA

hsla(#ffcc00)
// => HSLA
```

## rgba(color|r,g,b,a)

从r,g,b,a通道返回RGBA, 或提供color来调整透明度.

```stylus
rgba(255, 0, 0, 0.5)
// => rgba(255, 0, 0, 0.5)

rgba(255, 0, 0, 1)
// => #ff0000

rbga(#ffcc00, 0.5)
// => rgba(255,204,0,0.5)
```

另外, stylus支持#rgba以及#rrggbbaa符号

```stylus
#fc08
// => rgba(255, 204, 0, 0.5)

#ffcc00ee
// => rgba(255, 204, 0, 0.9)
```

## rbg(color | r, g, b)

从r,g,b通道返回RGBA或生成一个RGBA节点.

```stylus
rgb(255,204,0)
// => #ffcc00

rgb(#fff)
// => #fff
```

## lighten(color, amount)

给定color增量amount值. 该方法单位敏感. 例如, 支持百分比, 如下:

```stylus
lighten(#2c3c3c, 30)
// => #787878

lighten(#2c2c2c, 30%)
// => #393939
```

## darken(color, amount)

给定`color`变暗`amount`值. 该方法单位敏感. 例如, 支持百分比, 如下:

```stylus
darken(#D6282828, 30)
// => #551010

darken(#D62828, 30%)
// => #961c1c
```

## desaturate(color, amount)

给定`color`饱含度减小`amount`.

```stylus
desatureate(#f00, 40%)
// => #c33
```

## saturate(color, amount)

给定color饱含度减小amount

```stylus
saturate(#c33, 40%)
// => #f00
```

## invert(color)

颜色反相. 红绿蓝色反转, 透明度不变.

```stylus
invert(#d62828)
// => #29d7d7
```

## unquote(str|ident)

给定str引导去除, 返回literral节点.

```stylus
unquote('sans-serif')
// => sans=serif

unquote(sans-serif)
// => sans-serif

unquote('1px/2px')
// => 1px / 3px
```

## s(fmt, ...)

`s()`方法类似于`unquote()`, 不过后者返回的literal节点, 而这里起接受一个格式化的字符串, 非常像C语言的`sprintf()`, 目前, 唯一标识符是%s.

```stylus
s('bar()')
// => bar()

s('bar(%s)', 'baz')
// => bar(baz)

s('bar(%s)', 15px)
// => bar(15px)

s('rgba(%s, %s, %s, 0.5)', 255, 100, 50)
// => rgba(255, 100, 50, 0.5)

s('bar(%z)', 15px)
// => bar(%z)

s('bar(%s, %s)', 15px)
// => bar(15px. null)
```

## operate(op, left, right)

在left和right操作对象上执行给定的op

```stylus
op = '+'
operate(op, 15, 5)
// => 20
```

## length([expr])

括号表达式扮演元组, length()方法返回该表达式的长度.

```stylus
length(1 2 3 4)
// => 4

length(1 2)
// => 2

length(())
// => 0

length(1 2 3)
//=> 3

length(1)
// => 1

length()
// => 0
```

## warn(msg)

使用给定的error警告, 并不退出.

```stylus
warn('oh noes!')
```

## error(msg)

伴随给定的错误msg退出

```stylus
add(a, b)
  unless a is a 'unit' and b is a 'unit'
    error('add() expects units')
  a + b
```

## last(expr)

返回给定expr的最后一个值.

```stylus
nums = 1 2 3
last(nums)
last(1 2 3)
// => 3

last = (one 1) (two 2) (three 3)
last(list)
// => (three 3)
```

## p(expr)

检查给定的expr

```stylus
fonts = Arial, sans-serif
p('test'
p(123)
p((1 2 3))
p(fonts)
p(#fff)
p(rgba(0, 0, 0, 0.2))

add(a,b)
  a + b

p(add)
```

标准输出:

```bash
inspect: "test"
inspect: 123
inspect: 1 2 3
inspect: Arial, sans-serif
inspect: #fff
inspect: rgba(0, 0, 0, 0.2)
inspect: add(a, b)
```

## opposite-position(positions)

返回给定positions相反内容.

```stylus
opposite-position(right)
// => left

opposite-positoin(top left)
// => bottom right

opposite-position('top', 'left')
// => bottom right
```

## image-size(path)

返回指定path图片的width和height, 向上查找路径的方法和@import一样, paths设置的时候改变.

```stylus
width(img)
  return image-size(img)[0]

height(img)
  return image-size(img)[1]

image-size('tux.png')
// => 405px 250px

image-size('tux.png')[0] == width('tux.png')
// => true
```

## add-property(name, expr)

使用给定的expr为最近的块域添加属性name.

例如:

```stylus
something()
  add-property('bar', 1 2 3)
  s('bar')

body
  foo: something()
```

编译为:

```css
body {
  bar: 1 2 3;
  foo: bar;
}
```

接下来, "神奇"的`current-property`局部变量将大方异彩, 这个变量自动提供给函数体, 且包含当前属性名和值得表达式.

例如, 我们使用`p()`检查这个局部变量, 我们可以得到:

```stylus
p(current-property)
// => "foo" (foo __CALL__ bar baz)

p(current-property[0])
// => "foo"

p(current-property[1])
// => foo __CALL__ bar baz
```

使用current-property我们可以让例子走的更远, 使用新值复制改属性, 且确保功能的条件且确保功能的条件仅在属性中使用.

```stylus
something(n)
  if current-property
    add-property(current-property[0], s('-webkit-something(%s)', n))
    add-prperty(current-property[0], s('-moz-something(%s)', n))
    s('something(%s)', n)
  else
    error('something() must be used within a property')

body {
  foo: something(15px) bar;
}
```

生成为:

```css
body {
  foo: -webkit-something(15px);
  foo: -moz-something(15px);
  foo: something(15px) bar;
}
```

注意上面的例子, 会发现bar只在一开始调用的时候出现, 因为我们返回something(15px), 其仍留在表达式里, 然而, 其他人并不重视其余的表达式.

更强大的解决方案如下, 定义一个名为replace()的函数, 其克隆表达式, 以防止出现变化, 用另外一个替换表达式的字符串值, 并返回克隆的表达式. 然后我们继续在表示式中替换__CALL__, 表示循环调用something()

```stylus
replace(expr, str, val)
  expr = clone(expr)
  for e, i in expr
    if str == e
      expr[i] = val
  expr

something(n)
  if current-property
    val = current-property[1]
    webkit = replace(val, '__CALL__', s('-webkit-something(%s)', n)
    moz = replace(val, '__CALL__', s('-moz-something(%s)', n))
    add-property(current-property[0], webkit)
    add-property(current-propertu[0], moz)
    s('something(%s)', n)
  else
    error('something() 必须在属性中.')
```

生成:

```css
body {
  foo: foo -webkit-something(5px) bar baz;
  foo: foo -moz-something(5px) bar baz;
  foo: foo something(5px) bar baz;
}
```
无论是内部调用的使用还是调用的位置升, 我们事先了方法现在是完全透明的了. 这个强大的概念有助于在一些私有属性使用时调用, 例如渐变.

## 未定义方法

未定义方法 - 字面量形式输出. 例如, 我们可以在CSS中调用`rgba-stop(50%, #fff)`, 其会按照你所期望的显示, 我们也可以使用这些内部助手.

下面例子中简单定义了方法`stop()`, 其返回了字面上`rgba-stop()`调用.

```stylus
stop(pos, rgba)
  rgba-stop(pos, rgba)

stop(50%, orange)
// => rgba-stop(50%, #ffa500)
```