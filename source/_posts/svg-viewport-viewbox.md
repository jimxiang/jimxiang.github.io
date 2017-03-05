title: svg_viewport&viewbox
date: 2017-03-04 22:27:04
tags: svg | viewport | view box 
---
学习svg，除了掌握基本的图形元素，更要清楚svg元素的大小与svg内部图形大小的关系，svg图像的 viewport 和 view box 共同设置了图像可见部分的尺寸。现在我们一起学习下 viewport 和 view box 的知识，也许清不清楚这些知识对svg元素的使用不会产生多大的影响，但涉及到复杂图形的时候，了解这些知识会有助于我们更快速、更精准的控制元素，并且减轻维护成本。

### 1. The Viewport and View Box
**viewport** 是创建svg元素时给它设置的 width 和 height，决定了svg图像的可视区域。逻辑上svg图像可以无限大，但每次只有特定的区域是可视的，这个可视区域就是 viewport。你可以通过svg元素的 width 和 height 属性来指定 viewport 的大小：如

```html
<svg width="500" height="300"></svg>
```
这个例子定义了一个宽500单位、高300单位的viewport。   

**view box** 是 svg的一个属性，设置了内部图形的坐标系大小。   

更直观的解释是：viewport 就像是显示器，有固定的宽高，你只能在显示器屏幕的范围内观看影像，view box 设置了显示器里的影像通过何种比例显示出来。就像你看到一个大海，它也许只占了显示器里大小的1/4，但它实际的大小却是显示器的n倍。viewport 和 view box 指定了两个坐标系，内部的图形会根据这两个坐标系做适当的缩放来适应性的显示出来。

### 2. svg坐标系单位
如果你没有指定 width 和 height 属性的单位，那么单位会被默认为 px。你还可以使用 px 以外的单位，

| 单位 | 描述 |
| - | - |
| em | 相对单位：相对于父元素字体大小 |
| ex | 相对单位：相对于字符 x 的高度(很少使用) |
| px | 绝对单位，但相对于设备分辨率：像素 |
| pt | 绝对单位：点(1／72英寸) |
| pc | 绝对单位：(1／6英寸) |
| cm | 绝对单位：厘米 |
| mm | 绝对单位：毫米 |
| in | 绝对单位：英寸 |

给svg元素设置的单位只会影响svg元素的大小(viewport)。svg图像里显示的svg图形元素的大小取决于你给每个图形设置的单位。如果没有指定单位，默认使用 px。

下面展示一个svg元素与svg图像里的图形设置不同单位的例子：

```html
<svg width="10cm" height="10cm">
    <rect x="50" y="100" width="50" height="50" style="stroke: #000000; fill: none;"></rect>
    <rect x="100" y="100" width="50mm" height="50mm" style="stroke: #000000; fill: none;"></rect>
</svg>
```

svg图像单单位是cm，两个rect元素有自己的单位：第一个没有指明单位，默认px；第二个使用了mm。结果如下：

