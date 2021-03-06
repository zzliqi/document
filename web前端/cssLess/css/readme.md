### css 哪些属性会被继承

- 文本
  - color（颜色，a 元素除外）
  - direction（方向）
  - font（字体）
  - font-family（字体系列）
  - font-size（字体大小）
  - font-style（用于设置斜体）
  - font-variant（用于设置小型大写字母）
  - font-weight（用于设置粗体）
  - letter-spacing（字母间距）
  - line-height（行高）
  - text-align（用于设置对齐方式）
  - text-indent（用于设置首行缩进）
  - text-transform（用于修改大小写）
  - visibility（可见性）
  - white-space（用于指定如何处理空格）
  - word-spacing（字间距）
- 列表
  - list-style(列表属性)
  - list-style-image（用于为列表指定定制的标记）
  - list-style-position（用于确定列表标记的位置）
  - list-style-type（用于设置列表的标记）
- 表格
  - border-collapse（用于控制表格相邻单元格的边框是否合并为单一边框）
  - border-spacing（用于指定表格边框之间的空隙大小）
  - caption-side（用于设置表格标题的位置）
  - empty-cells（用于设置是否显示表格中的空单元格）
- 页面设置
  - orphans（用于设置当元素内部发生分页时在页面底部需要保留的最少行数）
  - page-break-inside（用于设置元素内部的分页方式）
  - widows（用于设置当元素内部发生分页时在页面顶部需要保留的最少行数）
- 其它
  - cursor（鼠标指针）
  - quotes（用于指定引号样式）

### 当规则发生冲突时

有时候多条规则会定义元素的同一属性，这时该怎么办？CSS 用层叠的原则来考虑**特殊性（specificity）**、**顺序（order）**和**重要性（importance）**，从而判断相互冲突的规则中哪个规则应该起作用。

1. 特殊性

特殊性规则指定选择器的具体程度。选择器越特殊，规则就越强。遇到冲突时，优先应用特殊性强的规则

2. 顺序

晚出现的优先级高，以下几条解释了顺序如何 决定样式规则的优先级

- 嵌入样式表（位于 style 元素内）与任何链接的外部样式表之间的关系取决于它们在 HTML 中的相对位置。在两者发生冲突时，如果 link 元素在 HTML 代码中出现的早，style 元素就会覆盖链接的样式表；如果 link 出现的晚，其中的样式及包含的任何导入样式就会覆盖 style 元素的规则
- 内联样式（直接应用于元素）在挖补央视和嵌入样式表之后。由于顺序最靠后，其优先级是最高的。一旦应用到任何地方，都会覆盖与之冲突的其它样式。
- 关于相互冲突的样式的顺序对于优先级的影响，有一种例外情况，就是标记!important 的样式总是具有最高的优先级，无论它出现在最前、最后、还是中间。不过尽量避免这种用法。

3. 重要性

如果还不够，可以声明一条特殊的规则覆盖整个系统中的规则，这条规则的重要程度比其它所有规则高。也可以在某条声明的末尾加上**!important**，比如 p{color: orange !important;}（除非特殊情况 ，否则不推荐这种用法。）

4. 小结

你编写的样式会覆盖浏览器的默认样式。当两个或两个以上的样式发生冲突时，会应用特殊性高的样式声明，不管它位于样式表中的哪个位置。如果两个或两个以上的规则拥有相同的特殊性，则使用后出现的规则，除非其中某条规则标记了 !important。

如果某元素没有指定某条规则，则使用继承的值（如果有的话）

### 伪元素、伪类及 CSS3 语法

在 CSS3 中，:first-line 的语法为::first-line，:first-letter 的语法为::firstletter。注意，它们用两个冒号代替了单个冒号。这样修改的目的是将伪元素（有四个，包括::first-line、::first-letter、::before 和::after） 与伪类（ 如:first-child、:link、:hover 等）区分开。

**伪元素（pseudo-element）**是 HTML 中并不存在的元素。例如，定义第一个字母或第一行文字时，并未在 HTML 中作相应的标记。它们是另一个元素（如：p 元素）的部分内容。

相反，**伪类（pseudo-class）**则应用于一组 HTML 元素，而你无需在 HTML 代码中用类标记它们。例如，使用:first-child 可以选择某元素的第一个子元素，你就不用写成 class="first-child"。

未来，::first-line 和::first-letter 这样的双冒号语法是推荐的方式，现代浏览器也支持它们。原始的单冒号语法则被废弃了，但浏览器出于向后兼容的目的，仍然支持它们。不过，IE9 之前的 Internet Explorer 版本均不支持双冒号。因此，你可以选择继续使用单冒号语法，除非你为 IE8 及以下版本设置了单独的 CSS（参见http://reference.sitepoint.com/css/conditionalcomments）。

### 按状态选择链接元素

