# JS

<a name="5e3cd849"></a>
## 作用域&闭包

作用域是指一个变量的应用范围-  全局作用域和函数作用域

作用域 (Scope)   和变量提升

全局作用域<br />所有函数的最外层称为全局作用域，全局作用域下定义的值是全局都可以访问到<br />在页面打开时创建，在页面关闭时销毁

变量的声明提前<br />函数声明也会提前<br />函数表达式声明不会提前

函数作用域<br />调用函数时创建函数作用域，函数执行完毕后，作用域销毁<br />函数操作一个变量的时候，首先从自身的作用域寻找，如果有就近使用，没有再向上一级作用寻找，再找不到向全局作用域寻找，找不到报错

全局变量和局部变量

函数内部可以读取函数外部的全局变量 <br />函数外部不能读取函数内部的局部变量


fuction f1 () {<br />let n = 999;<br />function f2() {<br />console.log(n);<br />}<br />return f2;<br />}<br />let result = f1();<br />result = 999;

闭包作用： 1、 读取函数内部的变量<br />     2、让这些变量的值始终保持在内存中<br />





闭包就是能够读取其他函数内部变量的函数。<br />由于在Javascript语言中，只有函数内部的子函数才能读取局部变量，因此可以把闭包简单理解成"定义在一个函数内部的函数"。<br /><br />本质上，闭包就是将函数内部和函数外部连接起来的一座桥梁。<br /><br /><br /><br />
<a name="d41d8cd9"></a>
### 


<a name="b1449413"></a>
## 对象

for  in  遍历对象键值和属性 

for( let key in objs) {<br />alert(key);    键值<br />alert(objs[key]);  属性<br />}<br />关于遍历 排序 ，如果是整数的话，按大小排序 从小到大；不是整数的话，按创建的顺序排序 

总结：<br />对象是具有一些特殊特性的关联数组。<br />他们存储键值对：
* 属性的键必须是字符串或者符号（通常是字符串）。
* 值可以是任何类型。

我们可以用下面的方法获取属性：
* 点符号: `obj.property`。
* 方括号 `obj["property"]`，方括号中可以使用变量 `obj[varWithKey]`。

其他操作：
* 删除属性：`delete obj.prop`。
* 检查属性是否存在：`"key" in obj`。
* 遍历对象：`for(let key in obj)` 循环。

