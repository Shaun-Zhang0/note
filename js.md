## 基本类型 引用类型

01. 基本类型 String Number Boolean Undefined Null
02. 引用类型 Array Object Function

## null 和 undefined

* Null 是一个空对象指针 转换为数值为0
* undefined表示的是一个没有初始化的值 转换为数值则就是NAN

## js常见的dom操作api

01. 获取元素节点 

    

``` 
        /***通过类名获取***/
        document.getElementByClassNames("类名")[0] // 返回的一个数组
        /***通过id获取***/
        document.getElementById(); // 直接返回一个元素节点对象
        /***通用查询***/
        document.querySelector("id || 类名"); // 直接返回节点对象

        /***设置属性***/
        nodeObject.setAttitude("属性名","属性值");
        /***设置样式***/
        nodeObject.style.样式 = "值"
    ```

## 解释一下事件冒泡 事件捕获

01. 事件冒泡

    从事件源一层层往上传递 直到document

02. 事件捕获

    从document开始触发 一级一级往下传递 直到事件源

## 阻止事件冒泡 阻止事件默认行为

01. e.stopPropagation();
02. e.preventDefalut();

## 事件委托

* 基于事件冒泡 

``` 
    parentNode.onclick = function(e){
        let event = e || window.event;
        /***点击元素***/
        let eventTarget = e.target || e.srcElement;
    }
```

## 闭包 

* 由于 js 特有的链式作用域 , 只能由函数内部访问函数外部 , 函数外部不能访问到函数内部
* 为了解决函数外部获取不到函数内部的变量 , 通过在函数内部中 , 在定义一个函数 将其 return 局部变量 出去

``` 
    function f1(){
        let n = 1123;
        return f2 = function(){
            return n;
        }
    }

```

* 缺点: 闭包会将函数中变量保存在内存中 , 导致内存消耗很大 , 滥用闭包会导致一些网页的性能问题 , IE 中可能会导致内存泄漏 
* 解决方式 : 退出函数前 , 将所有的局部变量全部删除 

## call apply bind

相同点: 

01. 三者都是改变函数的 this 指向 
02. 第一个参数都是 this 绑定的对象
03. 第二个参数都是传递的参数

不同点:

01. call 和 apply 都是立即执行函数 , 但是 传递参数的方式不同 , call是直接传参 , 而apply则是放在数组中传参
02. bind则是返回一个方法 不会执行

## this

* 函数执行时 , this总是指向调用该函数的对象

## 创建对象

01. 通过 { } 创建对象 , 字面量的方式
02. 使用 Object() 构造函数 创建对象
03. 通过 同一个构造函数创建对象 

## new 一个新的对象 的过程

01. 创建一个新的对象
02. 新的对象的_proto_属性指向构造函数的原型对象 , 这样新的对象就拥有了构造函数中的方法
03. 将构造函数的作用域赋给新的对象
04. 执行构造函数内部的代码 , 将属性添加给 this 新对象中
05. 返回新的对象person

## 手写 ajax

``` 
    var xhr = new XMLHttpRequest();
    xhr.open("GET",url,false);
    xhr.onreadstatechange = function(){
        if(xhr.readystatechange == 4){
            <!-- 内容解析完成 , 可以在客户端调用 -->
            if(xhr.status == 200){
                <!-- 客户端的请求成功 -->
            }
        }
    }
    xhr.send();

```

## 内置对象 本地对象 宿主对象

01. 内置对象 

    

   可以直接使用的对象 不需要创建 例如Math 

02. 本地对象 

   需要通过new关键字来创建的对象 例如date()

03. 宿主对象

   并不是JavaScript自身带有的对象 但是 javascript 可以使用的对象 例如Bom Dom

## attribute和property的区别

01. attribute 是由HTML定义 所有出现在 HTML 标签内的描述节点 都是attribute特性 , 类型为String
02. property 属于Dom对象 可以通过js操作普通的对象获取或者设置Dom对象的属性 类型为任意类型

## document lode事件 和 DOMContentLoaded 两个事件

01. DOMContentLoaded: Dom树解析完成 即触发此事件 无需等待资源的加载
02. load: 资源全部加载完成
03. 先执行DOMContentLoaded 再执行load

``` 
dom文档加载步骤

01. 解析HTML文档
02. 加载外部脚本和样式表文件
03. 解析并执行脚本代码
04. DOM树构建完成 // DOMContentloaded事件执行
05. 加载所依赖的外部资源
06. 页面加载完毕 // load事件执行

/***DOMContentloaded 事件***/
document.addEventListener("DOMContentLoaded",function(){
    // code
})

/***load***/
window.addEventListener("load",function(){
    //code
})

/***jquery***/
// DOMContentLoaded
$(document).ready(function(){
    // code
});
// load
$(document).load(function(){
    // code
});
```

## typeof

* 判断变量的类型 返回值的类型为String 

  

01. null - Object
02. undefined - undefined
03. NaN - number
04. array - Object
05. function(){} - function
06. 123 - number
07. "123" - String
08. true - Boolean

## "use strict" 好处和坏处

* 好处

   

01. 消除JavaScript语法的不合理 不严谨的地方 减少怪异行为
02. 消除代码运行的一些不安全之处 保证代码运行的安全
03. 提高编译器的效率
04. 为未来的新的版本的javaScript做好准备

* 坏处

01. ie6 7 8 9 均不支持严格模式

## js如何实现重载和多态

* js没有严格意义上的方法重载 , 可以通过 arguments 和 实参 的类型进行模拟
* 参数的个数 - argument
* 参数的类型 typeof

``` 
    argument是类数组 , 具有length的属性 但是数组特有的方法是 , 它是不能调用的
```