链接的状态无法从代码中指定，而是由访问者控制的。伪类让你可以获取链接的状态，以改变链接在该状态下的显示效果。

- a:link 设置从未被激活或指向，当前也没有被激活或指向的链接的外观
- a:visited 设置访问者已激活过的链接的外观
- a:focus ，前提是链接通过键盘选择并已准备好激活的
- a:hover，设置光标指向链接时链接的外观
- a:active 设置激活过的链接外观

> 也可以对其它元素使用:active 和:hover 伪类。例如，设置 P:hover{color: red;}以后，鼠标停留在任何段落都会显示红色。

> 由于链接可能同事处于多种状态（如同时处于激活和鼠标停留状态），且晚出现的规则会覆盖前面出现的规则，所以一定要按照下面的属性定义规则：link、visited、focus、hover、avtive（缩写为 LVFHA）

## 使用 CSS 布局

网站设计布局主要有两大类：固定宽度和响应式（流式 fluid 或 liquid 页面，它使用百分数定义宽度，允许页面随显示环境的改变进行放大或缩小）

### 盒模型

盒模型，这里的盒子由内容区域、内容区域周围的空间（内边距，padding）、内边距的外边缘（边框，border）和边框外面将元素与相邻元素隔开的不可见区域（外边距，margin）构成：  
![1](../imgs/1.png)

关于 CSS 的 width 属性对元素所显示宽度的影响，有两种处理方式。（不包含任何将其与邻近元素隔开的外边距。）

- 默认的处理方式实际上有些有悖于常理。浏览器中元素的宽度与其 width 属性值并不一致（除非它没有内边距和边框）。CSS 中的宽度指示的是内边距里内容区域的宽度，如上图表示的那样。而元素在浏览器中的显示宽度则是内容宽度、左右内边距和左右边框的总和。显示高度与之类似，只不过计算的是上下内边距和边框值。

- 对大多数代码编写人员来说，另一种方式则更为直观。使用这种方式的话，元素的显示宽度就等于 width 属性的值。内容宽度、内边距和边框都包含在里面（如下图所示）。height 属性与之类似。要使用这种模式，仅需对元素设置 box-sizing: border-box;。

![1](../imgs/2.png)

如下例：

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <title>test</title>
    <style>
      .defaultModel,
      .boxModel {
        width: 300px;
        border: 10px solid #09a149;
        padding: 15px;
        height: 170px;
      }
      .defaultModel {
        background: brown;
      }
      .boxModel {
        box-sizing: border-box;
        background: chartreuse;
      }
    </style>
  </head>
  <body>
    <div class="defaultModel">222</div>
    <br />
    <div class="boxModel">333</div>
  </body>
</html>
```

运行结果：  
![1](../imgs/3.png)

两个 div 的 border,padding,width,height 值都相同，第一个 div 是默认盒子模型，第二个是设置了 box-sizing: border-box;的盒模型。第一个要更高更宽，这是由于上下内边距和边框尺寸增加了显示高度。

可以使用* 通配符对所有元素应用 border-box 的规则。当然，也可以单独对元素应用该规则（用你需要的选择器替换* 即可）。带有-webkit- 和-moz- 这些奇怪前缀的属性可以让这些规则在旧的 Android 和 iOS 设备上起作用，同时在 Firefox 上也能正常工作。

```css
* {
  -webkit-box-sizing: border-box;
  -moz-box-sizing: border-box;
  box-sizing: border-box;
}
```

### 元素的显示类型和可见性

1. 显示类型

每个元素在默认情况下要么显示在单独的行（如 h1-h6、p 等）这种称为块级元素，要么显示在行内（如 em、strong、cite 等）这种称为行内元素。 造成这种情况的本质是它们的 display 属性，即块级元素被设置为 display: block；对于 li 元素被设置为 diaplay:list-item，而行内元素被设置为 display:inline;

当然使用 css 可以改变元素的默认显示类型，常见属性值如：

- none 此元素不会被显示

- block 此元素显示为块级元素，此元素前后会带有换行符

- inline 默认。此元素会被显示为内联元素，此元素前后没有换行符

- inline-block 行内块元素

  - 不能为行内元素设置宽高，除非为它们设置 display:inline-block 或 display:block 属性

- list-item 此元素会作为列表显示

- inherit 规定应该从父元素继承 display 属性的值

更多属性，可在[w3c 官网](https://www.w3school.com.cn/css/pr_class_display.asp)查看

2. 可见性

visibility 属性的主要目的是控制元素是否可见。与 diaplay 不同的是，使用 visibility 隐藏元素时，元素及其内容应该出现的位置会留下一片空白区域，隐藏元素的空白区域仍然会在文档流中占据位置。

### 元素浮动

浮动的元素不会影响其父元素的高度

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <title>test</title>
    <style>
      .left,
      .right {
        width: 300px;
        height: 170px;
      }
      .left {
        float: left;
        background: brown;
      }
      .right {
        float: right;
        background: chartreuse;
      }
    </style>
  </head>
  <body>
    <div class="container">
      <div class="left">222</div>
      <div class="right">333</div>
    </div>
    <footer>footer</footer>
  </body>
</html>
```

