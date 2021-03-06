**三、JavaScript**

**1 闭包**

- 闭包就是能够读取其他函数内部变量的函数
- 闭包是指有权访问另一个函数作用域中变量的函数，创建闭包的最常见的方式就是在一个函数内创建另一个函数，通过另一个函数访问这个函数的局部变量,利用闭包可以突破作用链域
- 闭包的特性：

- - 函数内再嵌套函数
  - 内部函数可以引用外层的参数和变量
  - 参数和变量不会被垃圾回收机制回收

说说你对闭包的理解

- 使用闭包主要是为了设计私有的方法和变量。闭包的优点是可以避免全局变量的污染，缺点是闭包会常驻内存，会增大内存使用量，使用不当很容易造成内存泄露。在js中，函数即闭包，只有函数才会产生作用域的概念
- 闭包 的最大用处有两个，一个是可以读取函数内部的变量，另一个就是让这些变量始终保持在内存中
- 闭包的另一个用处，是封装对象的私有属性和私有方法
- 好处：能够实现封装和缓存等；
- 坏处：就是消耗内存、不正当使用会造成内存溢出的问题

使用闭包的注意点

- 由于闭包会使得函数中的变量都被保存在内存中，内存消耗很大，所以不能滥用闭包，否则会造成网页的性能问题，在IE中可能导致内存泄露
- 解决方法是，在退出函数之前，将不使用的局部变量全部删除

**2 说说你对作用域链的理解**

- 作用域链的作用是保证执行环境里有权访问的变量和函数是有序的，作用域链的变量只能向上访问，变量访问到window对象即被终止，作用域链向下访问变量是不被允许的
- 简单的说，作用域就是变量与函数的可访问范围，即作用域控制着变量与函数的可见性和生命周期

**3 JavaScript原型，原型链 ? 有什么特点？**

- 每个对象都会在其内部初始化一个属性，就是prototype(原型)，当我们访问一个对象的属性时
- 如果这个对象内部不存在这个属性，那么他就会去prototype里找这个属性，这个prototype又会有自己的prototype，于是就这样一直找下去，也就是我们平时所说的原型链的概念
- 关系：instance.constructor.prototype = instance.__proto__
- 特点：

- - JavaScript对象是通过引用来传递的，我们创建的每个新对象实体中并没有一份属于自己的原型副本。当我们修改原型时，与之相关的对象也会继承这一改变

- 当我们需要一个属性的时，Javascript引擎会先看当前对象中是否有这个属性， 如果没有的
- 就会查找他的Prototype对象是否有这个属性，如此递推下去，一直检索到 Object 内建对象

**4 请解释什么是事件代理**

- 事件代理（Event Delegation），又称之为事件委托。是 JavaScript 中常用绑定事件的常用技巧。顾名思义，“事件代理”即是把原本需要绑定的事件委托给父元素，让父元素担当事件监听的职务。事件代理的原理是DOM元素的事件冒泡。使用事件代理的好处是可以提高性能
- 可以大量节省内存占用，减少事件注册，比如在table上代理所有td的click事件就非常棒
- 可以实现当新增子对象时无需再次对其绑定

**5 Javascript如何实现继承？**

- 构造继承
- 原型继承
- 实例继承
- 拷贝继承
- 原型prototype机制或apply和call方法去实现较简单，建议使用构造函数与原型混合方式

function Parent(){  this.name = 'wang';}function Child(){         this.age = 28;}     Child.prototype = new Parent();//继承了Parent，通过原型var demo = new Child();alert(demo.age);alert(demo.name);//得到被继承的属性

**6 谈谈This对象的理解**

- this总是指向函数的直接调用者（而非间接调用者）
- 如果有new关键字，this指向new出来的那个对象
- 在事件中，this指向触发这个事件的对象，特殊的是，IE中的attachEvent中的this总是指向全局对象Window

**7 事件模型**

W3C中定义事件的发生经历三个阶段：捕获阶段（capturing）、目标阶段（targetin）、冒泡阶段（bubbling）

- 冒泡型事件：当你使用事件冒泡时，子级元素先触发，父级元素后触发
- 捕获型事件：当你使用事件捕获时，父级元素先触发，子级元素后触发
- DOM事件流：同时支持两种事件模型：捕获型事件和冒泡型事件
- 阻止冒泡：在W3c中，使用stopPropagation()方法；在IE下设置cancelBubble = true
- 阻止捕获：阻止事件的默认行为，例如click - <a>后的跳转。在W3c中，使用preventDefault()方法，在IE下设置window.event.returnValue = false

**8 new操作符具体干了什么呢?**

- 创建一个空对象，并且 this 变量引用该对象，同时还继承了该函数的原型
- 属性和方法被加入到 this 引用的对象中
- 新创建的对象由 this 所引用，并且最后隐式的返回 this

**9 Ajax原理**

- Ajax的原理简单来说是在用户和服务器之间加了—个中间层(AJAX引擎)，通过XmlHttpRequest对象来向服务器发异步请求，从服务器获得数据，然后用javascript来操作DOM而更新页面。使用户操作与服务器响应异步化。这其中最关键的一步就是从服务器获得请求数据
- Ajax的过程只涉及JavaScript、XMLHttpRequest和DOM。XMLHttpRequest是ajax的核心机制

/** 1. 创建连接 **/var xhr = null;xhr = new XMLHttpRequest()/** 2. 连接服务器 **/xhr.open('get', url, true)/** 3. 发送请求 **/xhr.send(null);/** 4. 接受请求 **/xhr.onreadystatechange = function(){  if(xhr.readyState == 4){  if(xhr.status == 200){  success(xhr.responseText);  } else {   /** false **/  fail && fail(xhr.status);  }  }}

ajax 有那些优缺点?

- 优点：

- - 通过异步模式，提升了用户体验.
  - 优化了浏览器和服务器之间的传输，减少不必要的数据往返，减少了带宽占用.
  - Ajax在客户端运行，承担了一部分本来由服务器承担的工作，减少了大用户量下的服务器负载。
  - Ajax可以实现动态不刷新（局部刷新）

- 缺点：

- - 安全问题 AJAX暴露了与服务器交互的细节。
  - 对搜索引擎的支持比较弱。
  - 不容易调试。

**10 如何解决跨域问题?**

首先了解下浏览器的同源策略 同源策略/SOP（Same origin policy）是一种约定，由Netscape公司1995年引入浏览器，它是浏览器最核心也最基本的安全功能，如果缺少了同源策略，浏览器很容易受到XSS、CSFR等攻击。所谓同源是指"协议+域名+端口"三者相同，即便两个不同的域名指向同一个ip地址，也非同源

那么怎样解决跨域问题的呢？

- 通过jsonp跨域

var script = document.createElement('script');script.type = 'text/javascript';// 传参并指定回调执行函数为onBackscript.src = 'http://www.....:8080/login?user=admin&callback=onBack';document.head.appendChild(script);// 回调执行函数function onBack(res) {     alert(JSON.stringify(res));}

- document.domain + iframe跨域

此方案仅限主域相同，子域不同的跨域应用场景

