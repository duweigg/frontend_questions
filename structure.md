# CSS

## 盒子模型  
Margin(外边距) - 清除边框外的区域，外边距是透明的。   
Border(边框) - 围绕在内边距和内容外的边框。   
Padding(内边距) - 清除内容周围的区域，内边距是透明的。   
Content(内容) - 盒子的内容，显示文本和图像。   

W3C width = content width   
IE  width = content+padding+border

## BFC，Flex, Grid
display:inline-block   
避坑指南一：行内元素间隙   
几个行内元素之间出现了的空隙，这个空隙实际上是因为我们的HTML书写导致的，我们编写代码时输入空格、换行都会产生空白符   
想要解决这个间隙，我们可以给父元素设置font-size:0   
避坑指南二：高度塌陷，对齐问题   
vertical-align在默认情况下，会根据baseline进行定位，文字的定位不同，最终导致了整个块元素的高度塌陷。   
想要解决这一问题，我们只需将vertical-align设置为top

Flex Box   

flex-direction 决定主轴的方向
flex-wrap 决定了子元素如何换行
flex-flow 是flex-direction属性和flex-wrap属性的简写形式
jusity-content 决定了项目在主轴上的对齐方式
align-items 决定了项目在交叉轴上如何对齐
align-content  决定了多根轴线的对齐方式。如果项目只有一根轴线，该属性不起作用

子元素属性
order   决定项目的排列顺序。数值越小，排列越靠前，默认为0。
flex-grow   决定项目的放大比例，默认为0，即如果存在剩余空间，也不放大。
flex-shrink   决定项目的缩小比例，默认为1，即如果空间不足，该项目将缩小。
flex-basis   决定在分配多余空间之前，项目占据的主轴空间（main size）。浏览器根据这个属性，计算主轴是否有多余空间。它的默认值为auto，即项目的本来大小。
flex   是flex-grow, flex-shrink 和 flex-basis的简写，默认值为0 1 auto。后两个属性可选。
align-self   允许单个项目有与其他项目不一样的对齐方式，可覆盖align-items属性。默认值为auto，表示继承父元素的align-items属性，如果没有父元素，则等同于stretch。

注意点   
设为 Flex 布局以后，子元素的float、clear和vertical-align属性将失效。


Float  
float本身没有什么难度，但是设置了float会导致父元素的无法被撑开，margin失效，所以清除float也就成了开发必备知识。  
 
清除浮动
BFC, 

position属性决定了某个元素的定位方式，它的取值有以下几种：

static：该关键字指定元素使用正常的布局行为，即元素在文档常规流中当前的布局位置。
relative：该关键字下，元素先放置在未添加定位时的位置，再在不改变页面布局的前提下调整元素位置（因此会在此元素未添加定位时所在位置留下空白）。
absolute：元素会被移出正常文档流，并不为元素预留空间，通过指定元素相对于最近的非 static 定位祖先元素的偏移，来确定元素位置。绝对定位的元素可以设置外边距（margins），且不会与其他边距合并。
fixed：元素会被移出正常文档流，并不为元素预留空间，而是通过指定元素相对于屏幕视口（viewport）的位置来指定元素位置。元素的位置在屏幕滚动时不会改变。打印时，元素会出现在的每页的固定位置。
sticky：元素根据正常文档流进行定位，然后相对它的最近滚动祖先（nearest scrolling ancestor）和 containing block (最近块级祖先 nearest block-level ancestor)，包括table-related元素，基于top, right, bottom, 和 left的值进行偏移。偏移值不会影响任何其他元素的位置。


Normal flow（常规流）   （static， relative）   
BFC (Block Formatting Context)  

BFC的创建方法:

    根元素或其它包含它的元素。
    浮动 (元素的float不为none)。
    绝对定位元素 (元素的position为absolute或fixed)。
    行内块inline-blocks(元素的 display: inline-block)。
    表格单元格(元素的display: table-cell，HTML表格单元格默认属性)。
    overflow的值不为visible的元素。
    弹性盒flex boxes(元素的display: flex或inline-flex)。
 
效果：   

    内部的盒会在垂直方向一个接一个排列（可以看作BFC中有一个的常规流）。
    处于同一个BFC中的元素相互影响，可能会发生margin collapse。
    每个元素的margin box的左边，与容器块border box的左边相接触(对于从左往右的格式化，否则相反)，即使存在浮动也是如此。
    BFC就是页面上的一个隔离的独立容器，容器里面的子元素不会影响到外面的元素，反之亦然。
    计算BFC的高度时，考虑BFC所包含的所有元素，连浮动元素也参与计算。
    浮动盒区域不叠加到BFC上。