运行效果：
![1](../imgs/4.png)

故 footer 元素显示在靠近页面顶端的位置，两列内容的父元素高度为 0

解决办法是让容器自身具有清除浮动的能力。最可靠的方法是在样式表中引入.clearfix 的规则，然后为浮动元素的父元素添加 clearfix 类

```css
.clearfix:before,
.clearfix:after {
  content: " ";
  display: table;
}
.clearfix:after {
  clear: both;
}
.clearfix {
  *zoom: 1;
}
```

如上例为 container 添加 clearfix 类后会清除浮动的 left 和 right，从而让容器的高度等于两列中较高的那个，效果图如下：

![1](../imgs/5.png)

> footer 增加 clear:both 也可解决浮动问题，但是无法影响容器的高度（容器高度仍然为 0）

> 使用 overflow 创建自清除浮动元素通常，可以对浮动元素的父元素使用 overflow 属性以替代 clearfix 方法（参见图 11.12.8 和图 11.12.9）。例如，在示例页面中可以使用以下代码：

    ```css
    .container {
      overflow: hidden;
    }
    ```
    在某些情况下，overflow: hidden; 会将内容截断，对此要多加注意。有时使用overflow: auto; 也有效，但这样做可能会出现一个滚动条，这显然是我们不希望看到的。有的代码编写人员仅在overflow 能解决float 问题的情况下才使用overflow方法，在其他情况下则使用clearfix 方法。有的代码编写人员则始终使用clearfix 方法。顺便说一下， 可以将clearfix 或overflow 应用到浮动元素的任何一个非父元素的祖先元素。这样做不会让父元素变高，但祖先元素的高度会包含浮动元素。

### 相对定位

每个元素在页面的文档流中都有一个自然位置。相对于这个原始位置对元素进行移动就称为相对定位。周围的元素完全不受此影响。

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <title>test</title>
    <style></style>
  </head>
  <body>
    <div>
      <h1>Relative Position</h1>
      <p>
        When you position an element relatively, you
        <span class="example"> position it</span> relative to its normal
        location
      </p>
    </div>
  </body>
</html>
```

展示效果：  
![1](../imgs/6.png)

如上是一个普通的段落没什么特别的，此时给 p 中 span 加个相对定位

```css
.example {
  position: relative;
  top: 35px;
  left: 100px;
}
```

展示效果：  
![1](../imgs/7.png)

偏移自然流中元素的步骤：

1. 输入 position: relative;
2. 输入 top、right、bottom、或 left。

在输入:d，这里的 d 是希望元素从它的自然位置偏移的距离，可以表示为绝对值、相对值或百分数。可正可负。

> 其他元素不会收到偏移的影响，仍然按照这个元素原来的盒子进行排序。设置了相对定位的内容可能与其他内容重叠，这取决于 top、right、bottom 和 left 的值

> 使用相对定位、绝对定位或固定定位时，对于相互重叠的元素，可以用 z-index 属性指定它们的叠放次序。

### 绝对定位

通过对元素进行绝对定位，即指定它们**相对于 body 或最近的已定位祖先元素**的精确位置，可以让元素脱离正常的文档流。

这与相对定位不同，绝对定位的元素不会在原先的位置留下空白。这与元素浮动也不同。对于绝对定位的元素，其它元素不会环绕在它的周围。事实上，其它内容不知道它的存在，它也不知道其它内容的存在。

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <title>test</title>
    <style>
      .page {
        width: 960px;
        margin: 0 auto;
      }
      .masthead .social-sites {
        position: absolute;
        top: 41px;
        right: 0;
      }
    </style>
  </head>
  <body>
    <div class="page">
      <!-- ==== START MASTHEAD ==== -->
      <header class="masthead" role="banner">
        <p class="logo">
          <a href="/"><img src="logo.png" alt="Le Journal" /></a>
        </p>

        <ul class="social-sites">
          <li><a href="http://www.facebook.com">f</a></li>
          <li><a href="http://www.twitter.com">t</a></li>
          <li><a href="http://www.flickr.com">n</a></li>
        </ul>
      </header>
    </div>
  </body>
</html>
```

通过对列表进行绝对定位，我们让它脱离文档流。仅用这段代码还不能实现目的，因为没有另外进行指定的情况下设置 position:absolate 的元素是相对 body 进行定位的，结果如下：

![1](../imgs/8.png)

