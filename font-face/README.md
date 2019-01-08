# 自定义字体(@font-face)

`@font-face`跟其在CSS中表现一样, 在后面简单地添加个块状属性即可. 类似:

```stylus
@font-face
  font-family Geo
  font-style normal
  src url(fonts/geo_sans_light/GensansLight.ttf)

.ingeo
  font-family Geo
```

生成为:

```css
@font-face {
  font-family: Geo;
  font-style: normal;
  src: url("fonts/geo_sans_light/GensansLight.ttf")
}

.ingeo {
  font-family: Geo;
}
```
