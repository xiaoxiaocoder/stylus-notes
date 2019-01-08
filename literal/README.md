# CSS字面量(CSS Literal)

## 字面量CSS

不管什么原因, 如果遇到Stylus搞不定的特殊需求, 可以使用`@css`使其作为CSS字面量解决.

```stylus
@css {
  body {
    font: 14px;
  }
}
```

编译为:

```css
body {
  font: 14px;
}
```
