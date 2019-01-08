# 媒体(@media)

`@media`工作原理和常规的CSS中一样, 但是, 要使用Stylus的块状符号.

```stylus
@media print
  #header
  #footer
    display none
```

生成为:

```css
@media print {
  #header,
  #footer {
    display: none;
  }
}
```