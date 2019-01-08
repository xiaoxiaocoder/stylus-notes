## 错误报告(Error Reporting)

## 错误报告

Stylus内置梦幻般的错误报告，针对语法、解析以及计算错误，完整的堆栈跟踪，行号和文件名。

解析错误
解析错误例子：

```stylus
body
  form input
    == padding 5px
```

呈现为：

```txt
Error: /Users/tj/Projects/stylus/testing/test.styl:4
  3: '  form input'
  4: '    == padding 5px'

illegal unary ==
```

## 计算错误

这种“运行”或计算错误类似于传递字符串给border-radius()，而不是单位值。

```stylus
ensure(val, type)
  unless val is a type
    error('expected a ' + type + ', but got ' + typeof(val))

border-radius(n)
  ensure(n, 'unit')
  -webkit-border-radius n
  -moz-border-radius n
  border-radius n

body
  border-radius '5px'
```

呈现为：

```txt
Error: /Users/tj/Projects/stylus/examples/error.styl:12
  11: ''
  12: 'body'
  13: '  border-radius \'5px\''
  14: ''

expected a unit, but got string
    at ensure() (/Users/tj/Projects/stylus/examples/error.styl:2)
    at border-radius() (/Users/tj/Projects/stylus/examples/error.styl:5)
    at "body" (/Users/tj/Projects/stylus/examples/error.styl:10)
```