margin collapse 方法有以下几种：

    浮动元素不会与任何元素发生折叠，也包括它的子元素。
    创建了 BFC 的元素不会和它的子元素发生外边距折叠。
    绝对定位元素和其他任何元素之间不发生外边距折叠，也包括它的子元素。
    inline-block 元素和其他任何元素之间不发生外边距叠加，也包括它的子元素。
    给常规流中的块级元素添加padding、border、clear属性。

BFC计算高度包含浮动盒   
BFC内部不受浮动元素影响  

IFC (Inline Formatting Context)   
IFC由inline元素构成，它的布局规则是这样的：   

高度由其包含行内元素中最高的实际高度计算而来。   
IFC中的line box一般左右都贴紧整个IFC，但是会因为float元素而扰乱。float元素会位于IFC与与line box之间，使得line box宽度缩短。   
同个ifc下的多个line box高度会不同。   
水平的margin、padding、border有效，垂直无效。不能指定宽高。   
行框的高度由行高来决定。   

那么IFC一般有什么用呢？   

水平居中：当一个块要在环境中水平居中时，设置其为inline-block则会在外层产生IFC，通过text-align则可以使其水平居中。   
垂直居中：创建一个IFC，用其中一个元素撑开父元素的高度，然后设置其vertical-align:middle，其他行内元素则可以在此父元素下垂直居中。   

Unnormal Flow（非常规流）（absolute， fixed， sticky）   
对于非常规流，因为他们脱离了正常的文档流，所以他们不会对正常流的元素造成影响   

使用sticky布局的时候有几个注意点：

    父级元素不能有任何overflow:visible以外的overflow设置。   
    父级元素设置和粘性定位元素等高的固定的height高度值，或者高度计算值和粘性定位元素高度一样，没有粘滞效果。   
    同一个父容器中的sticky元素，如果定位值相等，则会重叠；如果属于不同父元素，且这些父元素正好紧密相连，则会鸠占鹊巢，挤开原来的元素，形成依次占位的效果。   
    sticky定位，不仅可以设置top，基于滚动容器上边缘定位；还可以设置bottom，也就是相对底部粘滞。如果是水平滚动，也可以设置left和right值。   
    z-index无效。

Grid
GFC(GridLayout Formatting Contexts)，"网格布局格式化上下文"，当为一个元素设置display值为grid的时候，此元素将会获得一个独立的渲染区域。  
我们可以通过在网格容器（grid container）上定义网格定义行（grid definition rows）和网格定义列（grid definition columns）属性各在网格项目（grid item）上定义网格行（grid row）和网格列（grid columns）为每一个网格项目（grid item）定义位置和空间。   
那么GFC有什么用呢，和table又有什么区别呢？首先同样是一个二维的表格，但GridLayout会有更加丰富的属性来控制行列，控制对齐以及更为精细的渲染语义和控制。

FFC(Flex Formatting Contexts)，"自适应格式化上下文"，display值为flex或者inline-flex的元素将会生成自适应容器（flex container）。 所以当我们使用flex布局的时候，我们就创建了一个FFC。

## 局中  
1. translate
```css
.parent {
    position: relative;
}
.child {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
}
```
2. flex
```css
.parent {
    display: flex;
    justify-content: center;
    align-items: center;
}
```
3. absolute margin auto
```css
.element {
    width: 600px; height: 400px;
    position: absolute; left: 0; top: 0; right: 0; bottom: 0;
    margin: auto;    /* 有了这个就自动居中了 */
}
```

4. table cell 
```HTML
<div class="Center-Container is-Table">
  <div class="Table-Cell">
    <div class="Center-Block">
    <!-- CONTENT -->
    </div>
  </div>
</div>
```
```CSS
.Center-Container.is-Table { display: table; }
.is-Table .Table-Cell {
  display: table-cell;
  vertical-align: middle;
}
.is-Table .Center-Block {
  width: 50%;
  margin: 0 auto;
}
```

# 变量类型

JS 的数据类型分类和判断   

    JavaScript中有6种数据类型：数字（number）、字符串（string）、布尔值（boolean）、undefined、null、对象（Object）。其中对象类型包括：数组（Array）、函数（Function）、还有两个特殊的对象：正则（RegExp）和日期（Date）。

typeof   

    typeof可以对基本类型number、string  、boolean、undefined做出准确的判断. 而对于引用类型，除了function之外返回的都是object。但当我们需要知道某个对象的具体类型时，typeof就显得有些力不从心了。

instanceof

    当我们需要知道某个对象的具体类型时,可以用运算符 instanceof，instanceof操作符判断左操作数对象的原型链上是否有右边这个构造函数的prototype属性，也就是说指定对象是否是某个构造函数的实例，最后返回布尔值  

    虽然 instanceof 能够判断出 [] 是Array的实例，但它认为 [] 也是Object的实例，为什么呢？ 我们来分析一下[]、Array、Object 三者之间的关系: 从instanceof 能够判断出 [].__proto__ 指向 Array.prototype， 而 Array.prototype.__proto__ 又指向了Object.prototype，Object.prototype.__proto__ 指向了null,标志着原型链的结束。因此，[]、Array、Object就形成了如下图所示的一条原型链：

