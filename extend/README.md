# 继承(@extend)

继承

Stylus的`@extend`指定受[SAAS实现](http://sass-lang.com/documentation/file.SASS_REFERENCE.html#extend)的启发, 基本一致, 除了些轻微差异. 此功能大大简化了继承其他语义规则集的维护.

## 混合书写下的"继承"

尽管可以使用婚鞋实现类似效果, 但是会导致重复的CSS, 典型的模式定义如下的几个类名, 然后归结到一个元素中. 如"warning message".

```css
.message,
.warning {
  padding: 10px;
  border: 1px solid #eee;
}

.warning {
  color: #e2e21e;
}
```

这样实现没什么问题, 但是维护上比较麻烦.

## 使用__@extend__

使用`__@extend__`得到同样的输出, 只要把对应的选择器传给@extend即可. 然后`.warning`选择器就会继承已经存在的.message规则.

```stylus
.message {
  padding: 10px;
  border: 1px solid #eee;
}

.warning {
  @extend .message;
  color: #e2e21e;
}
```

一个更复杂的例子. 演示`__@extend__`如何级联:

```stylus
red = #E33E1E
yellow = #e2e21e

.message
  padding: 10px
  font: 14px Helvetica
  border: 1px solid #eee

.warning
  @extend .message
  border-color: yellow
  background: yellow + 70%

.error
  @extend .message
  border-color: red
  background: red + 70%

.fatal
  @extend .error
  font-weight: bold
  color: red
```

生成的css如下:

```css
.message,
.warning,
.error,
.fatal {
  padding: 10px;
  font: 14px Helvetica;
  border: 1px solid #eee;
}

.warning {
  border-color: #e2e21e;
  background: #f6f6bc;
}

.error,
.fatal {
  border-color: #e33e1e;
  background: #f7c5bc;
}

.fatal {
  font-weight: bold;
  color: #e33e1e;
}
```

Stylus中, 只要选择器匹配, 就可以生效:

```stylus
form
  input[type=text]
  padding: 5px
  border: 1px solid #eee
  color: #ddd

textarea
  @extend form input[type=text]
  padding: 10px
```

生成:

```css
form input[type=text],
form textarea {
  padding: 5px;
  border: 1px solid #eee;
  color: #ddd;
}

textarea {
  padding: 10px;
}
```