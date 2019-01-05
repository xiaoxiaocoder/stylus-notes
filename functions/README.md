# 方法(Functions)

## 函数

Stylus强大之处就在其内置的语言函数定义. 其定义与混入(mixins)一致; 却可以返回值.

### 返回值

两数相加

```stylus
add(a, b)
  a + b
```

我们可以在特定条件下使用方法, 如在属性值中:

```stylus
body
  padding add(10px, 5)
```

渲染

```css
body {
  padding: 15px;
}
```

## 默认参数

可选参数往往有个默认的给定表达. 在Stylus中, 我们甚至可以超越默认参数.

```stylus
add(a, b = a)
  a + b

add(10, 5)
// => 15

add(10)
// => 20
```

**注意:**因为参数默认是赋值, 我们可以使用参数调用作为默认值.

```stylus
add(a, b = unit(a, px))
  a + b
```

## 函数体

我们可以吧简单的`add()`方法更进一步. 通过内置`unit()`把单位都变成px. 因为赋值在每个参数上, 因此, 我们可以无视单位转换.

```stylus
add(a, b = a)
  a = unit(a, px)
  b = unit(b, px)
  a + b

add(10%, 10deg)
// => 25
```

## 多个返回值

Stylus的函数可以返回多个值, 就像给变量赋多个值一样.

```stylus
sizes = 15px 10px

sizes[0]
/ => 15px
```

类似的, 我们可以在函数中返回多个值:

```stylus
sizes()
  15px 10px

sizes()[0]
// => 15px
```

一个**例外**就是返回值是标识符. 例如, 下面看上去像一个属性赋值给Stylus(因为没有操作符)

```stylus
swap(a, b)
```

为了避免歧义, 我么可以使用括号, 或者`return`关键字

```stylus
swap(a, b)
  (b, a)

swap(a, b)
  return b a
```

## 条件

比如, 我们想要创建一个名为`stringish()`的函数, 用来决定参数是否是字符串. 我们检查`val`是否是字符串或缩进(类似字符). 如下, 使用`yes`和`no`代替了`true`和`false`

```stylus
stringish(val)
  if val is a 'string' or val is a 'ident'
    yes
  else
    no
```

使用:

```stylus
stringish('yay')  == yes
// => true

stringish(yay) = yes
// => true

stringish(0) == no
// => true
```

**注意:**`yes`和`no`并不是布尔值. 本例中, 它们只是简单的未定义标识符.

另一个例子:

```stylus
compare(a, b)
  if a > b
    higher
  else if a < b
    lower
  else
    equal
```

使用:

```stylus
compare(5, 2)
// => higher

compare(1, 5)
// => lower

compare(10, 10)
// => equal
```

## 别名

给函数起个别名, 和简单,直接等于就可以了. 例如上面的`add()`弄个别名`plus()`, 如下:

```stylus
plus = add

puls(1, 2)
// => 3
```

## 变量函数

我们可以把函数当做变量传递到新的函数中. 例如,`invoke()`接受函数作为参数, 因此, 我们可以传递`add()`以及`sub()`

```stylus
invoke(a, b, fn)
  fn(a, b)

add(a, b)
  a + b

body
  padding invoke(5, 10, add)
  padding invoke(5, 10, sub)
```

结果:

```css
body {
  padding: 15;
  padding: -5;
}
```

## 参数

`arguments`是所有函数体都有局部变量, 包含传递的所有参数.

如:

```stylus
sum()
  n = 0
  for num in arguments
    n = n + num

sum(1,2,3,4,5)
/ => 15
```

## 哈希示例

下面, 我们定义`get(hash,key)`方法, 用来返回`key`值或者`null`, 我们遍历每个键值对, 如果键值匹配, 返回对应的值.

```styus
get(hash, key)
  return pair[1] if pair[0] == key for pair in hash
```

下面的例子可以证明, 语言函数模样的Stylus表达具有更大的灵活性

```stylus
hash = (one 1) (two 2) (three 3)

get(hash, two)
// => 2

get(hash, three)
// => 3

get(hash, something)
// => null

```