1.）父窗口：(http://www.domain.com/a.html)

<iframe id="iframe" src="http://child.domain.com/b.html"></iframe><script>
    document.domain = 'domain.com';
    var user = 'admin';</script>

2.）子窗口：(http://child.domain.com/b.html)

document.domain = 'domain.com';// 获取父窗口中变量alert('get js data from parent ---> ' + window.parent.user);

- nginx代理跨域
- nodejs中间件代理跨域
- 后端在头部信息里面设置安全域名

**11 模块化开发怎么做？**

- 立即执行函数,不暴露私有成员

var module1 = (function(){　　　　var _count = 0;　　　　var m1 = function(){　　　　　　//...　　　　};　　　　var m2 = function(){　　　　　　//...　　　　};　　　　return {　　　　　　m1 : m1,　　　　　　m2 : m2 　　　　};})();

**12 异步加载JS的方式有哪些？**

- defer，只支持IE
- async：
- 创建script，插入到DOM中，加载完毕后callBack

**13 那些操作会造成内存泄漏？**

- 内存泄漏指任何对象在您不再拥有或需要它之后仍然存在
- setTimeout 的第一个参数使用字符串而非函数的话，会引发内存泄漏
- 闭包使用不当

**14 XML和JSON的区别？**

- 数据体积方面

- - JSON相对于XML来讲，数据的体积小，传递的速度更快些。

- 数据交互方面

- - JSON与JavaScript的交互更加方便，更容易解析处理，更好的数据交互

- 数据描述方面

- - JSON对数据的描述性比XML较差

- 传输速度方面

- - JSON的速度要远远快于XML

**15 谈谈你对webpack的看法**

- WebPack 是一个模块打包工具，你可以使用WebPack管理你的模块依赖，并编绎输出模块们所需的静态文件。它能够很好地管理、打包Web开发中所用到的HTML、Javascript、CSS以及各种静态文件（图片、字体等），让开发过程更加高效。对于不同类型的资源，webpack有对应的模块加载器。webpack模块打包器会分析模块间的依赖关系，最后 生成了优化且合并后的静态资源

**16 说说你对AMD和Commonjs的理解**

- CommonJS是服务器端模块的规范，Node.js采用了这个规范。CommonJS规范加载模块是同步的，也就是说，只有加载完成，才能执行后面的操作。AMD规范则是非同步加载模块，允许指定回调函数
- AMD推荐的风格通过返回一个对象做为模块对象，CommonJS的风格通过对module.exports或exports的属性赋值来达到暴露模块对象的目的

**17 常见web安全及防护原理**

- sql注入原理

- - 就是通过把SQL命令插入到Web表单递交或输入域名或页面请求的查询字符串，最终达到欺骗服务器执行恶意的SQL命令

- 总的来说有以下几点

- - 永远不要信任用户的输入，要对用户的输入进行校验，可以通过正则表达式，或限制长度，对单引号和双"-"进行转换等
  - 永远不要使用动态拼装SQL，可以使用参数化的SQL或者直接使用存储过程进行数据查询存取
  - 永远不要使用管理员权限的数据库连接，为每个应用使用单独的权限有限的数据库连接
  - 不要把机密信息明文存放，请加密或者hash掉密码和敏感的信息

XSS原理及防范

- Xss(cross-site scripting)攻击指的是攻击者往Web页面里插入恶意html标签或者javascript代码。比如：攻击者在论坛中放一个看似安全的链接，骗取用户点击后，窃取cookie中的用户私密信息；或者攻击者在论坛中加一个恶意表单，当用户提交表单的时候，却把信息传送到攻击者的服务器中，而不是用户原本以为的信任站点

XSS防范方法

- 首先代码里对用户输入的地方和变量都需要仔细检查长度和对”<”,”>”,”;”,”’”等字符做过滤；其次任何内容写到页面之前都必须加以encode，避免不小心把html tag 弄出来。这一个层面做好，至少可以堵住超过一半的XSS 攻击

XSS与CSRF有什么区别吗？

- XSS是获取信息，不需要提前知道其他用户页面的代码和数据包。CSRF是代替用户完成指定的动作，需要知道其他用户页面的代码和数据包。要完成一次CSRF攻击，受害者必须依次完成两个步骤
- 登录受信任网站A，并在本地生成Cookie
- 在不登出A的情况下，访问危险网站B

CSRF的防御

- 服务端的CSRF方式方法很多样，但总的思想都是一致的，就是在客户端页面增加伪随机数
- 通过验证码的方法

**18 用过哪些设计模式？**

- 工厂模式：

- - 工厂模式解决了重复实例化的问题，但还有一个问题,那就是识别问题，因为根本无法
  - 主要好处就是可以消除对象间的耦合，通过使用工程方法而不是new关键字

- 构造函数模式

- - 使用构造函数的方法，即解决了重复实例化的问题，又解决了对象识别的问题，该模式与工厂模式的不同之处在于
  - 直接将属性和方法赋值给 this对象;

**19 为什么要有同源限制？**

- 同源策略指的是：协议，域名，端口相同，同源策略是一种安全协议
- 举例说明：比如一个黑客程序，他利用Iframe把真正的银行登录页面嵌到他的页面上，当你使用真实的用户名，密码登录时，他的页面就可以通过Javascript读取到你的表单中input中的内容，这样用户名，密码就轻松到手了。

**20 offsetWidth/offsetHeight,clientWidth/clientHeight与scrollWidth/scrollHeight的区别**

- offsetWidth/offsetHeight返回值包含content + padding + border，效果与e.getBoundingClientRect()相同
- clientWidth/clientHeight返回值只包含content + padding，如果有滚动条，也不包含滚动条
- scrollWidth/scrollHeight返回值包含content + padding + 溢出内容的尺寸

**21 javascript有哪些方法定义对象**

- 对象字面量： var obj = {};
- 构造函数： var obj = new Object();
- Object.create(): var obj = Object.create(Object.prototype);

**22 常见兼容性问题？**

- png24位的图片在iE6浏览器上出现背景，解决方案是做成PNG8
- 浏览器默认的margin和padding不同。解决方案是加一个全局的*{margin:0;padding:0;}来统一,，但是全局效率很低，一般是如下这样解决：

body,ul,li,ol,dl,dt,dd,form,input,h1,h2,h3,h4,h5,h6,p{margin:0;padding:0;}

- IE下,event对象有x,y属性,但是没有pageX,pageY属性
- Firefox下,event对象有pageX,pageY属性,但是没有x,y属性.

**23 说说你对promise的了解**

- 依照 Promise/A+ 的定义，Promise 有四种状态：

- - pending: 初始状态, 非 fulfilled 或 rejected.
  - fulfilled: 成功的操作.
  - rejected: 失败的操作.
  - settled: Promise已被fulfilled或rejected，且不是pending

- 另外， fulfilled与 rejected一起合称 settled
- Promise 对象用来进行延迟(deferred) 和异步(asynchronous) 计算

Promise 的构造函数

- 构造一个 Promise，最基本的用法如下：

var promise = new Promise(function(resolve, reject) {          if (...) {  // succeed              resolve(result);          } else {   // fails              reject(Error(errMessage));          }     });

- Promise 实例拥有 then 方法（具有 then 方法的对象，通常被称为thenable）。它的使用方法如下：

promise.then(onFulfilled, onRejected)

- 接收两个函数作为参数，一个在 fulfilled 的时候被调用，一个在rejected的时候被调用，接收参数就是 future，onFulfilled 对应resolve, onRejected对应 reject

**24 你觉得jQuery源码有哪些写的好的地方**

- jquery源码封装在一个匿名函数的自执行环境中，有助于防止变量的全局污染，然后通过传入window对象参数，可以使window对象作为局部变量使用，好处是当jquery中访问window对象的时候，就不用将作用域链退回到顶层作用域了，从而可以更快的访问window对象。同样，传入undefined参数，可以缩短查找undefined时的作用域链
- jquery将一些原型属性和方法封装在了jquery.prototype中，为了缩短名称，又赋值给了jquery.fn，这是很形象的写法
- 有一些数组或对象的方法经常能使用到，jQuery将其保存为局部变量以提高访问速度
- jquery实现的链式调用可以节约代码，所返回的都是同一个对象，可以提高代码效率

**25 vue、react、angular**

- Vue.js 一个用于创建 web 交互界面的库，是一个精简的 MVVM。它通过双向数据绑定把 View层和 Model 层连接了起来。实际的 DOM 封装和输出格式都被抽象为了Directives 和 Filters
- AngularJS 是一个比较完善的前端MVVM框架，包含模板，数据双向绑定，路由，模块化，服务，依赖注入等所有功能，模板功能强大丰富，自带了丰富的 Angular指令
- react React 仅仅是 VIEW 层是facebook公司。推出的一个用于构建UI的一个库，能够实现服务器端的渲染。用了virtual dom，所以性能很好。

**26 Node的应用场景**

- 特点：

- - 1、它是一个Javascript运行环境
  - 2、依赖于Chrome V8引擎进行代码解释
  - 3、事件驱动
  - 4、非阻塞I/O
  - 5、单进程，单线程

- 优点：

- - 高并发（最重要的优点）

- 缺点：

- - 1、只支持单核CPU，不能充分利用CPU
  - 2、可靠性低，一旦代码某个环节崩溃，整个系统都崩溃

**27 谈谈你对AMD、CMD的理解**

- CommonJS是服务器端模块的规范，Node.js采用了这个规范。CommonJS规范加载模块是同步的，也就是说，只有加载完成，才能执行后面的操作。AMD规范则是非同步加载模块，允许指定回调函数
- AMD推荐的风格通过返回一个对象做为模块对象，CommonJS的风格通过对module.exports或exports的属性赋值来达到暴露模块对象的目的

es6模块 CommonJS、AMD、CMD

- CommonJS 的规范中，每个 JavaScript 文件就是一个独立的模块上下文（module context），在这个上下文中默认创建的属性都是私有的。也就是说，在一个文件定义的变量（还包括函数和类），都是私有的，对其他文件是不可见的。
- CommonJS是同步加载模块,在浏览器中会出现堵塞情况，所以不适用
- AMD 异步，需要定义回调define方式
- es6 一个模块就是一个独立的文件，该文件内部的所有变量，外部无法获取。如果你希望外部能够读取模块内部的某个变量，就必须使用export关键字输出该变量 es6还可以导出类、方法，自动适用严格模式

**28 那些操作会造成内存泄漏**

- 内存泄漏指任何对象在您不再拥有或需要它之后仍然存在
- setTimeout 的第一个参数使用字符串而非函数的话，会引发内存泄漏
- 闭包、控制台日志、循环（在两个对象彼此引用且彼此保留时，就会产生一个循环）

**29 web开发中会话跟踪的方法有哪些**

- cookie
- session
- url重写
- 隐藏input
- ip地址

**30 介绍js的基本数据类型**

- Undefined、Null、Boolean、Number、String

**31 介绍js有哪些内置对象**

- Object 是 JavaScript 中所有对象的父对象
- 数据封装类对象：Object、Array、Boolean、Number 和 String
- 其他对象：Function、Arguments、Math、Date、RegExp、Error

**32 说几条写JavaScript的基本规范**

- 不要在同一行声明多个变量
- 请使用===/!==来比较true/false或者数值
- 使用对象字面量替代new Array这种形式
- 不要使用全局函数
- Switch语句必须带有default分支
- If语句必须使用大括号
- for-in循环中的变量 应该使用var关键字明确限定作用域，从而避免作用域污

**33 JavaScript有几种类型的值**

- 栈：原始数据类型（Undefined，Null，Boolean，Number、String）
- 堆：引用数据类型（对象、数组和函数）
- 两种类型的区别是：存储位置不同；
- 原始数据类型直接存储在栈(stack)中的简单数据段，占据空间小、大小固定，属于被频繁使用数据，所以放入栈中存储；
- 引用数据类型存储在堆(heap)中的对象,占据空间大、大小不固定,如果存储在栈中，将会影响程序运行的性能；引用数据类型在栈中存储了指针，该指针指向堆中该实体的起始地址。当解释器寻找引用值时，会首先检索其
- 在栈中的地址，取得地址后从堆中获得实体

![img](js考点.assets/75652e676966.gif)

**34 javascript创建对象的几种方式**

javascript创建对象简单的说,无非就是使用内置对象或各种自定义对象，当然还可以用JSON；但写法有很多种，也能混合使用

- 对象字面量的方式

person={firstname:"Mark",lastname:"Yun",age:25,eyecolor:"black"};

- 用function来模拟无参的构造函数

function Person(){}  var person=new Person();//定义一个function，如果使用new"实例化",该function可以看作是一个Class         person.name="Mark";         person.age="25";         person.work=function(){         alert(person.name+" hello...");}person.work();

- 用function来模拟参构造函数来实现（用this关键字定义构造的上下文属性）

function Pet(name,age,hobby){        this.name=name;//this作用域：当前对象        this.age=age;        this.hobby=hobby;        this.eat=function(){            alert("我叫"+this.name+",我喜欢"+this.hobby+",是个程序员");        }}var maidou =new Pet("麦兜",25,"coding");//实例化、创建对象maidou.eat();//调用eat方法

- 用工厂方式来创建（内置对象）

var wcDog =new Object();      wcDog.name="旺财";      wcDog.age=3;      wcDog.work=function(){        alert("我是"+wcDog.name+",汪汪汪......");      }      wcDog.work();

- 用原型方式来创建

function Dog(){}Dog.prototype.name="旺财";Dog.prototype.eat=function(){  alert(this.name+"是个吃货");}var wangcai =new Dog();wangcai.eat();

- 用混合方式来创建

 function Car(name,price){  this.name=name;  this.price=price;}Car.prototype.sell=function(){  alert("我是"+this.name+"，我现在卖"+this.price+"万元");}var camry =new Car("凯美瑞",27);camry.sell();

**35 eval是做什么的**

- 它的功能是把对应的字符串解析成JS代码并运行
- 应该避免使用eval，不安全，非常耗性能（2次，一次解析成js语句，一次执行）
- 由JSON字符串转换为JSON对象的时候可以用eval，var obj =eval('('+ str +')')

**36 null，undefined 的区别**

- undefined 表示不存在这个值。
- undefined :是一个表示"无"的原始值或者说表示"缺少值"，就是此处应该有一个值，但是还没有定义。当尝试读取时会返回 undefined
- 例如变量被声明了，但没有赋值时，就等于undefined
- null 表示一个对象被定义了，值为“空值”
- null : 是一个对象(空对象, 没有任何属性和方法)
- 例如作为函数的参数，表示该函数的参数不是对象；
- 在验证null时，一定要使用　=== ，因为 ==无法分别null 和　undefined

**37 ["1", "2", "3"].map(parseInt) 答案是多少**

- [1, NaN, NaN]因为 parseInt 需要两个参数 (val, radix)，其中radix 表示解析时用的基数。
- map传了 3个(element, index, array)，对应的 radix 不合法导致解析失败。

**38 javascript 代码中的"use strict";是什么意思**

- use strict是一种ECMAscript 5 添加的（严格）运行模式,这种模式使得 Javascript 在更严格的条件下运行,使JS编码更加规范化的模式,消除Javascript语法的一些不合理、不严谨之处，减少一些怪异行为

**39 JSON 的了解**

- JSON(JavaScript Object Notation) 是一种轻量级的数据交换格式
- 它是基于JavaScript的一个子集。数据格式简单, 易于读写, 占用带宽小
- JSON字符串转换为JSON对象:

var obj =eval('('+ str +')');var obj = str.parseJSON();var obj = JSON.parse(str);

- JSON对象转换为JSON字符串：

var last=obj.toJSONString(); var last=JSON.stringify(obj);

**40 js延迟加载的方式有哪些**

- defer和async、动态创建DOM方式（用得最多）、按需异步载入js

**41 同步和异步的区别**

- 同步：浏览器访问服务器请求，用户看得到页面刷新，重新发请求,等请求完，页面刷新，新内容出现，用户看到新内容,进行下一步操作
- 异步：浏览器访问服务器请求，用户正常操作，浏览器后端进行请求。等请求完，页面不刷新，新内容也会出现，用户看到新内容

**42 渐进增强和优雅降级**

- 渐进增强 ：针对低版本浏览器进行构建页面，保证最基本的功能，然后再针对高级浏览器进行效果、交互等改进和追加功能达到更好的用户体验。
- 优雅降级 ：一开始就构建完整的功能，然后再针对低版本浏览器进行兼容

**43 defer和async**

- defer并行加载js文件，会按照页面上script标签的顺序执行
- async并行加载js文件，下载完成立即执行，不会按照页面上script标签的顺序执行

**44 说说严格模式的限制**

- 变量必须声明后再使用
- 函数的参数不能有同名属性，否则报错
- 不能使用with语句
- 禁止this指向全局对象

**45 attribute和property的区别是什么**

- attribute是dom元素在文档中作为html标签拥有的属性；
- property就是dom元素在js中作为对象拥有的属性。
- 对于html的标准属性来说，attribute和property是同步的，是会自动更新的
- 但是对于自定义的属性来说，他们是不同步的

**46 谈谈你对ES6的理解**

- 新增模板字符串（为JavaScript提供了简单的字符串插值功能）
- 箭头函数
- for-of（用来遍历数据—例如数组中的值。）
- arguments对象可被不定参数和默认参数完美代替。
- ES6将promise对象纳入规范，提供了原生的Promise对象。
- 增加了let和const命令，用来声明变量。
- 增加了块级作用域。
- let命令实际上就增加了块级作用域。
- 还有就是引入module模块的概念

**47 ECMAScript6 怎么写class么**

- 这个语法糖可以让有OOP基础的人更快上手js，至少是一个官方的实现了
- 但对熟悉js的人来说，这个东西没啥大影响；一个Object.creat()搞定继承，比class简洁清晰的多

**48 什么是面向对象编程及面向过程编程，它们的异同和优缺点**

- 面向过程就是分析出解决问题所需要的步骤，然后用函数把这些步骤一步一步实现，使用的时候一个一个依次调用就可以了
- 面向对象是把构成问题事务分解成各个对象，建立对象的目的不是为了完成一个步骤，而是为了描叙某个事物在整个解决问题的步骤中的行为
- 面向对象是以功能来划分问题，而不是步骤

**49 面向对象编程思想**

- 基本思想是使用对象，类，继承，封装等基本概念来进行程序设计
- 优点

- - 采用面向对象思想设计的结构，可读性高，由于继承的存在，即使改变需求，那么维护也只是在局部模块，所以维护起来是非常方便和较低成本的
  - 易维护
  - 易扩展
  - 开发工作的重用性、继承性高，降低重复工作量。
  - 缩短了开发周期

**50 对web标准、可用性、可访问性的理解**

- 可用性（Usability）：产品是否容易上手，用户能否完成任务，效率如何，以及这过程中用户的主观感受可好，是从用户的角度来看产品的质量。可用性好意味着产品质量高，是企业的核心竞争力
- 可访问性（Accessibility）：Web内容对于残障用户的可阅读和可理解性
- 可维护性（Maintainability）：一般包含两个层次，一是当系统出现问题时，快速定位并解决问题的成本，成本低则可维护性好。二是代码是否容易被人理解，是否容易修改和增强功能。

**51 如何通过JS判断一个数组**

- instanceof方法

- - instanceof 运算符是用来测试一个对象是否在其原型链原型构造函数的属性

var arr = [];arr instanceof Array; // true

- constructor方法

- - constructor属性返回对创建此对象的数组函数的引用，就是返回对象相对应的构造函数

var arr = [];arr.constructor == Array; //true

- 最简单的方法

- - 这种写法，是 jQuery 正在使用的

Object.prototype.toString.call(value) == '[object Array]'// 利用这个方法，可以写一个返回数据类型的方法var isType = function (obj) {      return Object.prototype.toString.call(obj).slice(8,-1);}

- ES5新增方法isArray()

var a = new Array(123);var b = new Date();console.log(Array.isArray(a)); //trueconsole.log(Array.isArray(b)); //false

**52 谈一谈let与var的区别**

- let命令不存在变量提升，如果在let前使用，会导致报错
- 如果块区中存在let和const命令，就会形成封闭作用域
- 不允许重复声明，因此，不能在函数内部重新声明参数

**53 map与forEach的区别**

- forEach方法，是最基本的方法，就是遍历与循环，默认有3个传参：分别是遍历的数组内容item、数组索引index、和当前遍历数组Array
- map方法，基本用法与forEach一致，但是不同的，它会返回一个新的数组，所以在callback需要有return值，如果没有，会返回undefined

**54 谈一谈你理解的函数式编程**

- 简单说，"函数式编程"是一种"编程范式"（programming paradigm），也就是如何编写程序的方法论
- 它具有以下特性：闭包和高阶函数、惰性计算、递归、函数是"第一等公民"、只用"表达式"

**55 谈一谈箭头函数与普通函数的区别？**

- 函数体内的this对象，就是定义时所在的对象，而不是使用时所在的对象
- 不可以当作构造函数，也就是说，不可以使用new命令，否则会抛出一个错误
- 不可以使用arguments对象，该对象在函数体内不存在。如果要用，可以用Rest参数代替
- 不可以使用yield命令，因此箭头函数不能用作Generator函数

**56 谈一谈函数中this的指向**

- this的指向在函数定义的时候是确定不了的，只有函数执行的时候才能确定this到底指向谁，实际上this的最终指向的是那个调用它的对象
- 《javascript语言精髓》中大概概括了4种调用方式：
- 方法调用模式
- 函数调用模式
- 构造器调用模式

graph LRA-->B

- apply/call调用模式

**57 异步编程的实现方式**

- 回调函数

- - 优点：简单、容易理解
  - 缺点：不利于维护，代码耦合高

- 事件监听(采用时间驱动模式，取决于某个事件是否发生)：

- - 优点：容易理解，可以绑定多个事件，每个事件可以指定多个回调函数
  - 缺点：事件驱动型，流程不够清晰

- 发布/订阅(观察者模式)

- - 类似于事件监听，但是可以通过‘消息中心’，了解现在有多少发布者，多少订阅者

- Promise对象

- - 优点：可以利用then方法，进行链式写法；可以书写错误时的回调函数；
  - 缺点：编写和理解，相对比较难

- Generator函数

- - 优点：函数体内外的数据交换、错误处理机制
  - 缺点：流程管理不方便

- async函数

- - 优点：内置执行器、更好的语义、更广的适用性、返回的是Promise、结构清晰。
  - 缺点：错误处理机制

**58 对原生Javascript了解程度**

- 数据类型、运算、对象、Function、继承、闭包、作用域、原型链、事件、RegExp、JSON、Ajax、DOM、BOM、内存泄漏、跨域、异步装载、模板引擎、前端MVC、路由、模块化、Canvas、ECMAScript

**59 Js动画与CSS动画区别及相应实现**

- CSS3的动画的优点

- - 在性能上会稍微好一些，浏览器会对CSS3的动画做一些优化
  - 代码相对简单

- 缺点

- - 在动画控制上不够灵活
  - 兼容性不好

- JavaScript的动画正好弥补了这两个缺点，控制能力很强，可以单帧的控制、变换，同时写得好完全可以兼容IE6，并且功能强大。对于一些复杂控制的动画，使用javascript会比较靠谱。而在实现一些小的交互动效的时候，就多考虑考虑CSS吧

**60 JS 数组和对象的遍历方式，以及几种方式的比较**

通常我们会用循环的方式来遍历数组。但是循环是 导致js 性能问题的原因之一。一般我们会采用下几种方式来进行数组的遍历

- for in循环
- for循环
- forEach

- - 这里的 forEach回调中两个参数分别为 value，index
  - forEach 无法遍历对象
  - IE不支持该方法；Firefox 和 chrome 支持
  - forEach 无法使用 break，continue 跳出循环，且使用 return 是跳过本次循环

- 这两种方法应该非常常见且使用很频繁。但实际上，这两种方法都存在性能问题
- 在方式一中，for-in需要分析出array的每个属性，这个操作性能开销很大。用在 key 已知的数组上是非常不划算的。所以尽量不要用for-in，除非你不清楚要处理哪些属性，例如 JSON对象这样的情况
- 在方式2中，循环每进行一次，就要检查一下数组长度。读取属性（数组长度）要比读局部变量慢，尤其是当 array 里存放的都是 DOM 元素，因为每次读取都会扫描一遍页面上的选择器相关元素，速度会大大降低

**61 gulp是什么**

- gulp是前端开发过程中一种基于流的代码构建工具，是自动化项目的构建利器；它不仅能对网站资源进行优化，而且在开发过程中很多重复的任务能够使用正确的工具自动完成
- Gulp的核心概念：流
- 流，简单来说就是建立在面向对象基础上的一种抽象的处理数据的工具。在流中，定义了一些处理数据的基本操作，如读取数据，写入数据等，程序员是对流进行所有操作的，而不用关心流的另一头数据的真正流向
- gulp正是通过流和代码优于配置的策略来尽量简化任务编写的工作
- Gulp的特点：

- - 易于使用：通过代码优于配置的策略，gulp 让简单的任务简单，复杂的任务可管理
  - 构建快速 利用 Node.js 流的威力，你可以快速构建项目并减少频繁的 IO 操作
  - 易于学习 通过最少的 API，掌握 gulp 毫不费力，构建工作尽在掌握：如同一系列流管道

**62 说一下Vue的双向绑定数据的原理**

- vue.js 则是采用数据劫持结合发布者-订阅者模式的方式，通过Object.defineProperty()来劫持各个属性的setter，getter，在数据变动时发布消息给订阅者，触发相应的监听回调

**63 事件的各个阶段**

- 1：捕获阶段 ---> 2：目标阶段 ---> 3：冒泡阶段
- document ---> target目标 ----> document
- 由此，addEventListener的第三个参数设置为true和false的区别已经非常清晰了

- - true表示该元素在事件的“捕获阶段”（由外往内传递时）响应事件
  - false表示该元素在事件的“冒泡阶段”（由内向外传递时）响应事件

**64 let var const**

let

- 允许你声明一个作用域被限制在块级中的变量、语句或者表达式
- let绑定不受变量提升的约束，这意味着let声明不会被提升到当前
- 该变量处于从块开始到初始化处理的“暂存死区”

var

- 声明变量的作用域限制在其声明位置的上下文中，而非声明变量总是全局的
- 由于变量声明（以及其他声明）总是在任意代码执行之前处理的，所以在代码中的任意位置声明变量总是等效于在代码开头声明

const

- 声明创建一个值的只读引用 (即指针)
- 基本数据当值发生改变时，那么其对应的指针也将发生改变，故造成 const申明基本数据类型时
- 再将其值改变时，将会造成报错， 例如 const a = 3 ; a = 5时 将会报错
- 但是如果是复合类型时，如果只改变复合类型的其中某个Value项时， 将还是正常使用

**65 快速的让一个数组乱序**

var arr = [1,2,3,4,5,6,7,8,9,10];arr.sort(function(){     return Math.random() - 0.5;})console.log(arr);

**66 如何渲染几万条数据并不卡住界面**

这道题考察了如何在不卡住页面的情况下渲染数据，也就是说不能一次性将几万条都渲染出来，而应该一次渲染部分 DOM，那么就可以通过 requestAnimationFrame 来每 16 ms 刷新一次

<!DOCTYPE html><html lang="en"><head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Document</title></head><body>
  <ul>控件</ul>
  <script>
    setTimeout(() => {
      // 插入十万条数据
      const total = 100000
      // 一次插入 20 条，如果觉得性能不好就减少
      const once = 20
      // 渲染数据总共需要几次
      const loopCount = total / once      let countOfRender = 0
      let ul = document.querySelector("ul");
      function add() {
        // 优化性能，插入不会造成回流
        const fragment = document.createDocumentFragment();
        for (let i = 0; i < once; i++) {
          const li = document.createElement("li");
          li.innerText = Math.floor(Math.random() * total);
          fragment.appendChild(li);
        }
        ul.appendChild(fragment);
        countOfRender += 1;
        loop();
      }
      function loop() {
        if (countOfRender < loopCount) {
          window.requestAnimationFrame(add);
        }
      }
      loop();
    }, 0);
  </script></body></html>

**67 希望获取到页面中所有的checkbox怎么做？**

不使用第三方框架

 var domList = document.getElementsByTagName(‘input’)  var checkBoxList = [];  var len = domList.length;　　//缓存到局部变量  while (len--) {　　//使用while的效率会比for循环更高  　　if (domList[len].type == ‘checkbox’) {      　　checkBoxList.push(domList[len]);  　　}  }

**68 怎样添加、移除、移动、复制、创建和查找节点**

创建新节点

createDocumentFragment()    //创建一个DOM片段createElement()   //创建一个具体的元素createTextNode()   //创建一个文本节点

添加、移除、替换、插入

appendChild()      //添加removeChild()      //移除replaceChild()      //替换insertBefore()      //插入

查找

getElementsByTagName()    //通过标签名称getElementsByName()     //通过元素的Name属性的值getElementById()        //通过元素Id，唯一性

**69 正则表达式**

正则表达式构造函数var reg=new RegExp(“xxx”)与正则表达字面量var reg=//有什么不同？匹配邮箱的正则表达式？

- 当使用RegExp()构造函数的时候，不仅需要转义引号（即\”表示”），并且还需要双反斜杠（即\\表示一个\）。使用正则表达字面量的效率更高

邮箱的正则匹配：

var regMail = /^([a-zA-Z0-9_-])+@([a-zA-Z0-9_-])+((.[a-zA-Z0-9_-]{2,3}){1,2})$/;

**70 Javascript中callee和caller的作用？**

- caller是返回一个对函数的引用，该函数调用了当前函数；
- callee是返回正在被执行的function函数，也就是所指定的function对象的正文

那么问题来了？如果一对兔子每月生一对兔子；一对新生兔，从第二个月起就开始生兔子；假定每对兔子都是一雌一雄，试问一对兔子，第n个月能繁殖成多少对兔子？（使用callee完成）

var result=[];   function fn(n){  //典型的斐波那契数列      if(n==1){           return 1;      }else if(n==2){              return 1;      }else{           if(result[n]){                   return result[n];          }else{                  //argument.callee()表示fn()                  result[n]=arguments.callee(n-1)+arguments.callee(n-2);                  return result[n];          }     }  }

**71 window.onload和$(document).ready**

原生JS的window.onload与Jquery的$(document).ready(function(){})有什么不同？如何用原生JS实现Jq的ready方法？

- window.onload()方法是必须等到页面内包括图片的所有元素加载完毕后才能执行。
- $(document).ready()是DOM结构绘制完毕后就执行，不必等到加载完毕

function ready(fn){       if(document.addEventListener) {        //标准浏览器           document.addEventListener('DOMContentLoaded', function() {               //注销事件, 避免反复触发               document.removeEventListener('DOMContentLoaded',arguments.callee, false);               fn();            //执行函数           }, false);       }else if(document.attachEvent) {        //IE           document.attachEvent('onreadystatechange', function() {              if(document.readyState == 'complete') {                  document.detachEvent('onreadystatechange', arguments.callee);                  fn();        //函数执行              }          });      }  };

**72 addEventListener()和attachEvent()的区别**

- addEventListener()是符合W3C规范的标准方法; attachEvent()是IE低版本的非标准方法
- addEventListener()支持事件冒泡和事件捕获; - 而attachEvent()只支持事件冒泡
- addEventListener()的第一个参数中,事件类型不需要添加on; attachEvent()需要添加'on'
- 如果为同一个元素绑定多个事件, addEventListener()会按照事件绑定的顺序依次执行,attachEvent()会按照事件绑定的顺序倒序执行

**73 获取页面所有的checkbox**

var resultArr= [];var input = document.querySelectorAll('input');for( var i = 0; i < input.length; i++ ) {     if( input[i].type == 'checkbox' ) {         resultArr.push( input[i] );     }}//resultArr即中获取到了页面中的所有checkbox

**74 数组去重方法总结**

方法一、利用ES6 Set去重（ES6中最常用）

function unique (arr) {   return Array.from(new Set(arr))

}

var arr = [1,1,'true','true',true,true,15,15,false,false, undefined,undefined, null,null, NaN, NaN,'NaN', 0, 0, 'a', 'a',{},{}];

console.log(unique(arr))  //[1, "true", true, 15, false, undefined, null, NaN, "NaN", 0, "a", {}, {}]

方法二、利用for嵌套for，然后splice去重（ES5中最常用）

function unique(arr){                     for(var i=0; i<arr.length; i++){             for(var j=i+1; j<arr.length; j++){                 if(arr[i]==arr[j]){         //第一个等同于第二个，splice方法删除第二个                     arr.splice(j,1);                     j--;                 }             }         }  return arr;}var arr = [1,1,'true','true',true,true,15,15,false,false, undefined,undefined, null,null, NaN, NaN,'NaN', 0, 0, 'a', 'a',{},{}];console.log(unique(arr))     //[1, "true", 15, false, undefined, NaN, NaN, "NaN", "a", {…}, {…}]     //NaN和{}没有去重，两个null直接消失了

- 双层循环，外层循环元素，内层循环时比较值。值相同时，则删去这个值。
- 想快速学习更多常用的ES6语法

方法三、利用indexOf去重

function unique(arr) {     if (!Array.isArray(arr)) {         console.log('type error!')         return     }     var array = [];     for (var i = 0; i < arr.length; i++) {         if (array .indexOf(arr[i]) === -1) {             array .push(arr[i])         }     }     return array;}var arr = [1,1,'true','true',true,true,15,15,false,false, undefined,undefined, null,null, NaN, NaN,'NaN', 0, 0, 'a', 'a',{},{}];console.log(unique(arr))    // [1, "true", true, 15, false, undefined, null, NaN, NaN, "NaN", 0, "a", {…}, {…}]  //NaN、{}没有去重

新建一个空的结果数组，for 循环原数组，判断结果数组是否存在当前元素，如果有相同的值则跳过，不相同则push进数组

方法四、利用sort()

function unique(arr) {     if (!Array.isArray(arr)) {         console.log('type error!')         return;     }     arr = arr.sort()     var arrry= [arr[0]];     for (var i = 1; i < arr.length; i++) {         if (arr[i] !== arr[i-1]) {             arrry.push(arr[i]);         }     }     return arrry;}var arr = [1,1,'true','true',true,true,15,15,false,false, undefined,undefined, null,null, NaN, NaN,'NaN', 0, 0, 'a', 'a',{},{}];

console.log(unique(arr))// [0, 1, 15, "NaN", NaN, NaN, {…}, {…}, "a", false, null, true, "true", undefined]      //NaN、{}没有去重

利用sort()排序方法，然后根据排序后的结果进行遍历及相邻元素比对

方法五、利用对象的属性不能相同的特点进行去重

function unique(arr) {     if (!Array.isArray(arr)) {         console.log('type error!')         return     }     var arrry= [];      var  obj = {};     for (var i = 0; i < arr.length; i++) {         if (!obj[arr[i]]) {             arrry.push(arr[i])             obj[arr[i]] = 1         } else {             obj[arr[i]]++         }     }     return arrry;}var arr = [1,1,'true','true',true,true,15,15,false,false, undefined,undefined, null,null, NaN, NaN,'NaN', 0, 0, 'a', 'a',{},{}];console.log(unique(arr))//[1, "true", 15, false, undefined, null, NaN, 0, "a", {…}]    //两个true直接去掉了，NaN和{}去重

方法六、利用includes

function unique(arr) {     if (!Array.isArray(arr)) {         console.log('type error!')         return     }     var array =[];     for(var i = 0; i < arr.length; i++) {             if( !array.includes( arr[i]) ) {//includes 检测数组是否有某个值                     array.push(arr[i]);               }     }     return array}var arr = [1,1,'true','true',true,true,15,15,false,false, undefined,undefined, null,null, NaN, NaN,'NaN', 0, 0, 'a', 'a',{},{}];console.log(unique(arr))     //[1, "true", true, 15, false, undefined, null, NaN, "NaN", 0, "a", {…}, {…}]     //{}没有去重

方法七、利用hasOwnProperty

function unique(arr) {     var obj = {};     return arr.filter(function(item, index, arr){         return obj.hasOwnProperty(typeof item + item) ? false : (obj[typeof item + item] = true)     })

} var arr = [1,1,'true','true',true,true,15,15,false,false, undefined,undefined, null,null, NaN, NaN,'NaN', 0, 0, 'a', 'a',{},{}]; console.log(unique(arr))//[1, "true", true, 15, false, undefined, null, NaN, "NaN", 0, "a", {…}]   //所有的都去重了

利用hasOwnProperty 判断是否存在对象属性

方法八、利用filter

function unique(arr) {   return arr.filter(function(item, index, arr) {     //当前元素，在原始数组中的第一个索引==当前索引值，否则返回当前元素     return arr.indexOf(item, 0) === index;   });}var arr = [1,1,'true','true',true,true,15,15,false,false, undefined,undefined, null,null, NaN, NaN,'NaN', 0, 0, 'a', 'a',{},{}];

console.log(unique(arr))//[1, "true", true, 15, false, undefined, null, "NaN", 0, "a", {…}, {…}]

方法九、利用递归去重

function unique(arr) {     var array= arr;     var len = array.length;   array.sort(function(a,b){   //排序后更加方便去重  return a - b;  })   function loop(index){         if(index >= 1){             if(array[index] === array[index-1]){             array.splice(index,1);             }             loop(index - 1);    //递归loop，然后数组去重         }  }  loop(len-1);  return array;}var arr = [1,1,'true','true',true,true,15,15,false,false, undefined,undefined, null,null, NaN, NaN,'NaN', 0, 0, 'a', 'a',{},{}];

console.log(unique(arr))//[1, "a", "true", true, 15, false, 1, {…}, null, NaN, NaN, "NaN", 0, "a", {…}, undefined]

方法十、利用Map数据结构去重

function arrayNonRepeatfy(arr) {  let map = new Map();  let array = new Array();  // 数组用于返回结果  for (let i = 0; i < arr.length; i++) {  if(map .has(arr[i])) {  // 如果有该key值  map .set(arr[i], true);  } else {  map .set(arr[i], false);   // 如果没有该key值  array .push(arr[i]);  }  }  return array ;}  var arr = [1,1,'true','true',true,true,15,15,false,false, undefined,undefined, null,null, NaN, NaN,'NaN', 0, 0, 'a', 'a',{},{}];     console.log(unique(arr))//[1, "a", "true", true, 15, false, 1, {…}, null, NaN, NaN, "NaN", 0, "a", {…}, undefined]

创建一个空Map数据结构，遍历需要去重的数组，把数组的每一个元素作为key存到Map中。由于Map中不会出现相同的key值，所以最终得到的就是去重后的结果

方法十一、利用reduce+includes

function unique(arr){     return arr.reduce((prev,cur) => prev.includes(cur) ? prev : [...prev,cur],[]);}var arr = [1,1,'true','true',true,true,15,15,false,false, undefined,undefined, null,null, NaN, NaN,'NaN', 0, 0, 'a', 'a',{},{}];console.log(unique(arr));// [1, "true", true, 15, false, undefined, null, NaN, "NaN", 0, "a", {…}, {…}]

方法十二、[...new Set(arr)]

[...new Set(arr)]//代码就是这么少----（其实，严格来说并不算是一种，相对于第一种方法来说只是简化了代码）

**75 （设计题）想实现一个对页面某个节点的拖曳？如何做？（使用原生JS）**

- 给需要拖拽的节点绑定mousedown, mousemove, mouseup事件
- mousedown事件触发后，开始拖拽
- mousemove时，需要通过event.clientX和clientY获取拖拽位置，并实时更新位置
- mouseup时，拖拽结束
- 需要注意浏览器边界的情况

**76 Javascript全局函数和全局变量**

全局变量

- Infinity 代表正的无穷大的数值。
- NaN 指示某个值是不是数字值。
- undefined 指示未定义的值。

全局函数

- decodeURI() 解码某个编码的 URI。
- decodeURIComponent() 解码一个编码的 URI 组件。
- encodeURI() 把字符串编码为 URI。
- encodeURIComponent() 把字符串编码为 URI 组件。
- escape() 对字符串进行编码。
- eval() 计算 JavaScript 字符串，并把它作为脚本代码来执行。
- isFinite() 检查某个值是否为有穷大的数。
- isNaN() 检查某个值是否是数字。
- Number() 把对象的值转换为数字。
- parseFloat() 解析一个字符串并返回一个浮点数。
- parseInt() 解析一个字符串并返回一个整数。
- String() 把对象的值转换为字符串。
- unescape() 对由escape() 编码的字符串进行解码

**77 使用js实现一个持续的动画效果**

定时器思路

var e = document.getElementById('e')var flag = true;var left = 0;setInterval(() => {     left == 0 ? flag = true : left == 100 ? flag = false : ''     flag ? e.style.left = ` ${left++}px` : e.style.left = ` ${left--}px`}, 1000 / 60)

requestAnimationFrame

//兼容性处理window.requestAnimFrame = (function(){     return window.requestAnimationFrame       ||            window.webkitRequestAnimationFrame ||            window.mozRequestAnimationFrame    ||            function(callback){                 window.setTimeout(callback, 1000 / 60);            };})();var e = document.getElementById("e");var flag = true;var left = 0;function render() {     left == 0 ? flag = true : left == 100 ? flag = false : '';     flag ? e.style.left = ` ${left++}px` :         e.style.left = ` ${left--}px`;}(function animloop() {     render();     requestAnimFrame(animloop);})();

使用css实现一个持续的动画效果

animation:mymove 5s infinite;@keyframes mymove {     from {top:0px;}     to {top:200px;}}

- animation-name 规定需要绑定到选择器的 keyframe名称。
- animation-duration 规定完成动画所花费的时间，以秒或毫秒计。
- animation-timing-function 规定动画的速度曲线。
- animation-delay 规定在动画开始之前的延迟。
- animation-iteration-count 规定动画应该播放的次数。
- animation-direction 规定是否应该轮流反向播放动画

**78 封装一个函数，参数是定时器的时间，.then执行回调函数**

function sleep (time) {     return new Promise((resolve) => setTimeout(resolve, time));}

**79 怎么判断两个对象相等？**

obj={     a:1,     b:2}obj2={     a:1,     b:2}obj3={     a:1,     b:'2'}

可以转换为字符串来判断

JSON.stringify(obj)==JSON.stringify(obj2);//trueJSON.stringify(obj)==JSON.stringify(obj3);//false

**80 项目做过哪些性能优化？**

- 减少 HTTP 请求数
- 减少 DNS 查询
- 使用 CDN
- 避免重定向
- 图片懒加载
- 减少 DOM 元素数量
- 减少DOM 操作
- 使用外部 JavaScript 和 CSS
- 压缩 JavaScript 、 CSS 、字体、图片等
- 优化 CSS Sprite
- 使用 iconfont
- 字体裁剪
- 多域名分发划分内容到不同域名
- 尽量减少 iframe 使用
- 避免图片 src 为空
- 把样式表放在link 中
- 把JavaScript放在页面底部

**81 浏览器缓存**

浏览器缓存分为强缓存和协商缓存。当客户端请求某个资源时，获取缓存的流程如下

- 先根据这个资源的一些 http header 判断它是否命中强缓存，如果命中，则直接从本地获取缓存资源，不会发请求到服务器；
- 当强缓存没有命中时，客户端会发送请求到服务器，服务器通过另一些request header验证这个资源是否命中协商缓存，称为http再验证，如果命中，服务器将请求返回，但不返回资源，而是告诉客户端直接从缓存中获取，客户端收到返回后就会从缓存中获取资源；
- 强缓存和协商缓存共同之处在于，如果命中缓存，服务器都不会返回资源； 区别是，强缓存不对发送请求到服务器，但协商缓存会。
- 当协商缓存也没命中时，服务器就会将资源发送回客户端。
- 当 ctrl+f5 强制刷新网页时，直接从服务器加载，跳过强缓存和协商缓存；
- 当 f5刷新网页时，跳过强缓存，但是会检查协商缓存；

强缓存

- Expires（该字段是 http1.0 时的规范，值为一个绝对时间的 GMT 格式的时间字符串，代表缓存资源的过期时间）
- Cache-Control:max-age（该字段是 http1.1的规范，强缓存利用其 max-age 值来判断缓存资源的最大生命周期，它的值单位为秒）

协商缓存

- `Last-Modified`（值为资源最后更新时间，随服务器response返回）
- `If-Modified-Since`（通过比较两个时间来判断资源在两次请求期间是否有过修改，如果没有修改，则命中协商缓存）
- `ETag`（表示资源内容的唯一标识，随服务器response返回）
- `If-None-Match`（服务器通过比较请求头部的If-None-Match与当前资源的ETag是否一致来判断资源是否在两次请求之间有过修改，如果没有修改，则命中协商缓存）

**82` WebSocket`**

由于` http `存在一个明显的弊端（消息只能有客户端推送到服务器端，而服务器端不能主动推送到客户端），导致如果服务器如果有连续的变化，这时只能使用轮询，而轮询效率过低，并不适合。于是 WebSocket被发明出来

相比与` http `具有以下有点

- 支持双向通信，实时性更强；
- 可以发送文本，也可以二进制文件；
- 协议标识符是` ws`，加密后是` wss` ；
- 较少的控制开销。连接创建后，`ws`客户端、服务端进行数据交换时，协议控制的数据包头部较小。在不包含头部的情况下，服务端到客户端的包头只有2~10字节（取决于数据包长度），客户端到服务端的的话，需要加上额外的4字节的掩码。而HTTP协议每次通信都需要携带完整的头部；
- 支持扩展。`ws`协议定义了扩展，用户可以扩展协议，或者实现自定义的子协议。（比如支持自定义压缩算法等）
- 无跨域问题。

实现比较简单，服务端库如 `socket.io`、`ws`，可以很好的帮助我们入门。而客户端也只需要参照 api 实现即可

**83 尽可能多的说出你对 Electron 的理解**

最最重要的一点，electron 实际上是一个套了 `Chrome `的` nodeJS`程序

所以应该是从两个方面说开来

- `Chrome `（无各种兼容性问题）；
- `NodeJS`（`NodeJS `能做的它也能做）

**84 深浅拷贝**

浅拷贝

- `Object.assign`
- 或者展开运算符

深拷贝

- 可以通过` JSON.parse(JSON.stringify(object))` 来解决

```js
let a = {     
    age: 1,     
    jobs: 
   {         
       first: 'FE'
   }
}
let b = JSON.parse(JSON.stringify(a))
a.jobs.first = 'native'
console.log(b.jobs.first) // FE
```



该方法也是有局限性的

- 会忽略 undefined
- 不能序列化函数
- 不能解决循环引用的对象

**85 防抖/节流**

防抖

在滚动事件中需要做个复杂计算或者实现一个按钮的防二次点击操作。可以通过函数防抖动来实现

```js
// 使用 underscore 的源码来解释防抖动/**

- underscore 防抖函数，返回函数连续调用时，空闲时间必须大于或等于 wait，func 才会执行
  *
- @param  {function} func        回调函数
- @param  {number}   wait        表示时间窗口的间隔
- @param  {boolean}  immediate   设置为ture时，是否立即调用函数
- @return {function}             返回客户调用函数
  */_.debounce = function(func, wait, immediate) {
      var timeout, args, context, timestamp, result;

    var later = function() {
      // 现在和上一次时间戳比较
      var last = _.now() - timestamp;
      // 如果当前间隔时间少于设定时间且大于0就重新设置定时器
      if (last < wait && last >= 0) {
        timeout = setTimeout(later, wait - last);
      } else {
        // 否则的话就是时间到了执行回调函数
        timeout = null;
        if (!immediate) {
          result = func.apply(context, args);
          if (!timeout) context = args = null;
        }
      }
    };

    return function() {
      context = this;
      args = arguments;
      // 获得时间戳
      timestamp = _.now();
      // 如果定时器不存在且立即执行函数
      var callNow = immediate && !timeout;
      // 如果定时器不存在就创建一个
      if (!timeout) timeout = setTimeout(later, wait);
      if (callNow) {
        // 如果需要立即执行函数的话 通过 apply 执行
        result = func.apply(context, args);
        context = args = null;
      }

      return result;
    };
  };
```



整体函数实现

对于按钮防点击来说的实现

- 开始一个定时器，只要我定时器还在，不管你怎么点击都不会执行回调函数。一旦定时器结束并设置为 null，就可以再次点击了
- 对于延时执行函数来说的实现：每次调用防抖动函数都会判断本次调用和之前的时间间隔，如果小于需要的时间间隔，就会重新创建一个定时器，并且定时器的延时为设定时间减去之前的时间间隔。一旦时间到了，就会执行相应的回调函数

节流

防抖动和节流本质是不一样的。防抖动是将多次执行变为最后一次执行，节流是将多次执行变成每隔一段时间执行

```js
/**

- underscore 节流函数，返回函数连续调用时，func 执行频率限定为 次 / wait
  *
- @param  {function}   func      回调函数
- @param  {number}     wait      表示时间窗口的间隔
- @param  {object}     options   如果想忽略开始函数的的调用，传入{leading: false}。
- 如果想忽略结尾函数的调用，传入{trailing: false}
- 两者不能共存，否则函数不能执行
- @return {function}             返回客户调用函数   
  */_.throttle = function(func, wait, options) {
      var context, args, result;
      var timeout = null;
      // 之前的时间戳
      var previous = 0;
      // 如果 options 没传则设为空对象
      if (!options) options = {};
      // 定时器回调函数
      var later = function() {
        // 如果设置了 leading，就将 previous 设为 0
        // 用于下面函数的第一个 if 判断
        previous = options.leading === false ? 0 : _.now();
        // 置空一是为了防止内存泄漏，二是为了下面的定时器判断
        timeout = null;
        result = func.apply(context, args);
        if (!timeout) context = args = null;
      };
      return function() {
        // 获得当前时间戳
        var now = _.now();
        // 首次进入前者肯定为 true
     // 如果需要第一次不执行函数
     // 就将上次时间戳设为当前的
        // 这样在接下来计算 remaining 的值时会大于0
        if (!previous && options.leading === false) previous = now;
        // 计算剩余时间
        var remaining = wait - (now - previous);
        context = this;
        args = arguments;
        // 如果当前调用已经大于上次调用时间 + wait
        // 或者用户手动调了时间
      // 如果设置了 trailing，只会进入这个条件
     // 如果没有设置 leading，那么第一次会进入这个条件
     // 还有一点，你可能会觉得开启了定时器那么应该不会进入这个 if 条件了
     // 其实还是会进入的，因为定时器的延时
     // 并不是准确的时间，很可能你设置了2秒
     // 但是他需要2.2秒才触发，这时候就会进入这个条件
        if (remaining <= 0 || remaining > wait) {
          // 如果存在定时器就清理掉否则会调用二次回调
          if (timeout) {
            clearTimeout(timeout);
            timeout = null;
          }
          previous = now;
          result = func.apply(context, args);
          if (!timeout) context = args = null;
        } else if (!timeout && options.trailing !== false) {
          // 判断是否设置了定时器和 trailing
       // 没有的话就开启一个定时器
          // 并且不能不能同时设置 leading 和 trailing
          timeout = setTimeout(later, remaining);
        }
        return result;
      };
    };
```



**86 谈谈变量提升？**

当执行 JS 代码时，会生成执行环境，只要代码不是写在函数中的，就是在全局执行环境中，函数中的代码会产生函数执行环境，只此两种执行环境

- 接下来让我们看一个老生常谈的例子，var

b() // call bconsole.log(a) // undefinedvar a = 'Hello world'function b() {     console.log('call b')}

变量提升

这是因为函数和变量提升的原因。通常提升的解释是说将声明的代码移动到了顶部，这其实没有什么错误，便于大家理解。但是更准确的解释应该是：在生成执行环境时，会有两个阶段。第一个阶段是创建的阶段，JS 解释器会找出需要提升的变量和函数，并且给他们提前在内存中开辟好空间，函数的话会将整个函数存入内存中，变量只声明并且赋值为 undefined，所以在第二个阶段，也就是代码执行阶段，我们可以直接提前使用

在提升的过程中，相同的函数会覆盖上一个函数，并且函数优先于变量提升

b() // call b secondfunction b() {     console.log('call b fist')}function b() {     console.log('call b second')}var b = 'Hello world'

复制代码var 会产生很多错误，所以在 ES6中引入了 let。let 不能在声明前使用，但是这并不是常说的 let 不会提升，let 提升了，在第一阶段内存也已经为他开辟好了空间，但是因为这个声明的特性导致了并不能在声明前使用

**87 什么是单线程，和异步的关系**

- 单线程 - 只有一个线程，只能做一件事
- 原因 - 避免 DOM 渲染的冲突

- - 浏览器需要渲染 DOM
  - JS 可以修改 DOM 结构
  - JS 执行的时候，浏览器 DOM 渲染会暂停
  - 两段 JS 也不能同时执行（都修改 DOM 就冲突了）
  - webworker 支持多线程，但是不能访问 DOM

- 解决方案 - 异步

**88 是否用过 jQuery 的 Deferred**

![img](js考点.assets/30fbdcc1f1cc.png)

![img](js考点.assets/b726f5341f7d.png)

![img](js考点.assets/861eced36a45.png)

![img](js考点.assets/2d725f2b1e79.png)

![img](js考点.assets/67a6859cf8cb.png)

![img](js考点.assets/b83118b10829.png)

![img](js考点.assets/44771c6b30ab.png)

 

![img](js考点.assets/463132d1572a.png)

![img](js考点.assets/d6f7caf8b27c.png)

![img](js考点.assets/7f684e99e6cb.png)

**89 前端面试之hybrid**

[http://blog.poetries.top/2018/10/20/fe-interview-hybrid/](https://www.v5ant.com/go/?url=aHR0cDovL2Jsb2cucG9ldHJpZXMudG9wLzIwMTgvMTAvMjAvZmUtaW50ZXJ2aWV3LWh5YnJpZC8=)

**90 前端面试之组件化**

[http://blog.poetries.top/2018/10/20/fe-interview-component/](https://www.v5ant.com/go/?url=aHR0cDovL2Jsb2cucG9ldHJpZXMudG9wLzIwMTgvMTAvMjAvZmUtaW50ZXJ2aWV3LWNvbXBvbmVudC8=)

**91 前端面试之MVVM浅析**

[http://blog.poetries.top/2018/10/20/fe-interview-mvvm/](https://www.v5ant.com/go/?url=aHR0cDovL2Jsb2cucG9ldHJpZXMudG9wLzIwMTgvMTAvMjAvZmUtaW50ZXJ2aWV3LW12dm0v)

**92 实现效果，点击容器内的图标，图标边框变成border 1px solid red，点击空白处重置**

const box = document.getElementById('box');function isIcon(target) {   return target.className.includes('icon');}box.onClick = function(e) {   e.stopPropagation();   const target = e.target;   if (isIcon(target)) {     target.style.border = '1px solid red';   }}const doc = document;doc.onclick = function(e) {   const children = box.children;   for(let i; i < children.length; i++) {     if (isIcon(children[i])) {       children[i].style.border = 'none';     }   }}

**93 请简单实现双向数据绑定****mvvm**

<input id="input"/>

const data = {};const input = document.getElementById('input');Object.defineProperty(data, 'text', {   set(value) {     input.value = value;     this.value = value;   }});input.onChange = function(e) {   data.text = e.target.value;}

**94 实现Storage，使得该对象为单例，并对****localStorage****进行封装设置值setItem(key,value)和getItem(key)**

var instance = null;class Storage {   static getInstance() {     if (!instance) {       instance = new Storage();     }     return instance;   }   setItem = (key, value) => localStorage.setItem(key, value),   getItem = key => localStorage.getItem(key)}

**95 说说****event loop**

首先，js是单线程的，主要的任务是处理用户的交互，而用户的交互无非就是响应DOM的增删改，使用事件队列的形式，一次事件循环只处理一个事件响应，使得脚本执行相对连续，所以有了事件队列，用来储存待执行的事件，那么事件队列的事件从哪里被push进来的呢。那就是另外一个线程叫事件触发线程做的事情了，他的作用主要是在定时触发器线程、异步HTTP请求线程满足特定条件下的回调函数push到事件队列中，等待js引擎空闲的时候去执行，当然js引擎执行过程中有优先级之分，首先js引擎在一次事件循环中，会先执行js线程的主任务，然后会去查找是否有微任务microtask（promise），如果有那就优先执行微任务，如果没有，在去查找宏任务macrotask（setTimeout、setInterval）进行执行

**96 说说事件流**

事件流分为两种，捕获事件流和冒泡事件流

- 捕获事件流从根节点开始执行，一直往子节点查找执行，直到查找执行到目标节点
- 冒泡事件流从目标节点开始执行，一直往父节点冒泡查找执行，直到查到到根节点

事件流分为三个阶段，一个是捕获节点，一个是处于目标节点阶段，一个是冒泡阶段

**97 为什么****canvas****的图片为什么过有跨域问题**

**98 我现在有一个****canvas****，上面随机布着一些黑块，请实现方法，计算canvas上有多少个黑块**

https://www.jianshu.com/p/f54d265f7aa4

**99 请手写实现一个****promise**

https://segmentfault.com/a/1190000013396601

**100 说说从输入URL到看到页面发生的全过程，越详细越好**

- 首先浏览器主进程接管，开了一个下载线程。
- 然后进行HTTP请求（DNS查询、IP寻址等等），中间会有三次捂手，等待响应，开始下载响应报文。
- 将下载完的内容转交给Renderer进程管理。
- Renderer进程开始解析css rule tree和dom tree，这两个过程是并行的，所以一般我会把link标签放在页面顶部。
- 解析绘制过程中，当浏览器遇到link标签或者script、img等标签，浏览器会去下载这些内容，遇到时候缓存的使用缓存，不适用缓存的重新下载资源。
- css rule tree和dom tree生成完了之后，开始合成render tree，这个时候浏览器会进行layout，开始计算每一个节点的位置，然后进行绘制。
- 绘制结束后，关闭TCP连接，过程有四次挥手

**101 描述一下****this**

this，函数执行的上下文，可以通过apply，call，bind改变this的指向。对于匿名函数或者直接调用的函数来说，this指向全局上下文（浏览器为window，NodeJS为global），剩下的函数调用，那就是谁调用它，this就指向谁。当然还有es6的箭头函数，箭头函数的指向取决于该箭头函数声明的位置，在哪里声明，this就指向哪里

**102 说一下浏览器的缓存机制**

浏览器缓存机制有两种，一种为强缓存，一种为协商缓存

- 对于强缓存，浏览器在第一次请求的时候，会直接下载资源，然后缓存在本地，第二次请求的时候，直接使用缓存。
- 对于协商缓存，第一次请求缓存且保存缓存标识与时间，重复请求向服务器发送缓存标识和最后缓存时间，服务端进行校验，如果失效则使用缓存

协商缓存相关设置

- Exprires：服务端的响应头，第一次请求的时候，告诉客户端，该资源什么时候会过期。Exprires的缺陷是必须保证服务端时间和客户端时间严格同步。
- Cache-control：max-age：表示该资源多少时间后过期，解决了客户端和服务端时间必须同步的问题，
- If-None-Match/ETag：缓存标识，对比缓存时使用它来标识一个缓存，第一次请求的时候，服务端会返回该标识给客户端，客户端在第二次请求的时候会带上该标识与服务端进行对比并返回If-None-Match标识是否表示匹配。
- Last-modified/If-Modified-Since：第一次请求的时候服务端返回Last-modified表明请求的资源上次的修改时间，第二次请求的时候客户端带上请求头If-Modified-Since，表示资源上次的修改时间，服务端拿到这两个字段进行对比

**103 现在要你完成一个Dialog组件，说说你设计的思路？它应该有什么功能？**

- 该组件需要提供hook指定渲染位置，默认渲染在body下面。
- 然后改组件可以指定外层样式，如宽度等
- 组件外层还需要一层mask来遮住底层内容，点击mask可以执行传进来的onCancel函数关闭Dialog。
- 另外组件是可控的，需要外层传入visible表示是否可见。
- 然后Dialog可能需要自定义头head和底部footer，默认有头部和底部，底部有一个确认按钮和取消按钮，确认按钮会执行外部传进来的onOk事件，然后取消按钮会执行外部传进来的onCancel事件。
- 当组件的visible为true时候，设置body的overflow为hidden，隐藏body的滚动条，反之显示滚动条。
- 组件高度可能大于页面高度，组件内部需要滚动条。
- 只有组件的visible有变化且为ture时候，才重渲染组件内的所有内容

**104** **caller****和****callee****的区别**

callee

caller返回一个函数的引用，这个函数调用了当前的函数。

使用这个属性要注意

- 这个属性只有当函数在执行时才有用
- 如果在javascript程序中，函数是由顶层调用的，则返回null

functionName.caller: functionName是当前正在执行的函数。

function a() {   console.log(a.caller)}

callee

callee放回正在执行的函数本身的引用，它是arguments的一个属性

使用callee时要注意:

- 这个属性只有在函数执行时才有效
- 它有一个length属性，可以用来获得形参的个数，因此可以用来比较形参和实参个数是否一致，即比较arguments.length是否等于arguments.callee.length
- 它可以用来递归匿名函数。

function a() {   console.log(arguments.callee)}

**105 ajax、axios、fetch区别**

jQuery ajax

$.ajax({    type: 'POST',    url: url,    data: data,    dataType: dataType,    success: function () {},    error: function () {}});

优缺点：

- 本身是针对MVC的编程,不符合现在前端MVVM的浪潮
- 基于原生的XHR开发，XHR本身的架构不清晰，已经有了fetch的替代方案
- JQuery整个项目太大，单纯使用ajax却要引入整个JQuery非常的不合理（采取个性化打包的方案又不能享受CDN服务）

axios

axios({     method: 'post',     url: '/user/12345',     data: {         firstName: 'Fred',         lastName: 'Flintstone'     }}).then(function (response) {     console.log(response);}).catch(function (error) {     console.log(error);});

优缺点：

- 从浏览器中创建 XMLHttpRequest
- 从 node.js 发出 http 请求
- 支持 Promise API
- 拦截请求和响应
- 转换请求和响应数据
- 取消请求
- 自动转换JSON数据
- 客户端支持防止CSRF/XSRF

fetch

try {   let response = await fetch(url);   let data = response.json();   console.log(data);} catch(e) {   console.log("Oops, error", e);}

优缺点：

- fetcht只对网络请求报错，对400，500都当做成功的请求，需要封装去处理
- fetch默认不会带cookie，需要添加配置项
- fetch不支持abort，不支持超时控制，使用setTimeout及Promise.reject的实现的超时控制并不能阻止请求过程继续在后台运行，造成了量的浪费
- fetch没有办法原生监测请求的进度，而XHR可以