## 判断是否为数组

01. Array.isArray() // 根据
02. instanceof Array // 根据原型链判断
03. .constructor == Array // 根据constructor 判断

## 数组的方法

01. push
02. pop
03. unshift
04. shift
05. sort
07. concat
08. reverse
09. slice
10. splice

## 字符串的方法

``` 

01.  String.prototype.anchor() 创建一个html <a></a> 锚点元素
02.  String.prototype.bold() 创建一个<b>标签
03.  String.prototype.charAt() 返回索引处的字符
04.  String.prototype.concat() 拼接字符串
05.  String.prototype.endsWith() 判断是否以指定字符串为结尾
06.  String.prototype.startsWith() 判断是否以指定字符串为开头
07.  String.prototype.includes() 判断是否包含指定字符串
08.  String.prototype.indexOf() 返回给定字符串在原字符串中 返回首次出现的index值,找不到则返回 -1
09.  String.prototype.lastIndexOf() 返回给定字符串在原字符串中最后一次出现的索引 , 找不到则返回 -1
10. String.prototype.link() 用于创建一个超链接a标签
11. String.prototype.padEnd() 接受两个参数 第一个参数是期望字符串的长度 第二个是不满足长度时 尾部拼接上去 直至满足长度
12. String.prototype.padStart() 接受两个参数 第一个参数是期望字符串的长度 第二个是不满足长度时 头部拼接上去 直至满足长度
13. String.prototype.repeat() 用于把字符串重复n次 接受一个参数 
14. String.prototyoe.slice() 用于截取字符串的一部分 并返回新的字符串
15. String.prototype.split() 用于分割字符串成数组 
16. String.prototype.toLocaleUpperCase() 将字符串转换为大写
17. String.prototype.toLocaleLowerCase() 将字符串转换为小写
18. String.prototype.toString() 返回指定对象的字符串形式
19. String.prototype.trim() 清除字符串两端的空白
20. String.prototype.trimLeft() 清除字符串左端的空白
21. String.prototype.trimRight() 清除字符串右端的空白
22. String.prototype.replace() 替换字符串中的内容 并返回一个新的字符串

```

## dom0 和 dom2 事件处理

01. dom0级 事件处理程序

``` 
        // 被认为是元素的方法 在元素的作用域中运行

        <div id='btn'></div>
        <script>
            var node = document.getElementByid('btn');
            node.onclick = function(){
                console.log(this); // 会在事件冒泡流阶段被处理
            }
        </script>

        
```

02. dom2级 事件处理

``` 
   // dom2 级事件处理提供了两个方法 addEventListerner() 和 removeEventListerner()
   // 可以通过参数选择在冒泡流或者捕获流中执行
        
        <div id='btn'></div>
        <script>
            var node = document.getElementById('btn');
            <!-- true - 事件捕获流中触发 -->
            node.addEventListerner("click",function(){
                console.log("事件捕获中触发")
            },true);
            <!-- false - 事件冒泡流中触发 -->
            node.addEventListerner("click",function(){
                console.log("事件冒泡中触发")
            },false)
        </script>
```

## IE 事件处理

``` 
    // IE 提供了两个方法 attachEvent 和 deleteEvent , 作用分别是添加事件 和 删除事件.

    btn1Obj.attachEvent("onclick",method2);
    btn1Obj.disattachEvent("onclick",method2);
```

* ie8 前 

``` 
    先绑定的后执行
```

* ie9 后

``` 
    先绑定的先执行
```

 

## location.href 和 location.replace

``` 
    location.href写入浏览器的历史 window.history对象中 location.replace 则不会。

    用法:
        window.location.href = '';
        window.location.replace('');
```

## touch事件 和 click事件

touch事件:

    01. touchstart 
    02. touchmove
    03. touchend

``` 
    移动端执行顺序
    touchstart -> touchmove -> touchend -> click
```

click事件在移动端会延迟300ms , 用于判断这个是一个单击事件
使用touchstart事件的意义在于帮助用户节省300ms的时间

* PC端页面需要兼容移动端页面的时候, touch和click事件就产生了冲突, PC端页面没有touch事件, 移动端点击时会先后触发touch和click事件 

``` 
    解决方案:
        判断当前document是否存在'touchstart'事件
    let node = document.getElementByClassName('testNode')[0];
    const clickEvent = (function(){
        if('touchstart' in document.documentElement){
            return 'touchstart';
        }else{
            return 'click';
        }
    })()
    node.addEventListerner(clickEvent,function(){
        console.log('元素被点击了')
    })

## js 内存泄漏

01. 全局变量不使用var声明

```

    num = 1;
    // 相当于
    window.num = 1;

``` 

* 解决方案: use strict 启用严格模式来规避这一个问题

02. 定时器 没有及时清除 

```

  let timer = setInterval(function(){ alert("Hello"); }, 3000); 
  clearInterval(timer); 
  

``` 

* 因为定时器回调函数是一个闭包 
* 解决方法: 清除定时器

03. 闭包

```

outerFun(outerArgument){

    //被包含的内部函数可以访问外部函数的变量
    return function(){  
        return outerArgument+1
    } 

}
// 调用函数
var result = creatFun(8)
// 解除对匿名函数的引用
creatFun = null

``` 

* 解决方案: 将活动对象设置为null

04. dom元素已被清除 但是仍存在对该dom元素的应用
* 将调用对象设置为null

## event.target 和 currentTarget 的区别

```

event.target可以获取触发的事件的元素
event.currentTarget可以获取绑定事件的元素

```

* target -> 事件冒泡的起点
* currentTarget -> 事件冒泡的终点

