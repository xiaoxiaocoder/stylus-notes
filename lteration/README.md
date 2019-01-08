# 迭代(Lteration)

## 迭代

Stylus允许通过for/in对表达式进行迭代形式如下:

```stylus
for <val-name> [,<key-name>] in <expression>
```

例如:

```stylus
body
  for num in 1 2 3
    foo num
```

生成:

```css
body {
  foo: 1;
  foo: 2;
  foo: 3;
}
```

下面的例子演示了如何使用`<key-name>`:

```stylus
body
  fonts = Impact Arial sans-serif
  for font, i in fonts
    foo i font
```

生成为:

```css
body {
  foo: o Impact;
  foo: 1 Arial;
  foo: 2 sans-serif;
}
```

## 混合书写(Mixins)

我们可以在混写中使用循环实现更大的功能, 例如, 我们可以把表达式对作为使用插值和循环的属性.

下面, 我们定义`apply()`, 利用所有的arguments, 这样逗号分隔以及表达式列表都会支持.

```stylus
apply(props)
  props = arguments if length(arguments) > 1
  for prop in props
    (porp[0]) [prop[1]]

body
  apply(one 1, two 2, three 3)

body
  list =(one 1) (two 2) (three 3)
  apply(list)
```

## 函数(Functions)

Stylus函数同样可以包含for循环, 示例:

求和

```stylus
sum(nums)
  sum = 0
  for n in nums
    sum += n

sum(1 2 3)
// => 6
```

连接:

```stylus
join(delim, args)
  buf = ''
  for arg, index in args
    if index
      buf += delim + arg
    else
      buf += arg

join(', ', foo bar baz)
// => "foo, bar, baz"
```

## 后缀(Postfix)

和`if/unless`可以利用后面语句一样, `for`也可以. 如下面后缀解析的例子:

```stylus
sum(nums)
  sum = 0
  sum += n for n in nums

join(delim, args)
  buf = ''
  buf += i ? delim + arg : arg for arg, i in args
```

也可以从循环`返回`, 下面例子就是`n%2 == 0`为true的时候返回数字.

```stylus
first-even(nums)
  return n if n % 2 == 0 for n in nums

first-even(1 3 5 5 6 3 2)
// => 6
```
