- [1. JavaScript中如何检测一个变量是一个String类型？请写出函数实现](#1-javascript中如何检测一个变量是一个string类型请写出函数实现)
- [2. 请用js去除字符串空格？](#2-请用js去除字符串空格)
- [3. 获取URL字符串中的参数](#3-获取url字符串中的参数)
- [4. 怎样添加、移除、移动、复制、创建和查找节点](#4-怎样添加移除移动复制创建和查找节点)
- [5. 谈谈垃圾回收机制方式及内存管理](#5-谈谈垃圾回收机制方式及内存管理)
- [6. 写出3个使用this的典型应用](#6-写出3个使用this的典型应用)
- [7. 比较typeof与instanceof？](#7-比较typeof与instanceof)
- [8.如何理解闭包？](#8如何理解闭包)
- [9. 什么是跨域？跨域请求资源的方法有哪些？](#9-什么是跨域跨域请求资源的方法有哪些)
- [10. javascript面向对象中继承实现？](#10-javascript面向对象中继承实现)
- [11. 判断一个字符串中出现次数最多的字符，统计这个次数](#11-判断一个字符串中出现次数最多的字符统计这个次数)
- [12. 编写一个方法 去掉一个数组的重复元素](#12-编写一个方法-去掉一个数组的重复元素)

### 1. JavaScript中如何检测一个变量是一个String类型？请写出函数实现
```js
1. typeof(obj) === "string"
2. typeof obj === "string"
3. obj.constructor === String
```
### 2. 请用js去除字符串空格？

- 使用replace正则匹配的方法
    - 去除所有空格：str = str.replace(/\s*/g,"");      
    - 去除两头空格：str = str.replace(/^\s*|\s*$/g,"");
    - 去除 左 空 格：str = str.replace( /^\s*/g, “”);
    - 去除 右 空 格：str = str.replace(/(\s*$)/g, "");
- 实例如下：
    ```js
    var str = " 23 23 ";
    var str2 = str.replace(/\s*/g,"");
    console.log(str2); // 2323
    ```

### 3. 获取URL字符串中的参数
测试地址为：[http://www.runoob.com/jquery/misc-trim.html?channelid=12333&name=xiaoming&age=23](http://www.runoob.com/jquery/misc-trim.html?channelid=12333&name=xiaoming&age=23)
```js
function showWindowHref(){
    var sHref = window.location.href;
    var args = sHref.split('?');
    if(args[0] == sHref){
        return "";
    }
    var arr = args[1].split('&');
    var obj = {};
    for(var i = 0;i< arr.length;i++){
        var arg = arr[i].split('=');
        obj[arg[0]] = arg[1];
    }
    return obj;
}
var href = showWindowHref(); // obj
console.log(href['name']); // xiaoming
```
### 4. 怎样添加、移除、移动、复制、创建和查找节点
- 创建新节点
`createDocumentFragment()` //创建一个DOM片段
`createElement()` 创建具体的元素 
`createTextNode()` //创建一个文本节点
- 添加
`appendChild()` //添加
- 移除
`removeChild()` //移除
- 替换
`replaceChild()` //替换
- 插入
`insertBefore()` //插入
- 查找
`getElementsByTagName()` //通过标签名称
`getElementsByName()` //通过元素的Name属性的值
`getElementById()` //通过元素Id，唯一性
### 5. 谈谈垃圾回收机制方式及内存管理
- 回收机制方式
    1. 定义和用法：垃圾回收机制(GC:Garbage Collection),执行环境负责管理代码执行过程中使用的内存。

    2. 原理：垃圾收集器会定期（周期性）找出那些不在继续使用的变量，然后释放其内存。但是这个过程不是实时的，因为其开销比较大，所以垃圾回收器会按照固定的时间间隔周期性的执行。

    3. 实例如下：
        ```
        function fn1() {
            var obj = {name: 'hanzichi', age: 10};
        }
        function fn2() {
            var obj = {name:'hanzichi', age: 10};
        return obj;
        }
        var a = fn1();
        var b = fn2();
        ```
        fn1中定义的obj为局部变量，而当调用结束后，出了fn1的环境，那么该块内存会被js引擎中的垃圾回收器自动释放；在fn2被调用的过程中，返回的对象被全局变量b所指向，所以该块内存并不会被释放。

   4. 垃圾回收策略：标记清除(较为常用)和引用计数。

- 标记清除：

  定义和用法：当变量进入环境时，将变量标记"进入环境"，当变量离开环境时，标记为："离开环境"。某一个时刻，垃圾回收器会过滤掉环境中的变量，以及被环境变量引用的变量，剩下的就是被视为准备回收的变量。
  
  到目前为止，IE、Firefox、Opera、Chrome、Safari的js实现使用的都是标记清除的垃圾回收策略或类似的策略，只不过垃圾收集的时间间隔互不相同。

- 引用计数：
  定义和用法：引用计数是跟踪记录每个值被引用的次数。
  
  基本原理：就是变量的引用次数，被引用一次则加1，当这个引用计数为0时，被视为准备回收的对象。

- 内存管理
  1. 什么时候触发垃圾回收？

        垃圾回收器周期性运行，如果分配的内存非常多，那么回收工作也会很艰巨，确定垃圾回收时间间隔就变成了一个值得思考的问题。

        IE6的垃圾回收是根据内存分配量运行的，当环境中的变量，对象，字符串达到一定数量时触发垃圾回收。垃圾回收器一直处于工作状态，严重影响浏览器性能。

        IE7中，垃圾回收器会根据内存分配量与程序占用内存的比例进行动态调整，开始回收工作。

  2. 合理的GC方案：(1)、遍历所有可访问的对象; (2)、回收已不可访问的对象。

  3. GC缺陷：(1)、停止响应其他操作；

  4. 优化策略：(1)、分代回收（Generation GC）;(2)、增量GC

  5. 开发过程中遇到的内存泄露情况，如何解决的？
- 内存泄漏  
  1. 定义和用法：内存泄露是指一块被分配的内存既不能使用，又不能回收，直到浏览器进程结束。C#和Java等语言采用了自动垃圾回收方法管理内存，几乎不会发生内存泄露。我们知道，浏览器中也是采用自动垃圾回收方法管理内存，但由于浏览器垃圾回收方法有bug，会产生内存泄露。
  2. 内存泄露的几种情况:
        - 当页面中元素被移除或替换时，若元素绑定的事件仍没被移除，在IE中不会作出恰当处理，此时要先手工移除事件，不然会存在内存泄露。
        
            - 实例如下:
                ```html
                <div id="myDiv">
                    <input type="button" value="Click me" id="myBtn">
                </div>
                ```
                ```js
                var btn = document.getElementById("myBtn");
                btn.onclick = function(){
                document.getElementById("myDiv").innerHTML = "Processing...";
                ```
            - 解决方法如下：
                ```html
                <div id="myDiv">
                    <input type="button" value="Click me" id="myBtn">
                </div>
                ```
                ```js
                var btn = document.getElementById("myBtn");
                btn.onclick = function(){
                btn.onclick = null;
                document.getElementById("myDiv").innerHTML = "Processing...";
                }
                ```
        - 由于是函数内定义函数，并且内部函数--事件回调的引用外暴了，形成了闭包。闭包可以维持函数内局部变量，使其得不到释放。
            - 实例如下：
                ```js
                function bindEvent(){
                var obj=document.createElement("XXX");
                obj.onclick=function(){
                    //Even if it's a empty function
                }
                }
                ```
            - 解决方法如下：
                ```js
                function bindEvent(){
                var obj=document.createElement("XXX");
                    obj.onclick=function(){
                        //Even if it's a empty function
                    }
                    obj=null;
                }
                ```
### 6. 写出3个使用this的典型应用
- 在html元素事件属性中使用，如：

    ```html
    <input type=”button” onclick=”showInfo(this);” value=”点击一下”/>
    ```
- 构造函数

    ```js
    function Animal(name, color) {
        this.name = name;
        this.color = color;
    }
    ```
- input点击，获取值
    ```html
    <input type="button" id="text" value="点击一下" />
    ```
    ```js
    var btn = document.getElementById("text");
    btn.onclick = function() {
    alert(this.value);    //此处的this是按钮元素
    }
    ```
- apply()/call()求数组最值
    ```js
    var numbers = [5, 458 , 120 , -215 ]; 
    var maxInNumbers = Math.max.apply(this, numbers);  
    console.log(maxInNumbers);  // 458
    var maxInNumbers = Math.max.call(this,5, 458 , 120 , -215); 
    console.log(maxInNumbers);  // 458
    ```
### 7. 比较typeof与instanceof？
- 相同点：JavaScript 中 typeof 和 instanceof 常用来判断一个变量是否为空，或者是什么类型的。

- typeof的定义和用法：返回值是一个字符串，用来说明变量的数据类型。

- 细节：

    1. typeof 一般只能返回如下几个结果：number,boolean,string,function,object,undefined。

    2. typeof 来获取一个变量是否存在，如 if(typeof a!="undefined"){alert("ok")}，而不要去使用 if(a) 因为如果 a 不存在（未声明）则会出错。

    3. 对于 Array,Null 等特殊对象使用 typeof 一律返回 object，这正是 typeof 的局限性。

- Instanceof定义和用法：instanceof 用于判断一个变量是否属于某个对象的实例。
- 实例演示：
    ```js
    a instanceof b?alert("true"):alert("false"); //a是b的实例？真:假
    var a = new Array(); 
    alert(a instanceof Array);  // true
    alert(a instanceof Object)  // true
    ```
如上，会返回 true，同时 alert(a instanceof Object) 也会返回 true;这是因为 Array 是 object 的子类。
    ```js
    function test(){};
    var a = new test();
    alert(a instanceof test)   // true
    ```
- 细节：

    如下，得到的结果为‘N’,这里的 instanceof 测试的 object 是指 js 语法中的 object，不是指 dom 模型对象。
    ```js
    if (window instanceof Object){ alert('Y')} else {  alert('N');}  // 'N'
    ```
### 8.如何理解闭包？
- 定义和用法：当一个函数的返回值是另外一个函数，而返回的那个函数如果调用了其父函数内部的其它变量，如果返回的这个函数在外部被执行，就产生了闭包。

- 表现形式：使函数外部能够调用函数内部定义的变量。

- 实例如下：

    根据作用域链的规则，底层作用域没有声明的变量，会向上一级找，找到就返回，没找到就一直找，直到window的变量，没有就返回undefined。这里明显count 是函数内部的flag2 的那个count 。
    ```js
    var count=10;   //全局作用域 标记为flag1
    function add(){
        var count=0;    //函数全局作用域 标记为flag2
        return function(){
            count+=1;   //函数的内部作用域
            alert(count);
        }
    }
    var s = add()
    s();//输出1
    s();//输出2
    ```
- 变量的作用域

    要理解闭包，首先必须理解Javascript特殊的变量作用域。

    变量的作用域分类：全局变量和局部变量。

- 特点：

    1. 函数内部可以读取函数外部的全局变量；在函数外部无法读取函数内的局部变量。

    2. 函数内部声明变量的时候，一定要使用var命令。如果不用的话，你实际上声明了一个全局变量！

- 使用闭包的注意点

    1. 滥用闭包，会造成内存泄漏：由于闭包会使得函数中的变量都被保存在内存中，内存消耗很大，所以不能滥用闭包，否则会造成网页的性能问题，在IE中可能导致内存泄露。解决方法是，在退出函数之前，将不使用的局部变量全部删除。

    2. 会改变父函数内部变量的值。所以，如果你把父函数当作对象（object）使用，把闭包当作它的公用方法（Public Method），把内部变量当作它的私有属性（private value），这时一定要小心，不要随便改变父函数内部变量的值。
### 9. 什么是跨域？跨域请求资源的方法有哪些？

- 什么是跨域？

    由于浏览器同源策略，凡是发送请求url的协议、域名、端口三者之间任意一与当前页面地址不同即为跨域。存在跨域的情况：

    1. 网络协议不同，如http协议访问https协议。

    2. 端口不同，如80端口访问8080端口。

    3. 域名不同，如qianduanblog.com访问baidu.com。

    4. 子域名不同，如abc.qianduanblog.com访问def.qianduanblog.com。

    5. 域名和域名对应ip,如www.a.com访问20.205.28.90.

- 跨域请求资源的方法：
    1. porxy代理

        - 定义和用法：proxy代理用于将请求发送给后台服务器，通过服务器来发送请求，然后将请求的结果传递给前端。

        - 实现方法：通过nginx代理；

        - 注意点：1、如果你代理的是https协议的请求，那么你的proxy首先需要信任该证书（尤其是自定义证书）或者忽略证书检查，否则你的请求无法成功。

    2. CORS 【Cross-Origin Resource Sharing】

        - 定义和用法：是现代浏览器支持跨域资源请求的一种最常用的方式。

        - 使用方法：一般需要后端人员在处理请求数据的时候，添加允许跨域的相关操作。如下：
            ```js
            res.writeHead(200, {
                "Content-Type": "text/html; charset=UTF-8",
                "Access-Control-Allow-Origin":'http://localhost',
                'Access-Control-Allow-Methods': 'GET, POST, OPTIONS',
                'Access-Control-Allow-Headers': 'X-Requested-With, Content-Type'
            });
            ```
    3. jsonp

        - 定义和用法：通过动态插入一个script标签。浏览器对script的资源引用没有同源限制，同时资源加载到页面后会立即执行（没有阻塞的情况下）。

        - 特点：通过情况下，通过动态创建script来读取他域的动态资源，获取的数据一般为json格式。

        - 实例如下：
            ```js
            function testjsonp(data) {
            console.log(data.name); // 获取返回的结果
            }
            ```
            ```js
            var _script = document.createElement('script');
            _script.type = "text/javascript";
            _script.src = "http://localhost:8888/jsonp?callback=testjsonp";
            document.head.appendChild(_script);
            ```
        - 缺点：
            1. 这种方式无法发送post请求（这里）
            2. 另外要确定jsonp的请求是否失败并不容易，大多数框架的实现都是结合超时时间来判定。
### 10. javascript面向对象中继承实现？ 
- 面向对象的基本特征有：封闭、继承、多态。

- 在JavaScript中实现继承的方法：

    1. 原型链（prototype chaining）

    2. call()/apply()

    3. 混合方式(prototype和call()/apply()结合)

    4. 对象冒充

-   继承的方法如下：

    1. prototype原型链方式：
        ```js
        function teacher(name){
            this.name = name;
        }
        teacher.prototype.sayName = function(){
            console.log("name is "+this.name);
        }
        var teacher1 = new teacher("xiaoming");
        teacher1.sayName();
        
        function student(name){
            this.name = name;
        }
        student.prototype = new teacher()
        var student1 = new student("xiaolan");
        student1.sayName();
        //  name is xiaoming
        //  name is xiaolan
        ```
    2. call()/apply()方法
        ```js
        function teacher(name,age){
        this.name = name;
        this.age = age;
        this.sayhi = function(){
        alert('name:'+name+", age:"+age);
        }
        }
        function student(){
        var args = arguments;
        teacher.call(this,args[0],args[1]);
        // teacher.apply(this,arguments);
        }
        var teacher1 = new teacher('xiaoming',23);
        teacher1.sayhi();

        var student1 = new student('xiaolan',12);
        student1.sayhi();

        // alert: name:xiaoming, age:23
        // alert: name:xiaolan, age:12
        ```
    3. 混合方法【prototype,call/apply】
        ```js
        function teacher(name,age){
        this.name = name;
        this.age = age;
        }
        teacher.prototype.sayName = function(){
        console.log('name:'+this.name);
        }
        teacher.prototype.sayAge = function(){
        console.log('age:'+this.age);
        }

        function student(){
        var args = arguments;
        teacher.call(this,args[0],args[1]);
        }
        student.prototype = new teacher();

        var student1 = new student('xiaolin',23);
        student1.sayName();
        student1.sayAge();
        // name:xiaolin
        // age:23
        ```
    4. 对象冒充
        ```js
        function Person(name,age){
        this.name = name;
        this.age = age;
        this.show = function(){
        console.log(this.name+", "+this.age);
        }
        }

        function Student(name,age){
        this.student = Person; //将Person类的构造函数赋值给this.student
        this.student(name,age); //js中实际上是通过对象冒充来实现继承的
        delete this.student; //移除对Person的引用
        }

        var s = new Student("小明",17);
        s.show();

        var p = new Person("小花",18);
        p.show();
        // 小明, 17
        // 小花, 18
        ```
### 11. 判断一个字符串中出现次数最多的字符，统计这个次数
```js
var str = 'asdfssaaasasasasaa';
var json = {};
for (var i = 0; i < str.length; i++) {
    if(!json[str.charAt(i)]){
       json[str.charAt(i)] = 1;
    }else{
       json[str.charAt(i)]++;
    }
};
var iMax = 0;
var iIndex = '';
for(var i in json){
    if(json[i]>iMax){
         iMax = json[i];
         iIndex = i;
    }
}        
console.log('出现次数最多的是:'+iIndex+'出现'+iMax+'次');
```
### 12. 编写一个方法 去掉一个数组的重复元素
- 方法一：
    ```js
    var arr = [0,2,3,4,4,0,2];
    var obj = {};
    var tmp = [];
    for(var i = 0 ;i< arr.length;i++){
    if( !obj[arr[i]] ){
        obj[arr[i]] = 1;
        tmp.push(arr[i]);
    }
    }
    console.log(tmp);
    //结果如下： [0, 2, 3, 4]
    ```
- 方法二：
    ```js
    var arr = [2,3,4,4,5,2,3,6],
    arr2 = [];
    for(var i = 0;i< arr.length;i++){
        if(arr2.indexOf(arr[i]) < 0){
            arr2.push(arr[i]);
        }
    }
    console.log(arr2);
    结果为：[2, 3, 4, 5, 6]
    ```
- 方法三：
    ```js
    var arr = [2,3,4,4,5,2,3,6];
    var arr2 = arr.filter(function(element,index,self){
    return self.indexOf(element) === index;
    });
    console.log(arr2);
    //结果为：[2, 3, 4, 5, 6]
    ```