对象根据引用来赋值或者复制。换句话说，变量存的不是对象的"值"，而是值的 “引用”（内存地址）。 所以复制变量或者传递变量到方法中只是复制了对象的引用。 所有的引用操作（像增加，删除属性）都作用于同一个对象。<br />深拷贝的话我们可以使用 `Object.assign` 或者 [_.cloneDeep(obj)](https://lodash.com/docs#cloneDeep)。<br />我们在这一章学习的叫做“基本对象” — 对象。<br />JavaScript 中还有很多其他类型的对象：
* `Array` 存储有序数据集合。
* `Date` 存储时间日期。
* `Error` 存储错误信息
* …等等。

他们有一些特别的特性，我们将在后面学习到。有时候大家说“数组类型”，“时间类型”，他们都属于对象类型的一种，都以不同的方式对对象类型做了一些扩展。

垃圾回收<br />主要需要掌握的东西：
* 垃圾回收是自动完成的，我们不能强制执行或是阻止执行。
* 当对象是可达状态时，它在内存中是可达的。
* 被引用与可访问（从一个根）不同：一组相互连接的对象可能整体都无法访问。



<a name="81b1781e"></a>
#### 构造函数
主要目的 — 实现可重用的对象创建代码

构造函数和操作符 "new"<br />常规的 `{...}` 语法允许创建一个对象。但是我们经常需要创建许多类似的对象，例如多个用户或菜单项等等。<br />这可以使用构造函数和 `"new"` 操作符。<br />[构造函数](https://zh.javascript.info/constructor-new#gou-zao-han-shu)<br />构造函数在技术上是常规函数。不过有两个约定：
1. 他们首先用大写字母命名。
1. 它们只能用 `"new"` 操作符来执行。

通常，构造函数没有 `return` 语句。他们的任务是将所有必要的东西写入 `this`，并自动转换。<br />但是，如果有 `return` 语句，那么规则很简单：
* 如果 `return` 对象，则返回它，而不是 `this`。
* 如果 `return` 一个原函数，则忽略。

let obj = {} <br />function A() {return obj};<br />function B() {return obj};<br />这个时候函数返回的是对象，而不是this<br />new A() == new B()  // true;



    // 创建一个构造函数，专门用来创建Person对象<br />function Person(name, age, gender) {<br />this.name = name;<br />this.age = age;<br />this.gender = gender;<br />this.sayName = function() {<br />alert(this.name);<br />};<br />}

// 创建一个构造函数，专门用来创建 Dog 对象<br />function Dog() {}

var per = new Person("孙悟空", 18, "男");<br />var per2 = new Person("玉兔精", 16, "女");<br />var per3 = new Person("奔波霸", 38, "男");

var dog = new Dog();

构造函数就是一个普通的函数，创建方式和普通函数没有区别，不同的是构造函数习惯上首字母大写。<br />构造函数和普通函数的区别就是**调用方式**的不同：普通函数是直接调用，而构造函数需要使用new关键字来调<br />用。
* 构造函数或简言之，就是常规函数，但构造函数有个共同的约定，命名它们首字母要大写。
* 构造函数只能使用 `new` 来调用。这样的调用意味着在开始时创建空的 `this`，并在最后返回填充的对象。

我们可以使用构造函数来创建多个类似的对象。<br />JavaScript 为许多内置的对象提供了构造函数：比如日期 Date，设置集合 Set 以及其他我们计划学习的内容。

<a name="d41d8cd9-1"></a>
## 
<a name="185f7bf6"></a>
## 数据类型

- **基本数据类型（值类型）**：String 字符串、Number 数值、Boolean 布尔值、Null 空值、Undefined 未定义。

- **引用数据类型（引用类型）**：Object 对象

<a name="1460fc73"></a>
### 数字类型
在 JavaScript 中，我们通过在数字后附加字母 “e” 来缩短数字，并指定零的数量来计数<br />let num = 3e5;  // 300000;<br />let num = 3e-5  // 0.00003;  <br /><br />
<a name="0fb49f2a"></a>
#### 十六进制，二进制 ，八进制

toString(base);  转换进制

let num = 255;<br />num.toString(16) ; //  ff<br />num.toString(2);   // 11111111

<a name="7a2f5f41"></a>
#### 四舍五入
使用数字时最常用的操作之一是四舍五入。<br />有几个内置函数用于舍入：<br />`Math.floor`向下舍入：`3.1` 变成 `3`，`-1.1` 变成 `-2`。<br />`Math.ceil`向上舍入：`3.1` 变成 `4`，`-1.1` 变成 `-1`。<br />`Math.round`向最近的整数舍入：`3.1` 变成 `3`, 3.6`变成`4`，`-1.1`变成`-1`。<br />`Math.trunc`（IE 浏览器不支持这个方法）删除小数点后的所有内容而不舍入：`3.1` 变成 `3`，`-1.1` 变成 `-1`。

不精准计算 <br />toFixed
```
let sum = 0.1 + 0.2;
alert( sum.toFixed(2) ); // 0.30
```

<a name="197e6f41"></a>
#### ParseInt  和 ParseFloat
`parseInt` 和 `parseFloat` 的作用。<br />他们从字符串中“读出”一个数字，直到他们可以。如果发生错误，则返回收集的数字。函数 `parseInt` 返回一个整数，而 `parseFloat` 将返回一个浮点数：

`parseInt()` 函数有一个可选的第二个参数。它指定了数字系统的基础，因此 `parseInt` 还可以解析十六进制数字，二进制数字等字符串：
```javascript
alert( parseInt('0xff', 16) ); // 255
alert( parseInt('ff', 16) ); // 255, without 0x also works
alert( parseInt('2n9c', 36) ); // 123456
```






<br /><br />象。



<a name="this"></a>
## this

解析器在调用函数每次都会向函数内部传递进一个隐含的参数，这个隐含的参数就是this，this指向的是一个对象，这个对象我们称为函数执行的 上下文对象。

根据函数的调用方式的不同，this会指向不同的对象：【重要】<br />- 1.以函数的形式调用时，this永远都是window。比如`fun();`相当于`window.fun();`<br />- 2.以方法的形式调用时，this是调用方法的那个对象<br />- 3.以构造函数的形式调用时，this是新创建的那个对象<br />- 4.使用call和apply调用时，this是指定的那个对象

this 是在运行时求值的。它可以是任何值<br />箭头函数没有自己的this <br />总结：
* 存储在对象中函数称之为『方法』。
* 对象执行方法进行『操作』，比如 object.doSomething()。
* 方法可以将该对象引用为 this。

this 的值是在运行时求值的。
* 函数声明使用的 this 只有等到调用时才会有值。
* 函数可以在对象之间进行共用。
* 当函数使用『方法』语法 object.method() 调用时，调用过程中的 this 总是指向 object。

请注意箭头函数有些特别：它们没有 this。在箭头函数内部访问的都是来自外部的 this 值。
<a name="d86f8699"></a>
### 箭头函数

* `arr.forEach(func)` – `forEach` 对每个数组元素执行 `func`。
* `setTimeout(func)` – `func` 由内置调度程序执行。

总结：<br />箭头函数：
* 没有 `this`。
* 没有 `arguments`。
* 不能使用 `new`。
* （他们也没有 `super`，我们将在这一章 [类继承和 super](https://zh.javascript.info/class-inheritance) 研究）。



<a name="AJAX"></a>
## AJAX
简单总结5步

document.getElementById('btn').onclick = () => {<br />//（1）创建异步对象<br />let ajaxObj = new XMLHttpRequest();<br />// （2）设置请求参数 请求方法get/post,请求URL, 异步<br />ajaxObj.open('GET','ajax/getajax.php',true);<br />//（3）发送请求<br />ajaxObj.send();<br />////（4）注册事件。 onreadystatechange事件，状态改变时就会调用。<br />//如果要在数据完整请求回来的时候才调用，我们需要手动写一些判断的逻辑。<br />ajaxObj.onreadystatechange = function() {<br />// 为了数据返回 ，我们一般判断两个值<br />if(ajaxObj.readyState == 4 && ajaxObj.status == 200) {<br />console.log('数据返回成功');<br />// // 5.在注册的事件中 获取 返回的保存在 异步对象的 属性中<br />console.log(ajaxObj.responseText);<br />// 修改页面的显示<br />document.querySelector('h1').innerHTML = ajaxObj.responseText;<br />}<br />}<br />}


AJAX = 异步 JavaScript 和 XML。<br />AJAX 是一种用于创建快速动态网页的技术。<br />通过在后台与服务器进行少量数据交换，AJAX 可以使网页实现异步更新。这意味着可以在不重新加载整个网页的情况下，对网页的某部分进行更新。

AJAX 是用来与服务器交换数据并更新部分网页的艺术

XMLHTTPRequest 是AJAX 的基础 <br />XMLHTTPRequest 用于在后台与服务器交换数据<br />这意味着可以在不重新加载整个网页的情况下，对网页的某部分进行更新
<a name="9ed87761"></a>
### 创建 XMLHttpRequest 对象
所有现代浏览器（IE7+、Firefox、Chrome、Safari 以及 Opera）均内建 XMLHttpRequest 对象。

创建方法 variable=new XMLHttpRequest();<br />为了应对所有的现代浏览器，包括 IE5 和 IE6，请检查浏览器是否支持 XMLHttpRequest 对象。如果支持，则创建 XMLHttpRequest 对象。如果不支持，则创建 ActiveXObject ：<br />var xmlhttp;<br />if (window.XMLHttpRequest)<br />  {// code for IE7+, Firefox, Chrome, Opera, Safari<br />  xmlhttp=new XMLHttpRequest();<br />  }<br />else<br />  {// code for IE6, IE5<br />  xmlhttp=new ActiveXObject("Microsoft.XMLHTTP");<br />  }

<a name="0660ccca"></a>
### 向服务器发送请求
我们将请求发送到服务器端 用到XMLHttpRequest()对象 的open()和send()方法<br />![image.png](https://intranetproxy.alipay.com/skylark/lark/0/2019/png/116060/1551857274613-7d6b6aaf-7b02-419b-adc8-4804e6c6abb8.png#align=left&display=inline&height=339&name=image.png&originHeight=339&originWidth=631&size=26272&status=done&width=631)




<a name="a7625511"></a>
### url - 服务器上的文件
open() 方法的 url 参数是服务器上文件的地址：
<a name="f998bbea"></a>
### 异步 - True 或 False？
AJAX 指的是异步 JavaScript 和 XML（Asynchronous JavaScript and XML）。<br />XMLHttpRequest 对象如果要用于 AJAX 的话，其 open() 方法的 async 参数必须设置为 true：

<a name="bec8fc88"></a>
### Async = false
如需使用 async=false，请将 open() 方法中的第三个参数改为 false：<br />xmlhttp.open("GET","test1.txt",false);<br />我们不推荐使用 async=false，但是对于一些小型的请求，也是可以的。<br />请记住，JavaScript 会等到服务器响应就绪才继续执行。如果服务器繁忙或缓慢，应用程序会挂起或停止。<br />注释：当您使用 async=false 时，请不要编写 onreadystatechange 函数 - 把代码放到 send() 语句后面即可：

<a name="9ad54eff"></a>
### 服务器响应
如需获得来自服务器的响应，请使用 XMLHttpRequest 对象的 responseText 或 responseXML 属性。<br />
<br />![image.png](https://intranetproxy.alipay.com/skylark/lark/0/2019/png/116060/1551860876716-0c62c808-66b6-4daf-9135-e42a91614ec0.png#align=left&display=inline&height=113&name=image.png&originHeight=113&originWidth=785&size=9605&status=done&width=785)
<a name="8267985b"></a>
### onreadystatechange 事件
当请求被发送到服务器时，我们需要执行一些基于响应的任务。<br />每当 readyState 改变时，就会触发 onreadystatechange 事件。<br />readyState 属性存有 XMLHttpRequest 的状态信息。<br />![image.png](https://intranetproxy.alipay.com/skylark/lark/0/2019/png/116060/1551865720789-c40931c2-0610-41a1-bea8-c1daa2429b39.png#align=left&display=inline&height=300&name=image.png&originHeight=300&originWidth=686&size=26308&status=done&width=686)




<a name="3418cae3"></a>
## let  和 const 
let 关键字来实现块级作用域。<br />{<br />let x =1;<br />}<br /> let 关键字声明的全局作用域变量不属于 window 对象:<br />在相同的作用域或块级作用域中，不能使用 let 关键字来重置 var 关键字声明的变量:<br />在相同的作用域或块级作用域中，不能使用 let 关键字来重置 let 关键字声明的变量:<br />let 关键字定义的变量则不可以在使用后声明，也就是变量需要先声明再使用。

const 用于声明一个或多个常量，声明时必须进行初始化，且初始化后值不可再修改：<br />const PI = 3.14;

const 的本质: const 定义的变量并非常量，并非不可变，它定义了一个常量引用一个值。使用 const 定义的对象或者数组，其实是可变的。<br />const person = { name:'DrewB',age:33};<br />person.age:32;

<a name="JSON"></a>
## JSON
* JSON 英文全称 JavaScript Object Notation
* 一种轻量级的数据交换格式
* 独立语言，易于理解

json用于存储和传输格式的数据<br />通常用于服务端向网页传输的数据

json 实例 <br />{"sites":[<br />{"name":"Runoob", "url":"www.runoob.com"},<br />      {"name":"Google", "url":"www.google.com"},<br />      {"name":"Taobao", "url":"www.taobao.com"}<br />]}<br />JSON对象  用来处理JSON数据  主要有两个静态方法<br />两个静态方法：JSON.stringify()和JSON.parse()。

JSON.stringify()  用来将一个值转换为JSON字符串，该字符串符合JSON格式，并且可以被JSON.parse() 还原<br />如果对象的属性为 undefined ，则会被JSON.stringify() 过滤<br />如果数据的属性为undefined， 则会被JSON.stringify() 转换为null
```javascript
JSON.stringify('abc') // ""abc""
JSON.stringify(1) // "1"
JSON.stringify(false) // "false"
JSON.stringify([]) // "[]"
JSON.stringify({}) // "{}"
JSON.stringify([1, "false", false])
// '[1,"false",false]'
JSON.stringify({ name: "张三" })
// '{"name":"张三"}'
```



JSON.parse方法用于将 JSON 字符串转换成对应的值。
```javascript
JSON.parse('{}') // {}
JSON.parse('true') // true
JSON.parse('"foo"') // "foo"
JSON.parse('[1, 5, "false"]') // [1, 5, "false"]
JSON.parse('null') // null
var o = JSON.parse('{"name": "张三"}');
o.name // 张三
```

<a name="d41d8cd9-2"></a>
## 
<a name="DOM"></a>
## DOM
在HTML 中  一切皆是节点



节点父、子和同胞

节点树中的节点彼此拥有层级关系。<br />父（parent）、子（child）和同胞（sibling）等术语用于描述这些关系。父节点拥有子节点。同级的子节点被称为同胞（兄弟或姐妹）。
* 在节点树中，顶端节点被称为根（root）
* 每个节点都有父节点、除了根（它没有父节点）
* 一个节点可拥有任意数量的子
* 同胞是拥有相同父节点的节点

下面的图片展示了节点树的一部分，以及节点之间的关系：<br />![](https://intranetproxy.alipay.com/skylark/lark/0/2019/gif/116060/1553064804141-891a8c32-6359-4521-9bec-5ebbd6e7cbcb.gif#align=left&display=inline&height=255&originHeight=255&originWidth=381&size=0&status=done&width=381)

<a name="d41d8cd9-3"></a>
## 
总结：<br />创建节点的方法：
* `document.createElement(tag)` —— 用给定标签创建一个节点，
* `document.createTextNode(value)` —— 创建一个文本节点（很少使用），
* `elem.cloneNode(deep)` —— 如果参数 `deep==true` 将元素及后代子元素进行克隆。

插入和移除节点的方法：
* 从 parent
  * `parent.appendChild(node)`
  * `parent.insertBefore(node, nextSibling)`
  * `parent.removeChild(node)`
  * `parent.replaceChild(newElem, node)`
* 这些方法都返回 `node`。<br />
* 添加一些节点和字符串：
  * `node.append(...nodes or strings)` —— 在 `node` 末尾位置增加，
  * `node.prepend(...nodes or strings)` —— 在 `node`开头位置增加 ，
  * `node.before(...nodes or strings)` —— 在 `node` 之前位置增加，
  * `node.after(...nodes or strings)` —— 在 `node` 之后位置增加，
  * `node.replaceWith(...nodes or strings)` —— 替换 `node`。
  * `node.remove()` —— 移除 `node`。
* 把字符串当成“文本”插入。<br />
* 在 HTML 中添加内容`elem.insertAdjacentHTML(where, html)`，在 where 位置进行操作：
  * `"beforebegin"` —— 将 `html` 插入 `elem` 到开头的前面位置，
  * `"afterbegin"` —— 将 `html` 插入 `elem` 到开头的后面位置，
  * `"beforeend"` —— 将 `html` 插入 `elem` 到结尾的前面位置，
  * `"afterend"` —— 将 `html` 插入 `elem` 到结尾的后面位置。
* `elem.insertAdjacentText` 和 `elem.insertAdjacentElement` 跟 `elem.insertAdjacentHTML` 很相似，只不过他们一个用来插入字符串，一个用来插入元素，但是很少使用这两个方法。<br />
* 在页面加载完成之前添加 HTML 到页面中：
  * `document.write(html)`
* 如果是在页面加载完成以后调用会擦除加载完毕的内容。通常在很老的脚本才会使用这个方法了。<br />


document<br />更新节点:    innerHTML   innerText <br />插入节点:   appendChilde<br />删除节点： removeChild

改变CSS

.style <br />事件

遍历  for..of 语法
```javascript
for (let node of document.body.childNodes) {
  alert(node); // shows all nodes from the collection
}
```

子元素 childNodes, firstChild, lastChild<br />搜索 ： getElement  <br />id查找  document.getElementById  才是最佳选择

也有其他的方法来搜索节点：<br />elem.getElementsByTagName(tag) 用给定的标签来查找元素，并返回它们的集合。tag 参数也可以是“任何标签”的 "*"。

```
// 获取所有在文档中的 div
let divs = document.getElementsByTagName('div');
```

还有其他很少使用的方法：
* elem.getElementsByClassName(className) 返回具有给定 CSS 类的元素。元素也可能含有其他的类。
* document.getElementsByName(name) 返回具有给定 name 属性的元素，文档范围。因为历史原因而很少使用。在这里提出，只是考虑到了完整性。

querySelectorAll <br />[总结](https://zh.javascript.info/searching-elements-dom#zong-jie)<br />有 6 种主要的方法，可以在 DOM 中进行搜素：

| Method | Searches by... | Can call on an element? | Live? |
| --- | --- | --- | --- |
| `getElementById` | `id` | - | - |
| `getElementsByName` | `name` | - | ✔ |
| `getElementsByTagName` | tag or `'*'` | ✔ | ✔ |
| `getElementsByClassName` | class | ✔ | ✔ |
| `querySelector` | CSS-selector | ✔ | - |
| `querySelectorAll` | CSS-selector | ✔ | - |

请注意，只有在文档 document.getElementById(...) 的上下文中才能调用 getElementById 和 getElementsByName。但元素中没有 elem.getElementById(...) 回报错。<br />也可以在元素上调用其他方法，例如 elem.querySelectorAll(...) 将会在 elem（在 DOM 子树中）内部进行搜素。<br />除此以外：
* elem.matches(css) 用于检查 elem 与给定的 CSS 选择器是否匹配。
* elem.closest(css) 用于查找与给定 CSS 选择器相匹配的最近的祖先。elem 本身也会被检查。

最后我们在提一种检查父子关系的方法：
* 如果 elemB 在 elemA（elemA 的后代）中或者当 elemA==elemB 时 elemA.contains(elemB) 将返回 true。


<a name="jQuery"></a>
## jQuery

引入文件  head 里引入 

入口函数  简洁版<br />$(function() {


});
<a name="10b2761d"></a>
## 事件
**事件**是某事发生的信号。所有的 DOM 节点都生成这样的信号（但事件不仅限于 DOM）。<br />这里有一张最有用的 DOM 事件列表，请看：<br />**鼠标事件：**
* `click` —— 当鼠标点击一个元素时（触摸屏设备在 tap 时生成）。
* `contextmenu` —— 当鼠标右击一个元素时。
* `mouseover` / `mouseout` —— 当鼠标光标移入或移出一个元素时。
* `mousedown` / `mouseup` —— 当鼠标按下/释放一个元素时。
* `mousemove` —— 当鼠标移出时。

**表单元素事件**：
* `submit` —— 当访问者提交了一个 `<form>` 时。
* `focus` —— 当访问者聚焦一个元素时，例如 `<input>`。

**键盘事件**：
* `keydown` and `keyup` —— 当访问者按下然后松开按钮时。

**Document 事件**：
* `DOMContentLoaded` —— 当加载和处理 HTML 时，DOM 将会被完整地构建。

**CSS 事件**：
* `transitionend` —— 当 CSS 动画完成时。

总结：<br />有 3 种方法可以分发事件处理器：
1. HTML 属性：`onclick="..."`。
1. DOM 属性 `elem.onclick = function`。
1. 方法：添加 `elem.addEventListener(event, handler[, phase])`，移除 `removeEventListener`。

HTML 属性很少使用，因为 HTML 标签中的 JavaScript 看起来奇怪又陌生。而且也不能在里面写太多的代码。<br />DOM 属性可以使用，但我们不能为特定事件分发多个处理器。在许多场景中，这种限制并不严重。<br />最后一种方法是最灵活的，但也是编写内容最多的。有少数事件只能使用这种方式。例如 `transtionend` 和 `DOMContentLoaded`（有待讨论）。当然 `addEventListener` 也支持对象作为事件处理器。在这种场景下，事件发生时就需要调用 `handleEvent` 方法。<br />无论你如何分发处理器 —— 它都会将事件对象作为第一个参数。该对象包含事件发生的细节。



冒泡原理很简单。

**当事件发生在元素上，它首先会运行元素本身的处理器，然后运行父元素上的，再然后是其他祖先上的**。









<a name="d41d8cd9-4"></a>
## 















