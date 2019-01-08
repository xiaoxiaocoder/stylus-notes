# 导入(@import)

## 导入

Stylus支持字面`@import` CSS,也支持其他Stylus 样式的动态导入.

### 字面CSS

任何`.css`扩展的文件名将作为字面量. 例如:

```stylus
@import "reset.css"
```

渲染如下:

```css
@import "reset.css"
```

## Stylus导入

当使用`@import`没有.css扩展, 会被认为是Stylus片段(如:`@import "mixins/border-radius"`)

`@import`工作原理为: 遍历目录队列, 并检查任意目录中是否有该文件(类似node的`require.paths`). 该队列默认为单一路径, 从`filename`选项的`dirname`衍生而来. 因此, 如果你的文件名是`/tmp/testing/stylus/main.styl`. 导入将显示为`/tmp/testing/stylus/`.

`@import`也支持索引形式. 这意味着当你`@import blueprint`, 则会理解成`blueprint.styl`或`blueprint/index.styl`. 对于库而言, 这很有用, 既可以扎实所有特征与功能, 同时又能导入特征子集.

如下库结构:

```txt
./tablet
  |-- index.styl
  |-- vendor.styl
  |-- buttons.styl
  |-- images.styl
```

下例中, 我们设置`paths`选项用来为`Stylus`提供额外路径. 在`./test.styl`中, 我们可以`@import "mixins/border-radius"` 或者 `@import "border-radius"` (因为`./mixins`暴露给了Stylus)

```js
/*
* 依赖模块
*/

var stylus = require('../')
    ,str = require('fs').readFileSync(__dirname + '/test.styl', 'utf8')

var paths = [
  __dirname
  , __dirname + '/mixins'
];

stylus(str)
  .set('filename', __dirname + '/text.styl')
  .set('paths', paths)
  .render(function(err, css){
    if(err) throw err;
    console.log(css)
  })
```

## JavaScript 导入API

当使用`.import(path)`方法, 这些导入是被推迟的, 直到赋值.

```js
var stylus = require('../')
    , str = require('fs').readFileSync(__dirname + '/test.styl', 'utf8');

stylus(str)
  .set('filename', __dirname + '/test.styl')
  .import('mixins/vendor')
  .render(function(err, css){
    if(err) throw err;
    console.log(css)
  })
```

下面的

```stylus
@import "mixins/vendor"
```

等同于

```stylus
.import('mixins/vendor')
```