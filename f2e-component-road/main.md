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
4. 组件化类库介绍


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
# 一、业务的模块化

[slide]
## 任何公司的任何互联网产品，都可以划分业务模块

[slide]
## 一些通用的业务模块
![业务模块](/1-1.png)

[slide]
# 业务模块化的好处
专人维护专门的业务模块，业务模块之间很少会耦合，除非十分通用的库，否则不会有任何联系，这样的好处不言自明，永远不会混乱，而且非常利于团队管理。

[slide]
## 同学帮帮前端代码的业务模块
![](/1-2.png)

[slide]
# 我们应当具备组件化的编码思维
组件化的编码思维，就是在进行前端开发时，要**随时准备抽象**。

[slide]
# 如何在项目开发初期需求不明确的情况下就开始着手组件化？

[slide]
# 例子：一个组件化思维编码的例子

[slide]
![](/1-3.png)
![](/1-4.png)

弹出选项组件

[slide]
```javascript
var Selection = React.createClass({
    return {
        var isSingle = this.props.isSingle;
        render: function(){
            <div className="comm-selection">
                // ......
            </div>
        }
    }
})
```

[slide]
# 二、代码的结构化

[slide]
## 1. 写代码之前，先抓通用需求
极其通用的需求，用常规的第三方类库完全可以解决。不过在资源丰富的大型企业中，他们还是喜欢自己去造轮子。
比如：图片轮播、提示层、列表菜单、Alert、Confirm ……

**不推荐极其通用的需求再重造一遍轮子**

[slide]
## 2. 业务之后再规划代码结构
每个业务模块都由不同的页面组成，而不同的页面又是由组件组成。

**组件可以认为是最细粒度的代码结构**

[slide]
## 3.前端组件包含哪些代码结构？
UI、JS逻辑、带有后端数据交互的模块？都可以认为是一个前端组件，那么再落地一些，一个前端组件，很有可能是以下组合：
- DOM+CSS
- DOM+CSS+JS
- JS

[slide]
# 1. HTML结构化
可以把你的应用的页面想象成是由一个个HTML片段组合而成的结构。

[slide]
![](/1-5.png)

