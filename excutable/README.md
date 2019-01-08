# 可执行性(Excutable)

Stylus可执行代码

正因为stylus可执行性, Stylus才能将自身转换成CSS.

```md
Usage: stylus [options] [command] [<in [> out] [file|dir ...]

Commands:
  help <prop> Opens help info for <prop> in your default browser. (OS x Only)

Optios:
  -u, --use <path>        Utilize the stylus plugin at <path>
  -i, --interactive       Start interactive REPL
  -w, --watch             Watch file(s) for changes and re-compile
  -o, --out <dir>         Output to <dir> when passing files
  -C, --css <src> [dest]  Convert CSS Input to Stylus
  -I, --include <path>    Add <path> to lookup paths
  -c, --compress          Compress CSS  output
  -d, --compare           Display input along with output
  -f, --firebug           Emits debug infos in the generated css that can be used by the FireStylus                               Firebug plugin
  -l, --line-numbers      Emits comments in the generated CSS indicating the corresponding Stylus line
  -V, --version           Display the version of stylus
  -h, --help              Display help informattion
```

## STDIO编译范例

stylus读取stdin输出到stdout, 因此, 如下例:

```stylus
stylus --compress <some.styl> some.css
```

在终端机上尝试Stylus, 书写鞋面的内容, 然后按__EOF__(mac 回车)按下CTRL-D:

```stylus
$ stylus
  body
    color red
    font 14px Arial, sans-serif
```

## 编译文件范例

stylus亦接受文件和目录. 例如, 一个目录名为css将在同一目录编译并输出.css文件.

```stylus
stylus css
```

下面的将会输出到`./public/stylesheets`:

```bash
stylus css --out public/stylesheets
```

或一些文件:

```bash
stylus one.styl two.styl
```

为了开发的目的, 你可以使用`linenos`选项发出指令在生成的CSS中显示Stylus文件名以及行数.

```bash
stylus --line-numbers <path>
```

或是`firebug`选项, 如果想使用firebug的[fireStylus扩展](https://github.com/firebug/firebug)

```bash
stylus --firebug <path>
```

## 转换CSS

如果你想把CSS转换成简洁的Stylus语法，可以使用--css标志。

通过标准输入输出：

```bash
$ stylus --css < test.css > test.styl
```

输出基本名一致的.styl文件。

```bash
$ stylus --css test.css
```

输出特定的目标：

```bash
$ stylus --css test.css /tmp/out.styl
```

## CSS属性的帮助

在OS X上，stylus help <prop>会打开你默认浏览器并显示给定的<prop>属性的帮助文档。

```bash
$ stylus help box-shadow
```

## 壳层交互(Interactive Shell)

Stylus REPL (Read-Eval-Print-Loop)或“壳层交互(Interactive Shell)”允许你直接在终端机上把玩Stylus的表达式。

注意只有表达式可以生效，而不是选择器之类。为了简单，我们添加-i或--interactive标志：

```bash
$ stylus -i
> color = white
=> #fff
> color - rgb(200,50,0)
=> #37cdff
> color
=> #fff
> color -= rgb(200,50,0)
=> #37cdff
> color
=> #37cdff
> rgba(color, 0.5)
=> rgba(55,205,255,0.5)
```

## 利用插件

本例我们将使用[nib](https://github.com/visionmedia/nib)Stylus插件来说明它的CLI使用。

假设我们有如下的Stylus, 其导入nib并使用nib的linear-gradient()方法：

```bash
@import 'nib'

body
  background: linear-gradient(20px top, white, black) 
```

我们是使用stylus(1)通过标准输入输出试图渲染的第一个东西可能就像下面这样：

```bash
$ stylus < test.styl
```

这可能会生成如下的错误，因为Stylus不知道去哪里找到nib.

```txt
Error: stdin:3
    1| 
    2| 
  > 3| @import 'nib'
    4| 
    5| body
    6|   background: linear-gradient(20px top, white, black)
```

对于简单应用Stylus API们的插件，我们可以添加查找路径。通过使用--include或-I标志：

```
$ stylus < test.styl --include ../nib/lib
```

现在生成内容如下。您可能注意到了，gradient-data-uri()以及create-gradient-image()以字面量形式输出了。这是因为，当插件提供JavaScript API的时候，光暴露插件的路径是不够的。但是，如果我们仅仅想要的是纯粹Stylus nib函数，则足够了。

```css
body {
  background: url(gradient-data-uri(create-gradient-image(20px, top)));
  background: -webkit-gradient(linear, left top, left bottom, color-stop(0, #fff), color-stop(1, #000));
  background: -webkit-linear-gradient(top, #fff 0%, #000 100%);
  background: -moz-linear-gradient(top, #fff 0%, #000 100%);
  background: linear-gradient(top, #fff 0%, #000 100%);
}
```

因此，我们需要做的是使用--use或-u标志。其会找寻node模块（有或者没有.js扩展名）路径，这里的require()模块或调用style.use(fn())来暴露该插件（定义js函数等）。

```
$ stylus < test.styl --use ../nib/lib/nib
```

生成为：

```css
body {
  background: url("data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAAUCAYAAABMDlehAAAABmJLR0QA/wD/AP+gvaeTAAAAI0lEQVQImWP4+fPnf6bPnz8zMH358oUBwkIjKJBgYGNj+w8Aphk4blt0EcMAAAAASUVORK5CYII=");
  background: -webkit-gradient(linear, left top, left bottom, color-stop(0, #fff), color-stop(1, #000));
  background: -webkit-linear-gradient(top, #fff 0%, #000 100%);
  background: -moz-linear-gradient(top, #fff 0%, #000 100%);
  background: linear-gradient(top, #fff 0%, #000 100%);
}
```