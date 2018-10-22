# vertical-align

## vertical-align 起作用的前提

`vertical-align` 属性并不是在所有元素上都有效果，只在特定的元素上有效果：

> Applies to	inline-level and table-cell elements. It also applies to ::first-letter and ::first-line.
> 
> The vertical-align property can be used in two contexts:
> 
> * To vertically align an inline element's box inside its containing line box. For example, it could be used to vertically position an <img> in a line of text:
> * To vertically align the content of a cell in a table:

上面部分摘抄自 MDN，明确说明了 `vertical-align` 属性只作用于 `display` 属性为 `inline-*` 或者 `table-cell` 的元素，在 `::first-letter` / `::first-line` 伪元素上也有效果；在其他类型的元素上无效。

## 可取值

`vertical-align` 属性有以下四大类取值：

```css
/* Keyword values */
vertical-align: baseline;
vertical-align: sub;
vertical-align: super;
vertical-align: text-top;
vertical-align: text-bottom;
vertical-align: middle;
vertical-align: top;
vertical-align: bottom;

/* <length> values */
vertical-align: 10em;
vertical-align: 4px;

/* <percentage> values */
vertical-align: 20%;

/* Global values */
vertical-align: inherit;
vertical-align: initial;
vertical-align: unset;
```

### 相对于父元素计算位置的取值

* `baseline` - 将元素的 baseline 与其父元素的 baseline 对齐；如果该元素没有 baseline，则将该元素的底边与其父元素的 baseline 对齐
* `super` - 将元素的 baseline 与其父元素的 super-baseline 对齐
* `sub` - 将元素的 baseline 与其父元素的 sub-baseline 对齐
* `text-top` - 将元素的 顶部 与其父元素中的字体容器（光标选中的背景）的顶部对齐，字体越大，字体容器越大，只受父元素字体大小的影响
* `text-bottom` - 将元素的 底部 与其父元素中的字体容器（光标选中的背景）的底部对齐，字体越大，字体容器越大，只受父元素字体大小的影响
* `middle` - 将元素的 垂直方向的中心 与其父元素的 baseline + 当前字体字符x（**非字符容器** ） 的一半的位置对齐，即如果此时有一个标签 `<span style="vertical-align: middle;">x</span>`，则另外一个元素的垂直方向的中心会与该 span 标签中字符 x 的中心对齐
* `<length>` - 将元素的 baseline 相对于其父元素的 baseline 向上偏移 `<length>` 像素
* `<percentage>` - 将元素的 baseline 相对于其父元素的 baseline 向上偏移 `<percentage> * line-height` 像素

### 相对于行计算位置的取值

* `top` - 将元素的顶部与当前所在容器的顶部对齐
* `bottom` - 将元素的底部与当前所在容器的底部对齐

### 数值类：长度数值 + 百分比数值

* 数值类可取值的范围同 `width` / `height` 等属性
* 在使用数值类设置该属性时，其偏移相对于 `baseline` 所在的位置进行上下偏移
* 如果使用百分比数值来设置 `vertical-align` 属性，结果相对于 `line-height` 来计算，即垂直对齐的位置相对于 `baseline` 的位置偏移 `百分比 * line-height`

## 内容垂直居中

通过辅助元素使元素垂直居中对齐：

```html
<div style="200px;">
	<img />
	<i></i>
</div>
```
```css
img, i {
	display: inline-block;
	vertical-align: middle;
}
i {
	height: 100%;
}
```

不使用辅助元素：

```html
<div >
	<img />
</div
```
```css
div {
	line-height: 200px;
	font-size: 0;
}
img {
	vertical-align: center;
}
```

## 参考

* [vertical-align](https://developer.mozilla.org/en-US/docs/Web/CSS/vertical-align)
* [Why baseline of `inline-block` element with `overflow:hidden` is set to its bottom margin?](https://stackoverflow.com/questions/32078950/why-baseline-of-inline-block-element-with-overflowhidden-is-set-to-its-bott/34183059)

## Author 🐓

* [Github](https://github.com/Tao-Quixote)
* Email: <web.taox@gmail.com>
