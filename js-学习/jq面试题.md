
- [1. jQuery 库中的 $() 是什么？](#1-jquery-库中的--是什么)
- [2. 如何找到所有 HTML select 标签的选中项？](#2-如何找到所有-html-select-标签的选中项)
- [3. $(this) 和 this 关键字在 jQuery 中有何不同？](#3-this-和-this-关键字在-jquery-中有何不同)
- [4. jquery怎么移除标签onclick属性？](#4-jquery怎么移除标签onclick属性)
- [5. jquery中addClass,removeClass,toggleClass的使用。](#5-jquery中addclassremoveclasstoggleclass的使用)
- [6. JQuery有几种选择器?](#6-jquery有几种选择器)
- [7. jQuery中的Delegate()函数有什么作用？](#7-jquery中的delegate函数有什么作用)
- [8. $(document).ready()方法和window.onload有什么区别？](#8-documentready方法和windowonload有什么区别)
- [9. 如何用jQuery禁用浏览器的前进后退按钮？](#9-如何用jquery禁用浏览器的前进后退按钮)
- [10. jquery中`$.get()`提交和`$.post()`提交有区别吗？](#10-jquery中get提交和post提交有区别吗)
- [11. 写出一个简单的`$.ajax()`的请求方式？](#11-写出一个简单的ajax的请求方式)
- [12. jQuery的事件委托方法bind 、live、delegate、on之间有什么区别？](#12-jquery的事件委托方法bind-livedelegateon之间有什么区别)


### 1. jQuery 库中的 $() 是什么？
>$() 函数是 jQuery() 函数的别称。$() 函数用于将任何对象包裹成 jQuery 对象，接着你就被允许调用定义在 jQuery 对象上的多个不同方法。你可以将一个选择器字符串传入 $() 函数，它会返回一个包含所有匹配的 DOM 元素数组的 jQuery 对象。

### 2. 如何找到所有 HTML select 标签的选中项？
`$('[name=selectname] :selected')`
### 3. $(this) 和 this 关键字在 jQuery 中有何不同？
>$(this) 返回一个 jQuery 对象，你可以对它调用多个 jQuery 方法，比如用 text() 获取文本，用val() 获取值等等。

>而 this 代表当前元素，它是 JavaScript 关键词中的一个，表示上下文中的当前 DOM 元素。你不能对它调用 jQuery 方法，直到它被 $() 函数包裹，例如 $(this)。

### 4. jquery怎么移除标签onclick属性？
- 获得a标签的onclick属性: `$("a").attr("onclick")`

- 删除onclick属性：`$("a").removeAttr("onclick")`

- 设置onclick属性：`$("a").attr("onclick","test();")`

### 5. jquery中addClass,removeClass,toggleClass的使用。
- `$(selector).addClass(class)`：为每个匹配的元素添加指定的类名

- `$(selector).removeClass(class)`：从所有匹配的元素中删除全部或者指定的类，删除class中某个值；

- `$(selector).toggleClass(class)`：如果存在（不存在）就删除（添加）一个类

- `$(selector).removeAttr(class)`;删除class这个属性；

### 6. JQuery有几种选择器?
- 基本选择器：`#id`，`class`,`element`,`*`;

- 层次选择器：`parent > child`，`prev + next` ，`prev ~ siblings`

- 基本过滤器选择器：`:first`，`:last `，`:not `，`:even `，`:odd `，`:eq `，`:gt `，`:lt

- 内容过滤器选择器： `:contains `，`:empty `，`:has `，`:parent`

- 可见性过滤器选择器：`:hidden `，`:visible`

- 属性过滤器选择器：`[attribute]` ，[`attribute=value]` ，`[attribute!=value]` ，`[attribute^=value]` ，`[attribute$=value]` ，`[attribute*=value]`

- 子元素过滤器选择器：`:nth-child` ，`:first-child` ，`:last-child` ，`:only-child`

- 表单选择器： `:input` ，`:text` ，`:password` ，`:radio` ，`:checkbox` ，`:submit` 等；

- 表单过滤器选择器：`:enabled` ，`:disabled` ，`:checked` ，`:selected`

### 7. jQuery中的Delegate()函数有什么作用？
>delegate()会在以下两个情况下使用到：
- 如果你有一个父元素，需要给其下的子元素添加事件，这时你可以使用delegate()了，代码如下：
    ```js
    $("ul").delegate("li", "click", function(){
        $(this).hide(); 
    });
    ```
- 当元素在当前页面中不可用时，可以使用delegate()

### 8. $(document).ready()方法和window.onload有什么区别？
- window.onload方法是在网页中所有的元素(包括元素的所有关联文件)完全加载到浏览器后才执行的。

- $(document).ready() 方法可以在DOM载入就绪时就对其进行操纵，并调用执行绑定的函数。

### 9. 如何用jQuery禁用浏览器的前进后退按钮？
实现代码如下：
```js
$(document).ready(function() {
    window.history.forward(1);
    //OR window.history.forward(-1);
　　});
```
### 10. jquery中`$.get()`提交和`$.post()`提交有区别吗？
- 相同点：都是异步请求的方式来获取服务端的数据；
- 不同点：
    1. 请求方式不同：`$.get()` 方法使用GET方法来进行异步请求的。`$.post()` 方法使用POST方法来进行异步请求的。

    2. 参数传递方式不同：get请求会将参数跟在URL后进行传递，而POST请求则是作为HTTP消息的实体内容发送给Web服务器的，这种传递是对用户不可见的。

    3. 数据传输大小不同：get方式传输的数据大小不能超过2KB 而POST要大的多

    4. 安全问题： GET 方式请求的数据会被浏览器缓存起来，因此有安全问题。

### 11. 写出一个简单的`$.ajax()`的请求方式？
```js
$.ajax({
    url:'http://www.baidu.com',
    type:'POST',
    data:data,
    cache:true,
    headers:{},
    beforeSend：function(){},
    success:function(){},
    error:function(){},
    complete:function(){}
}); 
```
### 12. jQuery的事件委托方法bind 、live、delegate、on之间有什么区别？
- bind 【jQuery 1.3之前】
    1. 定义和用法：主要用于给选择到的元素上绑定特定事件类型的监听函数；

    2. 语法：bind(type,[data],function(eventObject))；

    3. 特点：

        - 适用于页面元素静态绑定。只能给调用它的时候已经存在的元素绑定事件，不能给未来新增的元素绑定事件。

        - 当页面加载完的时候，你才可以进行bind()，所以可能产生效率问题。

    4. 实例如下：$( "#members li a" ).bind( "click", function( e ) {} );

- live 【jQuery 1.3之后】
    1. 定义和用法：主要用于给选择到的元素上绑定特定事件类型的监听函数；

    2. 语法：live(type, [data], fn);

    3. 特点：

        - live方法并没有将监听器绑定到自己(this)身上，而是绑定到了this.context上了。

        - live正是利用了事件委托机制来完成事件的监听处理，把节点的处理委托给了document，新添加的元素不必再绑定一次监听器。

        - 使用live（）方法但却只能放在直接选择的元素后面，不能在层级比较深，连缀的DOM遍历方法后面使用，即$(“ul”").live...可以，但$("body").find("ul").live...不行； 

    4. 实例如下：$( document ).on( "click", "#members li a", function( e ) {} );

- delegate 【jQuery 1.4.2中引入】
    1. 定义和用法：将监听事件绑定在就近的父级元素上
    
    2. 语法：delegate(selector,type,[data],fn)

    3. 特点：
        - 选择就近的父级元素，因为事件可以更快的冒泡上去，能够在第一时间进行处理。
        - 更精确的小范围使用事件代理，性能优于.live()。可以用在动态添加的元素上。

    4. 实例如下：
        ```js
        $("#info_table").delegate("td","click",function(){/*显示更多信息*/});
        ```
        ```js
        $("table").find("#info").delegate("td","click",function(){/*显示更多信息*/});
        ```
- on 【1.7版本整合了之前的三种方式的新事件绑定机制】
    1. 定义和用法：将监听事件绑定到指定元素上。

    2. 语法：on(type,[selector],[data],fn)

    3. 实例如下：$("#info_table").on("click","td",function(){/*显示更多信息*/});参数的位置写法与delegate不一样。

    4. 说明：on方法是当前JQuery推荐使用的事件绑定方法，附加只运行一次就删除函数的方法是one()。

- 总结：.bind(), .live(), .delegate(),.on()分别对应的相反事件为：.unbind(),.die(), .undelegate(),.off()