对于包含列表的父元素设置 position: relative，从而让这些图标可以相对父元素（而不是 body）进行绝对定位。这样就可以让图标显示在我们希望他显示的位置

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <title>test</title>
    <style>
      .page {
        width: 960px;
        margin: 0 auto;
      }
      .masthead {
        position: relative;
      }
      .masthead .social-sites {
        position: absolute;
        top: 41px;
        right: 0;
      }
    </style>
  </head>
  <body>
    <div class="page">
      <!-- ==== START MASTHEAD ==== -->
      <header class="masthead" role="banner">
        <p class="logo">
          <a href="/"><img src="logo.png" alt="Le Journal" /></a>
        </p>

        <ul class="social-sites">
          <li><a href="http://www.facebook.com">f</a></li>
          <li><a href="http://www.twitter.com">t</a></li>
          <li><a href="http://www.flickr.com">n</a></li>
        </ul>
      </header>
    </div>
  </body>
</html>
```

效果图:  
![1](../imgs/9.png)

### 在栈中定位元素

当你开始使用相对定位、绝对定位和固定定位以后，很可能发现元素相互重叠的情况，这时可以选择哪些元素应该出现在顶层

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <title>test</title>
    <style>
      div {
        border: 1px solid #666;
        height: 125px;
        position: absolute;
        width: 200px;
      }
      .box1 {
        background: pink;
        left: 110px;
        top: 50px;
        z-index: 120;
      }
      .box2 {
        background: yellow;
        left: 0;
        top: 130px;
        z-index: 530;
      }
      .box3 {
        background: #ccc;
        position: static;
        /* 静态的，没有任何效果 */
        z-index: 1000;
      }
      .box4 {
        background: orange;
        left: 285px;
        top: 65px;
        z-index: 3;
      }
    </style>
  </head>
  <body>
    <div>
      <div class="box1"><p>Box 1</p></div>
      <div class="box2"><p>Box 2</p></div>
      <div class="box3"><p>Box 3</p></div>
      <div class="box4"><p>Box 4</p></div>
    </div>
  </body>
</html>
```

运行效果:  
![1](../imgs/10.png)

对于定位元素，z-index 最高的数显示在最上面，不管该元素在 HTML 中出现的次序。第一条规则为所有四个 div 设置了 position:absolute;而定义.box3 时又覆盖了这一规则，让.box3 回到默认的 static。因此， 尽管它的 z-index 值最高，但这没有任何效果，它总是位于最底层(因为它处于常规文档流)

> z-index 属性仅对定位过的元素（即设为绝对定位、相对定位或固定定位的元素）有效。上例中仅包含绝对定位的元素，但实际上可以对绝对定位、相对定位和固定定位的元素混合使用 z-index，z-index 会将它们作为整体进行安排，而不是分别安排。

### 设置字体大小

案例：

```css
body {
  font-family: Geneva, Tahoma, Verdana, sans-serif;
  font-size: 100%; /* 16px */
}
h1,
h2 {
  font-family: "Gill Sans", "Gill Sans MT", Calibri, sans-serif;
  font-weight: normal;
}
h1 {
  font-size: 2.1875em; /* 35px/16px */
}
h2 {
  font-size: 1.75em; /* 28px/16px */
}
em,
a:link,
.intro .subhead {
  font-weight: bold;
}
.intro .subhead {
  font-size: 1.125em; /* 18px/16px */
}
.intro p {
  font-size: 1.0625em; /* 17px/16px */
}
.project p {
  font-size: 0.9375em; /* 15px/16px */
}
```

body 里的 font-size: 100% 声明为 em 字体大小设置了参考的基准。这里的 100% 将被翻译为默认字体大小（大多数系统下为 16px）。每个 font-size 属性值后面的注释解释了该值的计算方法，同时显示了等价的像素值

1em 总是等于默认的字号大小，这是 em 的工作原理。在这里，1em 就等于 16px，因为我们将其创建为元素的默认字号。据此可以通过一点点除法确定 em 值（或百分比）

```
要指定的字体大小／父元素的字体大小＝值

但需要记住的是，em该值应该是相对于这些元素的父元素的
```

```
使用rem 设置字体大小

CSS3 引入了一些新的单位，其中很有意思的一个便是rem（root em 的简称）。它同em 很像，不过它总是以根元素为参照系设置其他元素的字体大小，而不是父元素。根元素是html 元素（因为它包含body，也就包含了所有内容）


这样做简化了字体大小的设置，因为html 的字体大小通常不会变，不像父元素的大小是不确定的，就像在段落中设置链接字体大小的例子那样因此，我们的公式（在前面公式的基础上调整而来）为：

要指定的字体大小／根元素字体大小＝值

实际上就是

要指定的字体大小／ 16 ＝值

虽然现代浏览器对它的支持程度很高，但Internet Explorer 直到IE9 才开始支持它，这也
是很多代码编写人员尚未使用rem 的原因
```
