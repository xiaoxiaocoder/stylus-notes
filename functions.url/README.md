# 函数 url

## 内联Data URI图像

Stylus捆绑了一个可选函数. `url()`, 其替换了字面上的`url()`调用(且使用base64 Data URIs有条件地内联它们).

### 示例

通过`require('stylus').url`该函数本事是可用的, 其接受一个options对象, 当看到`url()`时, 返回Stylus内部调用的函数.

`.define(name, callback)`方法指定了一个可被调用的JavaScript函数. 在这种情况下, 因为图片在`./css/images`中, 我们可以忽视paths选项(默认情况下, 会查找相关要呈现的图像文件). 如果愿意, 该行为时可以改变.

```stylus
stylus(str)
  .set('filename', __dirname + '/css/test.styl')
  .define('url', stylus.url())
  .render(function(err, css){
  })
```

例如, 想象图片在`./public/images`, 我们想要使用`url(images/tobi.png)`, 我们可以传递`paths`公共目录. 这样, 它就称为了向上查找进行的一部分.

同样, 如果想替换为`url(tobi.png)`, 我们可以传递`paths: [__dirname + '/public/images']`

```stylus
stylus(str)
  .set('filename', __dirname + '/css/test.styl')
  .define('url', stylus.url({paths: [__dirname + '/public']}))
  .render(function(err, css){})
```

## 选项(Options)

- limit 大小默认显示为30kb(30000)
- paths 图像解析路径
