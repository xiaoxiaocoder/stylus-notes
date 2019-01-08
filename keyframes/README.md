# 关键帧(@keyframes)

**@keyframes**

Stylus支持`@keyframes`规则, 当编译的时候转换成`@-webkit-keyframes`:

```stylus
@keyframes pulse
0%
  background-color red
  opacity 1.0
  -webkit-transform scale(1.0) rotate(0deg)

33%
  background-color blue
  opacity 0.75
  -webkit-transform scale(1.1) rotate(-5deg)

67%
  background-color green
  opacity 0.5
  -webkit-transform scale(1.1) rotate(5deg)

100%
  background-color red
  opacity 1.0
  -webkit-transform scale(1.0) rotate(0deg)
```

生成为:

```css
@-webkit-keyframes pulse {
  0%{
    background: red;
    opacity: 1;
    -webkit-transform: scale(1) rotate(0deg);
  }
  33% {
    background-color: blue;
    opacity: 0.75;
    -webkit-transform: scale(0.75) rotate(-5deg)
  }
  67% {
    background-color: green;
    opacity: 0.5;
    -webkit-transform: scale(0.5) rotate(5deg)
  }
  100% {
    background-color: red;
    opacity: 1;
    -webkit-transform: scale(1) rotate(0 deg);
  }
}
```

## 扩展

使用`@keyframes`, 通过`vendor`变量, 会自动添加私有前缀(`webkit moz offical`). 这意味着可以在任意时候立即高效修改.

```stylus
@keyframes foo {
  from {
    color: black;
  }
  to {
    color: white;
  }
}
```

扩增两个默认前缀. 官方解析:

```stylus
@-moz-keyframes foo {
  0% {
    color: #000;
  }
  100% {
    color: #fff;
  }
}

@-webkit-keyframes foo {
  0% {
    color: #000;
  }
  100% {
    color: #fff;
  }
}

@keyframes foo {
  0% {
    color: #000;
  }
  100% {
    color: #fff;
  }
}
```

如果我们只想有标准解析, 很简单, 修改`vendors`:

```stylus
vendors = offical

@keyframes foo {
  from: {
    color: black;
  }
  to: {
    color: white;
  }
}
```

生成为:

```css
@keyframes foo {
  0% {
    color: #000;
  }
  100% {
    color: #fff;
  }
}
```