Constructor   

    constructor属性的作用是，可以得知某个实例对象，到底是哪一个构造函数产生的。
    但是 constructor 属性易变，不可信赖，这个主要体现在自定义对象上，当开发者重写prototype后，原有的constructor会丢失。
    因此，为了规范，在重写对象原型时一般都需要重新给constructor赋值，以保证实例对象的类型不被改写。
```js
function F() {}
F.prototype = {
    constructor: F, 
_name: 'Eric',
};
var f = new F();
f.constructor === F; // true 
```

值类型和引用类型

值类型 number, string, null, undefined   

引用类型 object, function, array

值类型和引用类型的区别

    (1)基本类型的值是一经确定就不可变的
    (2)基本类型的比较是值的比较
    (3)基本类型的变量是存放在栈区的（栈区指内存里的栈内存）
    (4)引用类型的值是可变的
    (5)引用类型的值是同时保存在栈内存和堆内存中的对象
    (6)引用类型的比较是引用的比较

# 原型与原型链

原型和原型链定义   
    prototype is a property of a funtion, that references an object.   

想要弄清楚原型和原型链，这几个属性必须要搞清楚，__proto__、prototype、 constructor。   
其次你要知道js中对象和函数的关系，函数其实是对象的一种。   
最后你要知道函数、构造函数的区别，任何函数都可以作为构造函数，但是并不能将任意函数叫做构造函数，只有当一个函数通过new关键字调用的时候才可以成为构造函数   
1.__proto__、 constructor属性是对象所独有的；   
2.prototype属性是函数独有的；   
3.上面说过js中函数也是对象的一种，那么函数同样也有属性__proto__、 constructor；   


prototype设计之初就是为了实现继承，让由特定函数创建的所有实例共享属性和方法，也可以说是让某一个构造函数实例化的所有对象可以找到公共的方法和属性。有了prototype我们不需要为每一个实例创建重复的属性方法，而是将属性方法创建在构造函数的原型对象上（prototype）。那些不需要共享的才创建在构造函数中。

