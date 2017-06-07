![BiliPala....](http://upload-images.jianshu.io/upload_images/4007920-0b5fef175885bc45.jpeg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

> #### 浮动元素的特征，对父容器、对其他浮动元素、普通元素、文字的影响。

- 浮动会使应用的元素脱离文档流。按指定的位置来移动位置。当遇到其父元素或者相邻的元素时即停下。此样式可用于 块级元素 或 行内元素。
- 使用`float`浮动样式的行内元素，会跟使用`inline-block`样式一样可以设置宽高.

![float 样式版已经脱离文档流，能看到黄色父元素背景是因为添加了overflow..](http://upload-images.jianshu.io/upload_images/4007920-17749d1605cc7090.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

- 默认撑开文本内容的高度。（没内容的话就显示空白..不过只设置宽高背景色可以看到轮廓的。）

- 脱离了文档流，那就意味着父元素无法感知到有该元素，那么即显示没有内容时的默认宽高（除非设置固定宽高 | 样式）。
![float 会把元素挤到最前...](http://upload-images.jianshu.io/upload_images/4007920-29e97e0c5f4abcb2.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

- 浮动后，会置顶，文字会环绕...

![看图...](http://upload-images.jianshu.io/upload_images/4007920-4bfdf6869da55a3d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)





---

> ####  清除浮动 & 清除浮动：

- 清除浮动不是不要浮动，而是清除浮动带来的不利影响。另外，结合clear属性也可让父元素在视觉上包围浮动元素。

- 至于清除浮动：
 - 在父元素的子元素最后添加一个空div，并对其设置样式：clear:both;
由于在子元素最后添加了空div，并清除了浮动，因此父容器被撑开，实现了在视觉上包围浮动元素的效果。（略显浪费..）

 - 利用BFC（后有介绍）来清除浮动：
因为BFC可以包含浮动，因此可以让父元素生成一个新的BFC从而包围浮动的子元素。
可以对父元素设定以下样式之一生成新BFC。
<pre>
`float: left | right;`
`overflow: hidden | auto | scroll;`
`display: table-cell | table-caption | inline-block;`
`position: absolute | fixed;`
</pre>

 - 结合CSS特性的通用清除浮动方案，其本质还是第1种方法（通用）。
<pre>
```.clearfix {
      *zoom: 1;
   } 
                                     <!-- 隔行是总美 -->
.clearfix:after {
      content: "";
      display: block;
      clear: both;
}```</pre>






---
> #### 几种定位方式，如何实现定位，参考点，使用场景：

- inherit：从父元素继承；
- static：默认值，没有定位，元素出现在正常的文档流中。参考点是文档流中的位置。
- relative：相对定位。相对于元素本来的位置进行定位，通过top、bottom、left、right属性来设置偏移量。使用场景：为绝对定位设定参照物或对元素自身位置进行局部调整。
- absolute：绝对定位的元素的位置是相对于距离最近的非static祖先元素位置决定的。如果元素没有已定位的祖先元素，那么他的位置就相对于初始包含块html来定位。使用场景：当想让元素参照特定参照物进行定位时使用。
- fixed：固定定位。生成绝对定位元素，相对于屏幕窗口（viewport）进行定位。
- sticky：对象在常态时遵循普通流。它就像是relative和fixed的合体，当在屏幕中时按常规流排版，当卷动到屏幕外时则表现如fixed。（CSS3 产物。兼容性现在好多了...）

![Sticky兼容性](http://upload-images.jianshu.io/upload_images/4007920-f4ea0215c143bcdc.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


---

>  #### z-index 作用 & 使用.


因为绝对定位的元素脱离了普通流，所以绝对定位的元素可以覆盖页面上的其它元素。这时可以通过给元素设置z-index属性来控制叠放顺序，该属性值越高，元素位置越靠上。



![实操最要紧](http://upload-images.jianshu.io/upload_images/4007920-d47dca79691a233e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)



---
> #### position:relative 和 负margin 可以使元素位置发生偏移，区别：





- `position:relative;` 只相对自己原本位置发生偏移，不影响其它普通流中元素的位置。
- `margin ` 除了让元素自身发生偏移还影响其它普通流中的元素。


![margin后面的元素也会跟进...](http://upload-images.jianshu.io/upload_images/4007920-22808ee3d45f0b08.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)



---
> #### BFC （Block formatting contexts）

- [w3c规范中的BFC定义](http://www.w3.org/TR/CSS2/visuren.html#block-formatting)：
浮动元素和绝对定位元素，非块级盒子的块级容器（例如 inline-blocks, table-cells, 和 table-captions），以及overflow值不为“visiable”的块级盒子，都会为他们的内容创建新的BFC（块级格式上下文）。
在BFC中，盒子从顶端开始垂直地一个接一个地排列，两个盒子之间的垂直的间隙是由他们的margin 值所决定的。在一个BFC中，两个相邻的块级盒子的垂直外边距会产生折叠。
在BFC中，每一个盒子的左外边缘（margin-left）会触碰到容器的左边缘(border-left)（对于从右到左的格式来说，则触碰到右边缘）。

- BFC的通俗理解：
首先BFC是一个名词，是一个独立的布局环境，我们可以理解为一个箱子（实际上是看不见摸不着的），箱子里面物品的摆放是不受外界的影响的。转换为BFC的理解则是：BFC中的元素的布局是不受外界的影响（我们往往利用这个特性来消除浮动元素对其非浮动的兄弟元素和其子元素带来的影响。）并且在一个BFC中，块盒与行盒（行盒由一行中所有的内联元素所组成）都会垂直的沿着其父元素的边框排列。

##### 添加创建：
- 浮动，绝对定位元素，inline-blocks, table-cells, table-captions,和overflow的值不为visible的元素，（除了这个值已经被传到了视口的时候）将创建一个新的块级格式化上下文

- 上面的引述几乎总结了一个**BFC**是怎样形成的。但是让我们以另一种方式来重新定义以便能更好的去理解。一个BFC是一个HTML盒子并且至少满足下列条件中的任何一个：
 - `float`的值不为none.
 - `position`的值不为static或者relative.
 - `display`的值为 `table-cell`, `table-caption`,` inline-block`, 或者 `inline-flex`中的其中一个.
 - `overflow`的值不为visible.

- 一个BFC可以被显式的触发。如果想要创建一个新的BFC，只需要给它添加上面提到的任何一个CSS样式就可以了。

- 一个新的BFC可以通过给容器添加任何一个触发BFC的CSS样式，如overflow: scroll, overflow: hidden, display: flex, float: left,或者 display: table来创建。

 - display:table可能会产生一些问题
 - overflow:scroll可能会显示不必要的滚动条
 - float:left将会把元素置于容器的左边，其他元素环绕着它
 - overflow:hidden将会剪切掉溢出的元素

- 所以每当想要创建一个新的BFC的时候，我们会基于我们的需求选择最好的样式条件。

#####运用场景：

- 假设，一个 div容器 它设置了浮动...那么此时它的父元素是不会有任何高度的，它将不会去包含已经浮动的子元素，那么此时可以通过给其添加一个 `overflow：hidden`，在容器中创建一个新的BFC。那么这个将包含浮动的子元素，它的高度可扩展到可以包含它的子元素，**这些元素会回到页面的常规文档流。**

- 有时候一个浮动div周围的文字环绕着它（如下图中的左图所示）但是在某些案例中这并不是可取的，我们想要的是外观跟下图中的右图一样的。为了解决这个问题，我们可能使用外边距，但是我们也可以使用一个BFC来解决。

![image.png](http://upload-images.jianshu.io/upload_images/4007920-453472f67f3766f8.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)



- 还可以在多列布局中使用BFC
如果我们正在创建的一个多列布局占满了整个容器的宽度，在某些浏览器中最后一列有时候将会被挤到下一行。会发生这样可能是因为浏览器舍入（取整）了列的宽度使得总和的宽度超过了容器的宽度。然而，如果我们在一个列的布局中建立了一个新的BFC，它将会在前一列填充完之后的后面占据所剩余的空间。



----

>  #### 在什么场景下会出现外边距合并（折叠）？如何合并？如何不让相邻元素外边距合并？给个父子外边距合并的范例

- 合并外边距与BFC
在CSS当中，相邻的两个盒子（可能是兄弟关系也可能是祖先关系）的外边距可以结合成一个单独的外边距。这种合并外边距的方式被称为折叠，并且因而所结合成的外边距称为折叠外边距。

- 折叠的结果：
两个相邻的外边距都是正数时，折叠结果是它们两者之间较大的值。
两个相邻的外边距都是负数时，折叠结果是两者绝对值的较大值。
两个外边距一正一负时，折叠结果是两者的相加的和。

- 产生折叠的必备条件：margin必须是邻接的!
而根据w3c规范，两个margin是邻接的必须满足以下条件：
 - 必须是处于常规文档流（非float和绝对定位）的[块级盒子](http://www.w3.org/TR/CSS2/visuren.html#block-boxes),并且处于同一个[BFC](http://www.w3.org/TR/CSS2/visuren.html#block-formatting)当中。
 - 没有线盒，没有空隙（[clearance](http://www.w3.org/TR/CSS2/visuren.html#clearance)），没有padding和border将他们分隔开
 - 都属于垂直方向上相邻的外边距，可以是下面任意一种情况元素的margin-top与其第一个常规文档流的子元素的margin-top
 - 元素的margin-bottom与其下一个常规文档流的兄弟元素的margin-top
 - height为auto的元素的margin-bottom与其最后一个常规文档流的子元素的margin-bottom
 - 高度为0并且最小高度也为0，不包含常规文档流的子元素，并且自身没有建立新的BFC的元素的margin-top和margin-bottom


- 以上的条件意味着下列的规则：
 - 创建了新的BFC的元素（例如浮动元素或者'overflow'值为'visible'以外的元素）与它的子元素的外边距不会折叠
 - [浮动](http://www.w3.org/TR/CSS2/visuren.html#floats)元素不与任何元素的外边距产生折叠（包括其父元素和子元素）
 - 绝对定位元素不与任何元素的外边距产生折叠
 - inline-block元素不与任何元素的外边距产生折叠
 - 一个常规文档流元素的margin-bottom与它下一个常规文档流的兄弟元素的margin-top会产生折叠，除非它们之间存在间隙（clearance）。
 - 一个常规文档流元素的margin-top 与其第一个常规文档流的子元素的margin-top产生折叠，条件为父元素不包含 padding 和 border ，子元素不包含 clearance。
 - 一个 'height' 为 'auto' 并且 'min-height' 为 '0'的常规文档流元素的 margin-bottom 会与其最后一个常规文档流子元素的 margin-bottom 折叠，条件为父元素不包含 padding 和 border ，子元素的 margin-bottom 不与包含 clearance 的 margin-top 折叠。
 - 一个不包含border-top、border-bottom、padding-top、padding-bottom的常规文档流元素，并且其 'height' 为 0 或 'auto'， 'min-height' 为 '0'，其里面也不包含行盒(line box)，其自身的 margin-top 和 margin-bottom 会折叠。


![](http://upload-images.jianshu.io/upload_images/4007920-8366d3ce1e6890cb.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

- 浮动和绝对定位不与任何元素产生 margin 折叠

- inline-block元素与其兄弟元素、子元素和父元素的外边距都不会折叠（包括其父元素和子元素）

![](http://upload-images.jianshu.io/upload_images/4007920-f79be14768045df8.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![](http://upload-images.jianshu.io/upload_images/4007920-c3fa16c5229cc086.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

----
**参考传送门:** [🍼](http://www.w3cplus.com/css/understanding-bfc-and-margin-collapse.html)
**参考传送门: **[😱](http://www.w3cplus.com/css/understanding-block-formatting-contexts-in-css.html) 

---
