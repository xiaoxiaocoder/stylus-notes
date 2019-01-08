## 连接中间件(Connect Middleware)

## 连接中间件

有了连接中间件，无论Stylus片段什么时候改变，这些片段都能够自动编译。

```js
stylus.middleware(options)
```

**选项**
返回给定options下的连接中间件。

```md
`serve`     Serve the stylus files from `dest` [true]
`force`     Always re-compile
`src`       Source directory used to find .styl files
`dest`      Destination directory used to output .css files
            when undefined defaults to `src`.
`compile`   Custom compile function, accepting the arguments
           `(str, path)`.
`compress`  Whether the output .css files should be 
            compressed
`firebug`   Emits debug infos in the generated css that can
            be used by the FireStylus Firebug plugin
`linenos`   Emits comments in the generated css indicating 
            the corresponding stylus line
```
上面中文翻译如下：

```md
`serve`     从 `dest` 提供stylus文件 [true]
`force`     总是重新编译
`src`       资源目录用来查找 .styl 文件
`dest`      `src`默认为undefined时，用来输出 .css 文件的目标目录
`compile`   自定义编译函数，接受参数`(str, path)`.
`compress`  是否输出的 .css 文件要被压缩
`firebug`   生成的CSS中发出调试信息，可被Firebug插件FireStylus使
            用
`linenos`   生成的CSS中发出注解，表明响应的stylus行
```

### 例子

从./public提供.styl文件。

```js
var app = connect();

app.middleware(__dirname + '/public');
```

改变src以及dest项来修改.styl文件哪里被加载，哪里被保存。

```js
var app = connect();

app.middleware({
  src: __dirname + '/stylesheets',
  dest: __dirname + '/public'
});
```

这里我们建立自定义的编译函数，这样，我们就能设置compress项，或是定义附加的函数。

默认情况下，编译函数是简单地设置filename以及渲染CSS. 在下面这个例子中，我们压缩输出内容，使用"nib"库插件，以及自动导入。

```js
function compile(str, path) {
  return stylus(str)
    .set('filename', path)
    .set('compress', true)
    .use(nib())
    .import('nib');
}
```

作为选项传递应该像这样：

```js
var app = connect();

app.middleware({
    src: __dirname
  , dest: __dirname + '/public'
  , compile: compile
})
```