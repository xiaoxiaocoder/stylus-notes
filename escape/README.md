# 字符转码(Char Escaping)

## 转码

Stylus可以字符转码. 可以让字符变成标识符, 或是渲染成字面量.

例如

```stylus
body
  padding 1 \+ 2
```

编译成:

```css
body {
  padding: 1 + 2
}
```

注意, Stylus中`/`当做属性使用的时候需要用括号括起来:

```stylus
body
  font 14px/1.4
  font (fontpx/1.4)
```

生成:

```css
body {
  font: 14px/1.4;
  font: 10px;
}
```