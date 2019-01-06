# 关键字参数(Keyword Arguments)

## 关键字参数

Stylus支持关键字参数, 或"kwargs". 允许你根据相关参数名引用参数.

下面的这些例子功能上都是一样的. 但是, 我们可以在列表中的任何地方防止关键字参数. 其余不键入参数将适用于尚未得到满足的参数.

```stylus
body {
  color: rgba(255, 200, 100, 0.5)
  color: rgba(red: 255, green: 200, blue: 100, alpha: 0.5)
  color: rgba(alpha: 0.5, blue: 100, red: 255, 200)
  color: rgba(alpha: 0.5, blue: 100, 255, 200)
}
```

等同于

```css
body {
  color: rgba(255, 200, 100, 0.5);
  color: rgba(255, 200, 100, 0.5);
  color: rgba(255, 200, 100, 0.5);
  color: rgba(255, 200, 100, 0.5);
}
```

查看函数或混合书写中接受的参数, 可以使用`p()`方法

```stylus
p(rgba)
```

生成

```css
inspect: rgba(red, green, blue, alpha);
```