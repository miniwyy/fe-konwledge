#### 1.不同浏览器的标签默认的外边距和内填充不同

答：

**问题症状**：随便写几个标签，不加样式控制的情况下，各自的 margin 和 padding 差异较大

**解决方案**：CSS 里加入 `*{margin:0;padding:0;}`

**备注**：这个是最常见的也是最易解决的一个浏览器兼容性问题，几乎所有的 CSS 文件开头都会用通配符\*来设置各个标签的内外边距是 0。

#### 2.块属性标签 float 后，又有横行的 margin 情况下，在 IE6 显示 margin 比设置的大

答：

**问题症状**:常见症状是 IE6 中后面的一块被顶到下一行

**解决方案**：在 float 的标签样式控制中加入`display:inline;`将其转化为行内属性

**备注**：最常用的就是 div+CSS 布局了，而 div 就是一个典型的块属性标签，横向布局的时候通常都是用 div float 实现的，横向的间距设置如果用 margin 实现，这就是一个必然会碰到的兼容性问题。

#### 3.设置较小高度标签（一般小于 10px），在 IE6，IE7，遨游中高度超出自己设置高度

答：

**问题症状**：IE6、7 和遨游里这个标签的高度不受控制，超出自己设置的高度

**解决方案**：给超出高度的标签设置`overflow:hidden;`或者设置行高`line-height`小于设置的高度

**备注**：这种情况一般出现在设置小圆角背景的标签里。出现这个问题的原因是 IE8 之前的浏览器都会给标签一个最小默认的行高的高度。即使标签是空的，这个标签的高度还是会达到默认的行高。

#### 4.图片默认有间距

答：

**问题症状**：几个 img 标签放在一起的时候，有些浏览器会有默认的间距，而且通配符\*也不起作用。

**解决方案**：使用`float属性`为 img 布局

**备注**：因为 img 标签是行内属性标签，所以只要不超出容器宽度，img 标签都会排在一行里，但是部分浏览器的 img 标签之间会有个间距。去掉这个间距使用 float 是正道。（我之前使用负 margin，虽然能解决，但负 margin 本身就是容易引起浏览器兼容问题的用法，所以我后来不使用此方法）

#### 5.透明度的兼容 CSS 设置

答：

> 使用 hacker，可以把浏览器分为 3 类：IE6 ；IE7 和遨游；其他（IE8 chrome firefox safari opera 等）

◆IE6 认识的 hacker 是下划线`_`和星号`*`

◆IE7 遨游认识的 hacker 是星号`*`

**例子**：

```css
div {
  height: 300px;
  *height: 200px;
  _height: 100px;
}
```

说明：

    1.IE6浏览器在读到height:300px的时候会认为高是300px；继续往下读，它也认识*heihgt，所以当IE6读到*height:200px的时候会覆盖掉前一条的冲突属性值，认为高度是200px。继续往下读，IE6还认识_height,所以他又会覆盖掉200px高的设置，把高度设置为100px；
    2.IE7和遨游也是一样的从高度300px的设置往下读。当它们读到*height200px的时候就停下了，因为它们不认识_height。所以它们会把高度解析为200px；
    3.剩下的浏览器只认识第一个height:300px。

> 因为优先级相同且想冲突的属性设置后一个会覆盖掉前一个，所以书写的次序是很重要的。

#### 6.IE6 怪异解析，把 padding 与 border 算入宽高

答：

**问题症状**：未加文档声明造成非盒模型解析

**解决方案**：加入文档声明`<!DOCTYPE html>`

**备注**：假如不加 DOCTYPE 声明，那么各个浏览器会根据自己的行为去理解网页，即 IE 浏览器会采用 IE 盒子模型去解释你的盒子，而 Chrome 会采用标准 W3C 盒子模型解释你的盒子，所以网页在不同的浏览器中就显示的不一样了。反之，假如加上了 DOCTYPE 声明，那么所有浏览器都会采用标准 W3C 盒子模型去解释你的盒子，网页就能在各个浏览器中显示一致了。

> 标准 W3C 盒子模型的范围包括 margin、border、padding、content，并且 content 部分不包含其他部分。

> IE 盒子模型的范围也包括 margin、border、padding、content，和标准 W3C 盒子模型不同的是，IE 盒子模型的 content 部分包含了 border 和 padding。

**补充**：

CSS3 中有这样一个属性：box-sizing 属性允许以特定的方式定义匹配某个区域的特定元素。

