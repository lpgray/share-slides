title: 前端组件化之路
speaker: 张杨
url: lpgray.vipsinaapp.com
files: /css/theme.txbb.css


[slide]
<img src="/logo.png" style="width:128px;margin-bottom:30px;"/>
# 前端组件化之路
张杨 @ 同学帮帮

<p style="font-size: 20px;margin-top: 50px;">
www.txbb.com
</p>

[slide]
# 分享目标
1. 业务模块化
2. 代码结构化
3. 模块的压缩
4. 一些第三方的框架介绍


[slide]
# 什么是组件化？

[slide]
能够解决通用问题的模块，可以是UI型的，也可以是逻辑型的。对于前端，最常见的组件化类库就是Bootstrap，它包含的Button, Dropdown, Modal等组件可以很方便的应用到不同的业务中。

[slide]
# 为什么要做组件化？

[slide]
就是“偷懒”，来个新页面，“啪”一套；来个新项目，也是“啪”一套。功能棒棒哒，任务完成，老婆再也不用担心我加班晚归啦！

[slide]
# 其实就是 <br> Don't Repeat Yourself

[slide]
# 一、业务模块化

[slide]
## 任何公司的任何互联网产品，都可以划分业务模块

[slide]
## 业务模块
![业务模块](/1-1.png)

[slide]
# 业务模块化的好处
专注维护专门的业务模块，业务模块之间很少会耦合，除非十分通用的库，否则不会有任何联系，这样的好处不言自明，永远不会混乱，而且非常利于团队管理。

[slide]
## 前端代码中的业务模块
![](/1-2.png)

[slide]
# 具备组件化的编码思维

[slide]
# 一个组件化思维编码的例子

[slide]
![](/1-3.png)
![](/1-4.png)

[slide]

React有组件化的天然优势，在React的世界中，万事万物皆组件。

[slide]
# 二、代码的结构化


[slide]
# 如何在项目开发初期需求不明确的情况下就开始着手组件化？

[slide]
# 1. 更细粒度的代码结构
每个业务模块都由不同的页面组成，而不同的页面又是由组件组成。

**组件可以认为是最细粒度的代码**

[slide]
# 2. 抓住通用需求
极其通用的需求，用常规的第三方类库完全可以解决。不过在资源丰富的大型企业中，他们还是喜欢自己去造轮子。
比如：图片轮播、提示层、列表菜单、Alert、Confirm ……

**不推荐极其通用的需求再重造一遍轮子**

[slide]
# 3.代码约束
你要形成自己的代码书写规律，或者说规范，如果团队有团队规范，就应该遵循团队规范，社区遵循社区规范，这才是一个合格的开发者。

**组件化的代码，一定是有规可循的代码结构，而前端代码最容易乱**

[slide]
# 4.前端组件包含哪些？
UI、JS逻辑、带有后端数据交互的模块？都是，那么再落地一些，一个前端组件，很有可能是以下组合：
- DOM+CSS
- DOM+CSS+JS
- JS

[slide]
# HTML结构化
可以把你的应用的页面想象成是由一个个HTML片段组合而成的结构。

[slide]
![](/1-5.png)

<small>图片来自 [div.io](http://div.io?from=zy)</small>

[slide]
```html
<div class=”page”>
    <header class=”header”></header>
    <div class=”body”></header>
    <footer class=”footer”></footer>
    ......
</div>
```

[slide]
# 以DOM类名做命名空间
header只服务于一个业务，当另一个业务突然冒出了通用需求，你可以直接将header改为comm-header，因为此时已经有两个业务方向使用了同一个组件，此时你已经完成了**抽象**的第一步了。

[slide]
> 前端的复杂之处就是对于UI的交互逻辑难以进行抽象化。

<br>
—— 前端开发之痛

[slide]
# CSS结构化
刚刚我们定义的每一个DOM的最外层的classname做为命名空间，然后你可以在命名空间下，随意使用其他的类名。

对于这种情况，推荐使用Sass, Less等预编译。

[slide]
```css
.comm-header {
    .title {}  /* ...... */
}
.mod-body{
    .title {}  /* ...... */
}
.comm-footer{
    .title {}  /* ...... */
}
```
以上是 Less 代码

以「comm-」开头的为通用模块，以「mod-」开头的为非通用模块，这是我目前定的规则。

[slide]

也许这只是一个以DOM的类名作为命名空间的编码习惯。

[slide]

Talking is Cheap,

Show me the code

[slide]

![](/2-1.png)
<img src="/2-2.png" style="position: absolute;top: -10px;right: -50px;width: 500px;"/>

[slide]
# JS编写的两种形态

1. 模板动态生成
2. 模板直接存在

[slide]
不讨论JS编写细节，你可以用任何前端库。

[slide]
# 组件，不一定非得有JS

小到一个 Button，大到一个发送手机密码的业务逻辑，都可以认为是一个组件。

[slide]
# 代码的压缩

[slide]
可以在初期针对每一个业务模块分别压缩。
<img src="/1-2.png" style="width: 400px;"/>

[slide]
工具

<img src="/2-3.png" style="border: none;"/>

[slide]
# 三、组件库的形成

[slide]
![](/3-1.png)

[slide]
# 三大方向

纯样式、工具类、交互

[slide]
# 简单定义一下
以DOM的类名作为命名空间的组件，HTML以特定的类名作为片段根节点，然后子节点随便你怎么折腾，此为**封装**。而后，以**根节点的类名为命名空间去写样式**，最后你的**页面是由HTML片段组合而成**，随着业务的发展，你会**不断重构你的HTML片段及CSS样式**，然后达到**逐渐抽象**的目的，最后是你的JS，某段JS会服务特定的HTML／CSS片段，他们的组合可以认为是组件。

[slide]
# 四、组件的设计

[slide]
# 组件API设计
- Classname的命名规范
- HTML元素的data-attribute的使用
- JS的面向对象设计

[slide]
# JS的面向对象设计
- 设计默认参数
- 设计回调方法
- 设计实例方法
- 设计静态方法

[slide]
# 默认参数
todo

[slide]
# 回调方法
todo

[slide]
# 实例方法
todo

[slide]
# 静态方法
todo

[slide]
![](/4-1.png)

[slide]
如何进行事件绑定，到底是用传统的绑定形式呢，还是使用第三方的双向绑定类库，这些都随开发者自己折腾，只要对外暴露的API经久不衰，我们就达到目的了。

[slide]
自此，我的组件化之路就介绍的差不多了，<strong>带有命名空间的HTML片段与CSS，JS来做支持</strong>。

[slide]
```html
<div class=”page”>
   <div class=”header”></div>
</div>
```
```css
.page .header {
   position:fixed;
}
```
```javascript
$(’.page’).on(’hover’,function(){
});
```

[slide]
![](/4-2.png)
<small>图片来自 [div.io](http://div.io?from=zy)</small>

[slide]
![](/4-3.png)
<br>
眼熟

[slide]
# Web Components

[slide]
# Web Component
- Shadow DOM
- HTML Imports
- Custom Element
- Template

[slide]
# 算不算一次革命？
HTML/CSS/JS vs HTML Imports

[slide]
回头看看咱们的代码的结构，跟Polymer很像
![](/4-4.png)

[slide]
> 应用是由页面组成，页面是由组件组成。

——组件化思维

[slide]
# 五、使用组件化类库

[slide]
# 组件化类库
- Polymer
- React
- Angular 2

[slide]
# 总结

[slide]
带有命名空间的HTML/CSS/JS组件化编码方式
<br>
一个面向未来的组件化代码书写方式

[slide]
Thanks
