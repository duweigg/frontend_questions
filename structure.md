# CSS

## 盒子模型  
Margin(外边距) - 清除边框外的区域，外边距是透明的。   
Border(边框) - 围绕在内边距和内容外的边框。   
Padding(内边距) - 清除内容周围的区域，内边距是透明的。   
Content(内容) - 盒子的内容，显示文本和图像。   

W3C width = content width   
IE  width = content+padding+border

## BFC，Flex  
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
## 局中  
## Grid  


# 变量类型

JS 的数据类型分类和判断
值类型和引用类型


# 原型与原型链

原型和原型链定义
继承


# 作用域和闭包

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