`box-sizing: content-box|border-box|inherit`

    1.参数content-box：【标准W3C盒子模型】宽度和高度分别应用到元素的内容框。在宽度和高度之外绘制元素的内边距和边框。
    2.参数border-box：【IE盒子模型】为元素指定的任何内边距和边框都将在已设定的宽度和高度内进行绘制。通过从已设定的宽度和高度分别减去边框和内边距才能得到内容的宽度和高度。
    3.参数inherit：规定应从父元素继承box-sizing属性的值。

> W3C 终于承认了人家 IE 盒模型的合理性。通过设置 box-sizing 的值为 border-box 来模拟这一规范。

#### 7.IE6 在块元素、左右浮动、设定 marin 时造成 margin 双倍

答：

**问题症状**：在 IE6 下如果某个标签使用了 float 属性，同时设置了其外边距“margin:10px 0 0 10px”可以看出，上边距和左边距同样为 10px，但第一个对象距左边有 20px。

**解决方法**：将其`display`属性设置为`inline`时问题就解决了。

**备注**：这个现象仅当块级对象设置了浮动属性后才会出现，内联对象（行级对象）不会出现此问题。并且只有设置左边距和右边距的值才会出问题，上下边距不会出现问题。

#### 8.IE6 下高度小于 19px 的元素，高度会被当做 19px 来处理

答：

**解决方法**：将其`font-size`属性值设置为`0`时问题就解决了。

#### 9.浮动有什么作用？

答：

    1.使块元素在一行显示
    2.使内嵌支持宽高
    3.不设置宽度的时候宽度由内容撑开
    4.脱离文档流
    5.提升层级（半层） 层级包括【元素本身】和【元素内容】两部分，其中【元素内容】在上半层，【元素本身】在下半层

> 文档流是文档中可显示对象在排列时所占用的位置。

元素加了浮动，会脱离文档流，按照指定的一个方向（`left/right/none`）移动直到碰到父级的边界或者另外一个浮动元素停止

补充：在 IE6、7 的元素浮动要并在同一行的元素都要加浮动

#### 10.清除浮动的方法有哪些？

答：

    1.给浮动元素的父级添加浮动 // 相对麻烦，要不断给父级加浮动
    2.给浮动元素的父级添加display: inline-block // 本身不脱离文档流，但问题较多，样式要重新写
    3.在浮动元素下加<div class="clear"></div>
    .clear{ height: 0; font-size: 0; clear: both} // 要考虑IE6下的兼容性，所以加上font-size: 0;
    4.在浮动元素下加<br clear="all" />  // 兼容IE6，但不符合W3C标准
    [推荐]5.给浮动元素的父级加.clear{zoom: 1}
    .clear:after{ content: ""; display: block; clear: both;}// 在IE6、7下浮动元素的父级有宽度就不用清除浮动  关键词：hasLayout
    6.给浮动元素的父级添加overflow: auto; 一定要配合zoom: 1; // IE6下不起作用

> hasLayout 根据元素内容的大小 或者父级的父级的大小来重新的计算元素的宽高

    触发hasLayout有
    1. display: inline-block
    2. height: (任何值除了auto)
    3. float: (left或right)
    4. width: (任何值除了auto)
    5. zoom: (除了normal外任意值) // 作用是放大和缩小

#### 11.什么时候用 margin，什么时候用 padding？

答：

    使用margin的条件有：
    1.需要在border外侧添加空白区域时
    2.空白处不需要背景颜色时
    3.上下相连的两个盒子的空白，需要互相抵消时。例子：15px + 20px的margin，将得到20px的空白

    使用padding的条件有：
    1.需要在border内侧添加空白区域时
    2.空白处需要背景颜色时
    3.上下相连的两个盒子的空白，需要等于两者之和时。例子：15px + 20px的padding，将得到35px的空白

> 总的来说，margin 用来隔开元素与元素之间的距离，padding 用来隔开元素与内容之间的距离。

#### 12.CSS 中可以继承和不可以继承的有哪些？

答：

可以继承：

1.所有元素可以继承：`cursor`、`visibility`

2.内联元素可以继承：`color`、`line-height`、`font`、【`font-style`、`font-variant`、`font-family`、`font-size`、`font-width`】、【`text-decoration`、`text-transform`】、【`letter-spacing`、`word-spacing`、`white-space`】

3.列表元素可以继承：`list-style`、【`list-style-type`、`list-style-position`、`list-style-image`】

4.表格元素可以继承：`border-collapse`

不可以继承：

`width`、【`min-width`、`max-width`】、`height`、【`min-height`、`max-height`】、`display`、`margin`、`border`、`padding`、`background`、`position`、【`top`、`right`、`left`、`bottom`】、`float`、`clear`、`z-index`、`overflow`、`vertical-align`、`table-layout`