<small>图片来自 [div.io](http://div.io?from=zy)</small>

[slide]
那么以下的一个HTML结构，就组成了一个页面：

```html
<div class=”page”>
    <header class=”header”></header>
    <div class=”body”></header>
    <footer class=”footer”></footer>
    ......
</div>
```

[slide]
# 2. 以DOM类名做命名空间

比如，header只服务于一个业务，当另一个业务突然冒出了通用需求，你可以直接将header改为comm-header，因为此时已经有两个业务方向使用了同一个组件，此时你已经完成了**抽象**的第一步了。

[slide]
> 前端的复杂之处就是对于UI的交互逻辑难以进行抽象化。

<br>
—— 前端开发之痛

[slide]
# 3. CSS结构化
刚刚我们定义的每一个DOM的最外层的class做为命名空间，然后你可以在命名空间下，随意使用其他的类名，而不用担心冲突，你只需要维护**组件类名**就可以了。


[slide]
对于刚刚那种以class为命名空间的形式编写样式，我推荐使用Sass, Less等预编译：

```css
.comm-header {
    .title {}  /* ...... */
    .body {}
    .footer {}
}
```

以上是 Less 代码

[slide]

也许这只是一个以DOM的类名作为命名空间的编码习惯。

[slide]

Talking is Cheap,

Show me the code

[slide]

![](/2-1.png)
<img src="/2-2.png" style="position: absolute;top: -10px;right: -50px;width: 500px;"/>

[slide]
# 4. JS无非就两种形态

1. 模板直接存在
2. 模板动态生成

[slide]
# 模板直接存在

HTML / CSS写好之后，再写对应的JS的形态属于模板直接存在的形态，大部分的Web站点都是此种形态，我们中规中矩的去写以下这种工程结构:
```
- project
  - styles
  - scripts
  - images
  - html
```

[slide]
模板动态生成的形态，可以使用第三方模板类库:

```html
<script id="entry-template" type="text/x-handlebars-template">
  <div class="entry">
    <h1>{{title}}</h1>
    <div class="body">
      {{body}}
    </div>
  </div>
</script>
```

[slide]
简单一些的也可以直接在JS中拼字符串:

```javascript
var tmpl = '<div>';
tmpl += ' <p>Hello World</p>'
tmpl += '</div>';
```

[slide]
当然现在ES6也支持了Template特性:

```javascript
var name = 'World';
console.debug(`Hello, ${name}!`);

// Hello, World!
```

[slide]
前端的组件，无非就是 HTML / CSS / JS 的三者结合。

[slide]
今天，不讨论JS编写细节，你可以用任何前端库，无论是 jQuery也好，抑或 React、Angular等。

[slide]
# 组件，不一定非得有JS

小到一个 Button，大到一个发送手机密码的业务逻辑，都可以认为是一个组件，我们要做的就是**不断提炼和封装**。

[slide]
# 三、组件库的形成

[slide]
# 三大方向
纯样式、工具类、交互
![](/3-1.png)

[slide]
# 简单定义一下
以DOM的类名作为命名空间的组件，HTML以特定的类名作为片段根节点，然后子节点随便你怎么折腾，此为**封装**。而后，以**根节点的类名为命名空间去写样式**，最后你的**页面是由HTML片段组合而成**，随着业务的发展，你会**不断重构你的HTML片段及CSS样式**，然后达到**逐渐抽象**的目的，最后是你的JS，某段JS会服务特定的HTML／CSS片段，他们的组合可以认为是组件。

[slide]
# 四、如何设计组件？

[slide]
# 组件设计
1. 定义你的命名空间，编写表现层（HTML/CSS）

2. API设计（JS）

[slide]
# JS的API设计
- 设计回调方法
- 设计默认参数

[slide]
# 回调方法
当你设计组件的时候，首先应该考虑的是，组件的职能。
比如，选择一个日期，组件会返回一个日期字符串:
```javascript
Txbb.DatePicker({
    onDateReceived : function(date) {}
})
```
比如，在地图上选择一个位置，组件返回此位置周边的餐馆：
```javascript
Txbb.LocationSearch({
    onResturantsReceived : function(resturants) {}
})
```

[slide]
# 默认参数
默认参数的设计很重要，容错，空对象、空函数，“空”甚至都是一种设计模式

[slide]
我们的一个API示例

![](/4-1.png)

[slide]
自此，我的组件化之路就介绍的差不多了，<strong>带有命名空间的HTML片段与CSS，然后JS专门进行针对开发</strong>。

[slide]
# 组件化的代码结构

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
# 代码的组织形式

过去的代码：
```shell
- app
    - scripts
    - images
    - html
    - style
```
现在的代码：
```shell
- app
    - user-center
        - header
           - header.css
           - header.js
        - footer
    - activity
        - header
            - header.css
            - header.js
        - footer
    - common
        - header
            - header.css
            - header.js
        - footer
```


[slide]
# 代码的新形式

![](/4-2.png)
<small>图片来自 [div.io](http://div.io?from=zy)</small>

[slide]
![](/4-3.png)
<br>
眼熟

[slide]
# Web Components

新一代Web前端开发标准

[slide]
# Web Components
- Shadow DOM
- **HTML Imports**
- Custom Element
- Template

[slide]
# 算不算一次革命？
**HTML/CSS/JS** vs **HTML Imports**

[slide]
回头看看咱们的代码的结构
![](/4-4.png)

[slide]
> 应用是由页面组成，页面是由组件组成。

——组件化思维


[slide]
# 五. 代码的构建

[slide]
可以在初期分别对每一个业务模块分别压缩。
<img src="/1-2.png" style="width: 500px;"/>

[slide]
# 工具
<img src="/2-3.png" style="border: none;"/>

[slide]
# 使用gulp构建的示例
![](/5-1.png)

[slide]
# 六、使用组件化类库

[slide]
# 组件化类库
- Polymer
- React
- Angular 2

[slide]
# React
JSX的扩展，直接更改了传统书写DOM的开发形式，让你在开发过程中不得不采用组件化的形式，在React的世界里，万事万物皆组件。

<img src="/mbp-1.png" style="width: 300px;"/>
<img src="/mbp-2.png" style="width: 300px;"/>

[slide]
# Angular 2
有人说Angular 1 与 2 的区别相同于 Java 与 JavaScript 的区别，Angular 2 支持 Web Components。

```js
@Component({selector: 'my-app'})
@View({template: '<h1>Hi {{ name }}</h1>'})
// Component controller
class MyAppComponent {
  constructor() {
    this.name = 'Ali';
  }
}
```

[slide]
# Polymer
构建在 Web Components 基础之上的前端框架，据说是最接近标准的库，它本身其实就是一个组件集，但目前的浏览器支持程度较差，一些内部的管理软件，还是可以尝试使用这一技术。

```html
<dom-module id="contact-card">
  <link rel="import" type="css" href="contact-card.css">
  <template>
    <content></content>
    <iron-icon icon="star" hidden$="{{!starred}}"></iron-icon>
  </template>
  <script>
    Polymer({
      is: 'contact-card',
      properties: {
        starred: Boolean
      }
    });
  </script>
</dom-module>
```

```html
<contact-card starred>
  <img src="profile.jpg" alt="Eric's photo">
  <span>Eric Bidelman</span>
</contact-card>
```

[slide]
# 总结

[slide]
从现在开始，就以带有**命名空间的HTML/CSS/JS组件化编码方式**来规划你的项目，做好业务模块化、页面组件化。
<br>
在你不想使用第三方组件库的情况下，也许，这是一个面向未来的组件化代码书写方式。

[slide]
# Thanks

![](/github-qrcode.png)

<small>从这里获取这次分享的PPT</small>
