#### 1.不同浏览器的标签默认的外边距和内填充不同

答：

**问题症状**：随便写几个标签，不加样式控制的情况下，各自的margin和padding差异较大

**解决方案**：CSS里加入 `*{margin:0;padding:0;}`

**备注**：这个是最常见的也是最易解决的一个浏览器兼容性问题，几乎所有的CSS文件开头都会用通配符*来设置各个标签的内外边距是0。

#### 2.块属性标签float后，又有横行的margin情况下，在IE6显示margin比设置的大

答：

**问题症状**:常见症状是IE6中后面的一块被顶到下一行

**解决方案**：在float的标签样式控制中加入`display:inline;`将其转化为行内属性

**备注**：最常用的就是div+CSS布局了，而div就是一个典型的块属性标签，横向布局的时候通常都是用div float实现的，横向的间距设置如果用margin实现，这就是一个必然会碰到的兼容性问题。

#### 3.设置较小高度标签（一般小于10px），在IE6，IE7，遨游中高度超出自己设置高度

答：

**问题症状**：IE6、7和遨游里这个标签的高度不受控制，超出自己设置的高度

**解决方案**：给超出高度的标签设置`overflow:hidden;`或者设置行高`line-height`小于设置的高度

**备注**：这种情况一般出现在设置小圆角背景的标签里。出现这个问题的原因是IE8之前的浏览器都会给标签一个最小默认的行高的高度。即使标签是空的，这个标签的高度还是会达到默认的行高。

#### 4.图片默认有间距

答：

**问题症状**：几个img标签放在一起的时候，有些浏览器会有默认的间距，而且通配符*也不起作用。

**解决方案**：使用`float属性`为img布局

**备注**：因为img标签是行内属性标签，所以只要不超出容器宽度，img标签都会排在一行里，但是部分浏览器的img标签之间会有个间距。去掉这个间距使用float是正道。（我之前使用负margin，虽然能解决，但负margin本身就是容易引起浏览器兼容问题的用法，所以我后来不使用此方法）

#### 5.透明度的兼容CSS设置

答：

> 使用hacker，可以把浏览器分为3类：IE6 ；IE7和遨游；其他（IE8 chrome firefox safari opera等）

◆IE6认识的hacker是下划线`_`和星号`*`

◆IE7 遨游认识的hacker是星号`*`

**例子**：
```css
div{
    height:300px;
    *height:200px;
    _height:100px;
} 
```
说明：

    1.IE6浏览器在读到height:300px的时候会认为高是300px；继续往下读，它也认识*heihgt，所以当IE6读到*height:200px的时候会覆盖掉前一条的冲突属性值，认为高度是200px。继续往下读，IE6还认识_height,所以他又会覆盖掉200px高的设置，把高度设置为100px；
    2.IE7和遨游也是一样的从高度300px的设置往下读。当它们读到*height200px的时候就停下了，因为它们不认识_height。所以它们会把高度解析为200px；
    3.剩下的浏览器只认识第一个height:300px。
    
> 因为优先级相同且想冲突的属性设置后一个会覆盖掉前一个，所以书写的次序是很重要的。


#### 6.IE6怪异解析，把padding与border算入宽高 

答：

**问题症状**：未加文档声明造成非盒模型解析 

**解决方案**：加入文档声明`<!DOCTYPE html>` 

**备注**：假如不加DOCTYPE声明，那么各个浏览器会根据自己的行为去理解网页，即IE浏览器会采用IE盒子模型去解释你的盒子，而Chrome会采用标准W3C盒子模型解释你的盒子，所以网页在不同的浏览器中就显示的不一样了。反之，假如加上了DOCTYPE声明，那么所有浏览器都会采用标准W3C盒子模型去解释你的盒子，网页就能在各个浏览器中显示一致了。

> 标准W3C盒子模型的范围包括margin、border、padding、content，并且content部分不包含其他部分。

>IE盒子模型的范围也包括 margin、border、padding、content，和标准W3C盒子模型不同的是，IE盒子模型的content部分包含了border和padding。

**补充**：

CSS3中有这样一个属性：box-sizing属性允许以特定的方式定义匹配某个区域的特定元素。

`box-sizing: content-box|border-box|inherit`

    1.参数content-box：【标准W3C盒子模型】宽度和高度分别应用到元素的内容框。在宽度和高度之外绘制元素的内边距和边框。
    2.参数border-box：【IE盒子模型】为元素指定的任何内边距和边框都将在已设定的宽度和高度内进行绘制。通过从已设定的宽度和高度分别减去边框和内边距才能得到内容的宽度和高度。
    3.参数inherit：规定应从父元素继承box-sizing属性的值。

> W3C终于承认了人家IE盒模型的合理性。通过设置box-sizing的值为border-box来模拟这一规范。

#### 7.IE6在块元素、左右浮动、设定marin时造成margin双倍

答：

**问题症状**：在IE6下如果某个标签使用了float属性，同时设置了其外边距“margin:10px 0 0 10px”可以看出，上边距和左边距同样为10px，但第一个对象距左边有20px。

**解决方法**：将其`display`属性设置为`inline`时问题就解决了。

**备注**：这个现象仅当块级对象设置了浮动属性后才会出现，内联对象（行级对象）不会出现此问题。并且只有设置左边距和右边距的值才会出问题，上下边距不会出现问题。
