## 自检API(Introspection API)

## 自检API

Stylus支持自我检测的API, 这允许混写以及函数反应调用者的相关性。

## 混写(mixin)

mixin这个局部变量在函数体内自动赋值。如果调用的函数在根级别，则mixin包含字符串root, 如果其他情况，则是block, 如果调用函数有返回值，最终为false.

下面这个例子中，我们定义reset(), 根据其是混入了根部，还是混入块状域，还是混入返回值中，来修改其值，并作为foo属性的值呈现：

```stylus
reset()
  if mixin == 'root'
    got
      root true
  else if mixin
    got 'a mixin'
  else
    'not a mixin'

reset()

body
  reset()
  foo reset()
```

编译为：

```css
got {
  root: true;
}
body {
  foo: "not a mixin";
  got: "a mixin";
}
```