![pic_1](http://o7bp9e1ec.bkt.clouddn.com/1488696584964)

### 3. The View Box
你可以通过 viewBox 属性重新定义没有单位的坐标。注：view box属性不要带单位。

```html
<svg width="500" height="200" viewBox="0 0 50 20">
    <rect x="20" y="10" width="10" height="5" style="stroke: #000000; fill: none;"></rect>
</svg>
```

这个例子中我们创建了一个宽500px高200px的svg元素。viewBox属性有四个值 x y width height，这些值定义了svg元素的视区，x 和 y是视区的左上角坐标，width 和 height是视区的宽高。在这个例子中，视区从(0, 0)开始，宽高分别是50和20，这意味着宽500px、高200px的svg元素在内部使用的坐标系是从(0, 0)开始，到(50, 20)。换句话说，svg元素内部坐标系中的1单位相当于宽度500/50=10px、高度200/20=10px。这就是为什么x轴偏移20单位、y轴偏移10单位的矩形实际位置却是偏移到了(200px, 100px)处。因为内部坐标系中1单位相当于10px。

结果为：

![pic_2](http://o7bp9e1ec.bkt.clouddn.com/1488691161226)

### 4. Preserving Aspect Ratio
如果 viewport 和 view box 没有使用相同的长宽比(repect ratio)，你需要指定浏览器如何显示svg图像，这时你需要svg元素的preserveAspectRatio属性。   

preserveAspectRatio属性由两个被空格分隔的值组成。第一个值设置view box在viewport中如何对齐，这个值由两部分组成；第二个值设置如何保留长宽比（如果需要的话）。   

第一个值由两部分组成：x轴的对其方式和y轴的对齐方式，下面是这两个值的列表：

| 值 | 描述 |
|-|-|
| xMin | 将 view box 和 viewport 左边对齐 |
| xMid | 将 view box 和 viewport x轴中心对齐 |
| xMax | 将 view box 和 viewport 右边对齐 |
| yMin | 将 view box 和 viewport 上边对齐 |
| yMid | 将 view box 和 viewport y轴中心对齐 |
| yMax | 将 view box 和 viewport 下边对齐 |

这两个部分可以通过驼峰命名的方式组合起来：xMinYMin。   

第二个值有三个值：

| 值 | 描述 |
|-|-|
| meet | 保留长宽比并缩放 view box 以适应 viewport |
| slice | 保留长宽比并把超出 viewport 的部分裁剪掉 |
| none | 不保留长宽比，缩放图像以将 view box 完全置入 viewport。长宽比被破坏 |

这两个值之间需要有一个空格：
```
preserveAspectRatio="xMidYMid meet"
preserveAspectRatio="xMinYMin slice"
```

接下来我们来看看不同的 preserveAspectRatio 属性值带来的效果。
##### (1).
```html
<svg width="500" height="75" viewBox="0 0 250 75" style="border: 1px solid #cccccc;">
    <rect x="1" y="1" width="50" height="50" style="stroke: #000000; fill: none;"</rect>
</svg>
```
![pic_3](http://o7bp9e1ec.bkt.clouddn.com/1488693398271)

这种不设置 preserveAspectRatio 的情况与 xMidYMid meet 的效果相同，由此可推测浏览器会默认让图像以最合适、最舒服的方式显示出来。

##### (2).
```html
<svg width="500" height="75" viewBox="0 0 250 75" preserveAspectRatio="xMinYMin meet" style="border: 1px solid #cccccc;">
    <rect x="1" y="1" width="50" height="50" style="stroke: #000000; fill: none;"</rect>
</svg>
```
![pic_4](http://o7bp9e1ec.bkt.clouddn.com/1488693927989)
这个例子中设置了 preserveAspectRatio 为 xMinYMin meet，这会确保长宽比是保留了的，view box 会调整大小来适应 viewport。所以，view box 根据两个长宽比中(500/250=2, 75/75=1)较小的比例进行缩放(width: 50\*1=50, height: 50\*1=50)，xMinYMin 使图形左上对齐。

##### (3).
```html
<svg width="500" height="75" viewBox="0 0 250 75" preserveAspectRatio="xMinYMin slice" style="border: 1px solid #cccccc;">
    <rect x="1" y="1" width="50" height="50" style="stroke: #000000; fill: none;"></rect>
</svg>
```
![pic_5](http://o7bp9e1ec.bkt.clouddn.com/1488694387507)
这个例子中设置了 preserveAspectRatio 为 xMinYMin slice，同样保留了长宽比，但 view box 根据两个比例中(500/250=2, 75/75=1)较大的比例进行缩放(width: 50\*2=100, height: 50\*2=100)，结果超过了 viewport 的大小，所以 slice 掉超出的部分。

##### (4).
```html
<svg width="500" height="75" viewBox="0 0 250 75" preserveAspectRatio="none" style="border: 1px solid #cccccc;">
    <rect x="1" y="1" width="50" height="50" style="stroke: #000000; fill:none;"></rect>
</svg>
```
![pic_6](http://o7bp9e1ec.bkt.clouddn.com/1488694788943)
这个例子中设置了 preserveAspectRatio 为 none，view box 将会填满整个 viewport，从而使图像失真，因为x轴和y轴的长宽比不同(x轴 2:1，y轴 1:1)。