![alt text](https://segmentfault.com/img/remote/1460000021232136)

__proto__属性相当于通往prototype（“琅琊福地”）唯一的路（指针）
__proto__属性是对象（包括函数）独有的， 它的含义就是告诉我们一个对象的原型对象是谁。

![alt text](https://segmentfault.com/img/remote/1460000021232139)
```js
p1.__proto__ === Parent.prototype; // true
```

万物继承自Object.prototype。这也就是为什么我们可以实例化一个对象，并且可以调用该对象上没有的属性和方法了。如：
```js
//我们并没有在Parent中定义任何方法属性，但是我们可以调用
p1.toString();//hasOwnProperty 等等的一些方法
```
现在引出原型链的概念，当我们调用p1.toString()的时候，先在p1对象本身寻找，没有找到则通过p1.__proto__找到了原型对象Parent.prototype，也没有找到，又通过Parent.prototype.__proto__找到了上一层原型对象Object.prototype。在这一层找到了toString方法。返回该方法供p1使用。
当然如果找到Object.prototype上也没找到，就在Object.prototype.__proto__中寻找，但是Object.prototype.__proto__ === null所以就返回undefined。这就是为什么当访问对象中一个不存在的属性时，返回undefined了。   

constructor属性是让“徒弟”、“徒孙” 们知道是谁创造了自己，这里可不是“师父”啊
而是自己的父母，父母创造了自己，父母又是由上一辈人创造的，……追溯到头就是Function() 【女娲】。   
constructor是对象才有的属性，从图中看到它是从一个对象指向一个函数的。指向的函数就是该对象的构造函数。
![alt text](https://segmentfault.com/img/remote/1460000021232138)

它的作用是从一个对象指向一个函数，这个函数就是该对象的构造函数。通过栗子我们可以看到，p1的constructor属性指向了Parent，那么Parent就是p1的构造函数。同样Parent的constructor属性指向了Function，那么Function就是Parent的构造函数，然后又验证了Function就是根构造函数。

bug:
constructor属性本质上是只有prototype对象才有的，也就是构造函数.prototype.contructor === 该构造函数，而实例对象之所以也有，只是通过__proto__继承来自其构造函数的原型对象。
所以p1 => Parent() => Function()这里的contructor属性应该用虚线表示，注明来自继承得来。
```js
p1.hasOwnProperty('constructor') // false
Parent.prototype.hasOwnProperty('constructor') // true
```



    By default, the prototype object will have a constructor property which points to the original function or the class that the instance was created from.

    So when you try to access leo.constructor, leo doesn’t have a constructor property so it will delegate that lookup to Animal.prototype which indeed does have a constructor property.

    The way that instanceof works is it checks for the presence of constructor.prototype in the object’s prototype chain. In the example above, leo instanceof Animal is true because Object.getPrototypeOf(leo) === Animal.prototype. In addition, leo instanceof User is false because Object.getPrototypeOf(leo) !== User.prototype.

    Arrow functions don’t have their own this keyword. As a result, arrow functions can’t be constructor functions and if you try to invoke an arrow function with the new keyword, it’ll throw an error.
    arrow functions also don’t have a prototype property.



# 作用域和闭包

作用域：

    全局作用域
        带有关键字 var 的声明
---
    函数作用域
        立即执行函数：
        这是个很实用的函数，很多库都用它分离全局作用域，形成一个单独的函数作用域；
 ```html
 <script type="text/javascript">
     (function() {
     var testValue = 123;
     var testFunc = function () { console.log('just test'); };
     })();
     console.log(window.testValue);		// undefined
     console.log(window.testFunc);		// undefined
 </script>
 ````
        复制代码它能够自动执行 (function() { //... })() 里面包裹的内容，能够很好地消除全局变量的影响；
---
    块级作用域
        如果想要实现 块级作用域 那么我们需要用 let, const 关键字声明！！！
```js
    for(let i = 0; i < 5; i++) {
        // ...
    }
    console.log(i)				// 报错：ReferenceError: i is not defined
```
        在 for 循环执行完毕之后 i 变量就被释放了，它已经消失了！！！

```js
//problem
for(var i = 0; i < 5; i++) {
  setTimeout(function() {
     console.log(i);			// 5 5 5 5 5
  }, 200);
};

//solution 1 create 5 function scope
for(var i = 0; i < 5; i++) {
  abc(i);
};

function abc(i) {
  setTimeout(function() {
     console.log(i);			// 0 1 2 3 4 
  }, 200); 
}

//solution 2 create 5 value
for(var i = 0; i < 5; i++) {
  (function(j) {
    setTimeout(function() {
      console.log(j);
    }, 200);
  })(i);
};

//solution 3 block scope
for(let i = 0; i < 5; i++) {
    setTimeout(function() {
      console.log(i);
    }, 200);
};
```

    词法作用域 (Lexical scope) 
![alt text](https://user-gold-cdn.xitu.io/2018/3/28/1626ce92a304bc47?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)
```js
var testValue = 'outer';
function foo() {
  console.log(testValue);		// "outer"
}
function bar() {
  var testValue = 'inner';
  foo();
}
bar();    //"outer"
```
![alt text](https://user-gold-cdn.xitu.io/2018/3/28/1626ce99fad0f0ea?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)

---
    动态作用域 动态作用域跟 this 引用机制相关
        动态作用域，作用域是基于调用栈的，而不是代码中的作用域嵌套；
        作用域嵌套，有词法作用域一样的特性，查找变量时，总是寻找最近的作用域；


执行上下文
this
闭包


# 性能问题

有没有做过性能优化
如何定位性能问题
如何解决的


# webpack

loader
plugin
Tree Shaking
代码分割
打包优化技巧


# Promise

Promise 及其方法的实现


# HTTP 1/2

HTTP 有什么缺点
HTTP2 有什么好处
HTTPS 有什么好处， 有什么缺点，为什么。
TCP, UDP 的区别，  最佳场景
为什么说HTTPS 是安全的
解释一下加密过程
三次握手的过程，为什么握手三次, 为什么挥手四次


# 安全相关

## XSS
xss = 代码注入  
XSS 攻击可分为存储型、反射型和 DOM 型三种。
存储型-> database
反射型-> redirect
DOM  -> 

预防:

关键字过滤，   
长度限制，   
白名单   
escapeHTML() 转义：

React 会将所有要显示到 DOM 的字符串转义，防止 XSS
解决过度转义（特殊符号）
https://segmentfault.com/a/1190000012299682


小明为了加快网页的加载速度，把一个数据通过 JSON 的方式内联到 HTML 中
escapeEmbedJSON() 函数

## CSRF


# 浏览器缓存策略

缓存头相关
浏览器 Cookie 相关


# 基础的数据结构和算法

Tree,
BFS
DFS
递归
动态规划


# 框架相关(如果你写了的话)

1、React diff
2、虚拟dom
3、react 受控 非受控组件
4、react 新旧生命周期
5、 事件传播
6、Event loop


#  一些发散性问题

# 输入URL 到页面展示发生了什么


# 稳定性保障

# 错误监控， 收集，分析


# 项目架构经验等
# 如何设计一个好的组件
# 节流，防抖


作者：皮小蛋
链接：https://juejin.cn/post/6844903961518931981
来源：掘金
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。