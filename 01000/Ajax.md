# Ajax-day1

##客户端和服务器的基本概念

- 上网的目的：
  - 获取和使用资源，请求数据
- 客户端和服务器(服务端)
  - 客户端：
    - 客户指的是使用服务的人，客户端指的是**使用服务**的计算机
    - 如果一台计算机希望成为客户端，必须安装浏览器
  - 服务端：
    - 指的是**提供服务**的计算机
    - 如果一台计算机希望成为服务端，必须**安装特定的服务端软件**即可

## URL网址的基本概念

- URL概念：统一资源定位符 （Uniform   Resource  Locator）
  - 俗称网址，用来标识某个资源在网络中的唯一位置。
- 组成部分：
  - 示例网址：<https://detail.tmall.com/item.htmid=555428842095&spm=a310p.7395781.1998038982.3>
  - 通信协议： https://
  - 域名（服务器地址）： detail.tmall.com
  - 资源（文件）的具体位置：  /item.htm?id=555428842095&spm=a310p.7395781.1998038982.3

## 请求和响应的流程

- 任意的一次网络访问(访问网站根目录、img加载、audio加载、link标签....)都是下面的3个步骤
- 步骤
  - 1 **请求：客户端请求服务器**
  - 2 处理：服务器的内部处理（找找资源等..）
  - **3 响应：服务器响应客户端**

###浏览器的network面板的使用

> network用来检测浏览器发出的每次**请求**以及**响应**内容

- 可以使用：<http://ntlias3.boxuegu.com/> 网站进行尝试
- 打开方式：浏览器 -> F12 -> Network -> 进行操作
  - 左侧为所有请求的请求列表
  - 顶部具有请求的筛选功能
  - 选择某一条请求后，可以查看请求的具体内容
    - request 请求
    - response 响应

## 网站中的资源

- 常见资源为：图片、文字、音视频、css文件...
- 核心资源：数据（根据数据生成页面结构可以让页面制作变简便，维护成本降低）
- 与html、css、js的关系
  - html是网页的结构、骨架
  - css是网页的样式、颜值
  - js是网页的行为、控制交互
  - **数据是网页灵魂**

## 资源的请求方式get post

- 请求类型：get()     post()
  - **语义的区别**
    - get 用来进行**获取资源**的请求操作
      - 获取图片、音视频、js文件、css文件、地址栏输入地址回车，location.href，a标签跳转。。。
    - post 用来进行**发送资源**的请求操作
      - 表单提交form标签（get、post均可，可以自己选择）
      - ajax也可以发送get和post请求
  - **可发送数据大小有区别**
    - get请求受限制于浏览器对url的限制，2M左右
    - post请求理论上无大小限制，实际上受限制于服务端实际的业务需求和处理能力
  - **可发送的数据格式有区别**
    - get请求只能发送文本格式数据
    - post请求不限制发送的数据格式，服务器会根据业务需求进行处理

### 之前使用过的请求发送方式

- 地址栏
- a标签
- location.href
- img.src  link.href 我们无法进行干预
- form+submit

> 上面是我们之前学习过的发送请求的方式，统一特点：**都会出现跳转(有的是我们无法干预的)**
>
> 实际页面功能制作时，很多的功能虽然请求了新的数据，但是并没有出现跳转，只是局部刷新
>
> 小结论：传统的请求方式无法满足现代网页的所有功能，就需要使用新的请求方式----AJAX。

## AJAX简介

> Ajax（**Async**hronous Javascript And XML（异步 JavaScript 和 XML））

- 作用：用来发送请求的一种方式
- 实现方式简介：浏览器提供了一个XMLHttpRequest的构造函数，创建的对象用来进行ajax操作
  - 为了让大家更好的理解ajax的使用，先学习jQuery中的ajax操作，再学习ajax的原生实现和封装。
- 特点：无需刷新页面，也可以进行请求响应处理（局部刷新）

### 同步和异步的概念

> 同步任务：

- **执行顺序：代码按顺序从上往下一个一个执行。**
- 同步任务有哪些：除了异步任务都是同步任务。

> 异步任务：

- 为什么要有异步任务: 因为某些任务较为耗时，或执行时间不确定，为了避免卡住（阻塞）后续代码，设置为异步任务。
- **常见异步任务有哪些：**
  - 定时器
    - 示例：无论定时器的时间为多少，都会比同步任务执行晚。
  - Ajax
- **执行顺序：异步任务的执行一定晚于同步任务**

###6.2单线程和js语言特性回顾

> js的语言特性
>
> - js是弱类型语言
> - js是动态语言
> - js是脚本语言
> - js是基于对象的语言(面向对象语言)
> - js是基于原型的语言
> - js是事件驱动的语言
> - **js是单线程的语言**
>   - 单线程（只有一个人干活）
>     - 因为js中具有DOM操作，例如修改元素颜色，单个线程操作不会与其他线程产生干扰冲突
>     - es5后js也出现了多线程的概念，但是有限制，多个线程只能进行辅助操作，主线程进行控制
>   - 多线程（有好多人干活）

## $.get()的使用

> 没有请求参数，不接收响应数据

```js
$.get(地址); // 通过浏览器调试工具的network查看请求的细节和响应的数据

$.get('http://www.liulongbin.top:3006/api/getbooks');
```

> 没有请求参数，接收响应数据

```js
$.get(地址, function(res) {
  // 响应接收完毕后，执行回调函数
  // res代表响应的数据，如果res为JSON格式，jQuery会自动转换
});

$.get('http://www.liulongbin.top:3006/api/getbooks', function (res) {
     // 响应完成后，触发这个回调函数
     // console.log('执行了回调函数');

     // 回调函数的参数表示响应的数据，一般称为response或res
     // 发现，响应的JSON格式数据被jQuery自动转换为js对象
     console.log(res);
   });
```

> 有请求参数，接收响应数据
>
> 请求参数：请求中发送给服务端的数据，是一个对象

```js
$.get(地址, 请求参数组成的对象, 回调函数);

$.get('http://www.liulongbin.top:3006/api/getbooks', { id: 2 }, function (res) {
      console.log(res);
    });
```

## $.post()的使用

> 没有请求参数，不接收响应数据

```js
$.post(地址); // 通过浏览器调试工具的network查看请求的细节和响应的数据

$.post('http://192.168.141.45:3005/common/post');
```

> 没有请求参数，接收响应数据

```js
$.post(地址, function(res) {
  // 响应接收完毕后，执行回调函数
  // res代表响应的数据，如果res为JSON格式，jQuery会自动转换为js对象
});

$.post('http://192.168.141.45:3005/common/post', function (res) {
      console.log('成功接收响应内容');
      console.log(res);
    })
```

> 有请求参数，接收响应数据
>
> 请求参数：请求中发送给服务端的数据，是一个对象

```js
$.post(地址, 请求参数组成的对象, 回调函数);

$.post(
      'http://192.168.141.45:3005/common/post',
      { name: 'jack', age: 18 },
      function (res) {
        console.log('成功接收响应内容');
        console.log(res);
      });
```

## $.ajax()的使用

- type表示请求方式，默认为'GET'，可以设置为'GET'/'POST'
- url表示请求地址
  - 只有url属性是必须设置的
- data表示请求参数，对象结构
- success表示响应成功时的处理函数
  - res参数，表示响应内容

```js
// 1 使用$.ajax()发送GET请求
    $.ajax({
      // type: 'GET', // 默认为GET，一般发送GET请求时，都不设置type
      url: 'http://192.168.141.45:3005/common/get',
      data: {
        name: 'jack',
        age: 18,
        gender: '男'
      },
      success: function (res) {
        console.log(res);
      }
    }); 
```

```js
// 2 使用$.ajax()发送POST请求
    $.ajax({
      type: 'POST',
      url: 'http://192.168.141.45:3005/common/post',
      data: {
        width: 200,
        height: 600,
        bgc: 'red'
      },
      success: function (res) {
        console.log(res);
      }
   });
```

> (了解) $.get() / $.post()与 $.ajax()的关系
>
> $.ajax是jQuery中设置的一个用来进行ajax请求发送的方法 $.get() $.post()只是调用了$.ajax()实现的功能

## 接口的概念

- 接口：电源接口    usb接口     网线接口    type-c接口
  - 概念：接口指的是**能够提供某种能力**的事物。
- 应用程序编程接口（API）
  - 概念：提供应用程序编程能力的事物
  - 以前学习过的API
    - WebAPI
      - 浏览器提供的，与web开发相关的一些API，本质上就是一堆属性方法
    - 内置对象API
      - js解析器提供的，用于js基础语法操作的一些API，本质上就是一堆属性方法
    - js的组成部分和浏览器的主要构成
      - 浏览器的两个主要构成部分
        - 内核(渲染引擎): html和css渲染，WebAPI
        - js解析器：执行ECMAScript
      - 规范相关内容：
        - w3c规范：html  css  webAPI
        - ECMA规范：语法(含内置对象)
- 数据接口：
  - 概念：数据接口是**能够提供数据的**一种事物。表现形式就是一个URL
    - **简单来说，能够提供数据的一个URL地址，就称为是数据接口**
  - 说明：当我们进行前端和后端(服务器)交互时，所说的'**接口**'，指的就是数据接口。
  - 使用方式：**严格遵守接口的文档进行操作即可。**

## 时间戳格式化方法

```js
// 用来将时间戳进行日期格式化的函数：

    function dateFormat(timestamp) {
        var time = new Date(parseInt(timestamp));
        var y = time.getFullYear();
        var m = time.getMonth() + 1;
        m = m > 9 ? m : '0' + m;
        var d = time.getDate();
        d = d > 9 ? d : '0' + d;
        var h = time.getHours();
        h = h > 9 ? h : '0' + h;
        var mm = time.getMinutes();
        mm = mm > 9 ? mm : '0' + mm;
        var s = time.getSeconds();
        s = s > 9 ? s : '0' + s;
        return y + '-' + m + '-' + d + ' ' + h + ':' + mm + ':' + s;
    }
    
    var time=1575808501208;    -------时间戳
    time=dateFormat(time);
```

# Ajax-day2

##1.表单form

> 表单在网页中主要负责数据采集功能。HTML中的<form>标签，就是用于采集用户输入的信息 ,
>
> 由于<form>标签的submit提交操作会发生跳转，用户体验很差，页面之前的状态和数据会丢失。
>
> **经常使用表单进行数据采集(用输入框等元素获取输入内容)，使用ajax进行请求发送即可(提交)**

###1.1**表单的组成部分**

- form标签
- 表单域：input标签。。textarea。。select....
- 提交按钮： \<input type="submit">  \<button type="submit">提交</button>
  - 如果希望button不进行提交操作，只是普通按钮，可以设置type为button

### 1.2form标签的属性

> <form>标签的属性则是用来规定如何把采集到的数据发送到服务器。

- action   
  - action 属性的值是一个URL地址，定义向何处提交表单，默认值为当前页面的 URL 地址。
  - 注意：当提交表单后，页面会立即跳转到 action 属性指定的 URL 地址。
- target  
  - 规定在何处打开 action URL。
  - _self 默认在本窗口打开   _blank在新窗口打开
- method  
  - 规定以何种方式把表单数据提交到 action URL ，get和post
- enctype  
  - 规定在发送表单数据之前如何对数据进行编码 
  - 在涉及到文件上传的操作时，必须将 enctype 的值设置为 multipart/form-data

###1.3表单操作的特点

- 提交数据时会出现页面跳转的情况
- 提交后，页面之前的状态和数据会丢失。

###1.4常用请求方式

- **使用表单进行数据采集(用输入框等元素获取输入内容)，使用ajax进行请求发送即可(提交)**

##2.表单和ajax结合使用

### 2.1监听表单提交事件 

在 jQuery 中，可以使用如下两种方式，监听到表单的提交事件： 

```js
$('#form1').submit(function(e) {
   alert('监听到了表单的提交事件')
})

$('#form1').on('submit', function(e) {
   alert('监听到了表单的提交事件')
})
```

### 2.2阻止表单的默认提交行为

> 在submit事件中，设置e.preventDefault()方法即可(推荐)， return false也可以

```js
$('#form1').submit(function(e) {
   // 阻止表单的提交和页面的跳转
   e.preventDefault()
})

$('#form1').on('submit', function(e) {
   // 阻止表单的提交和页面的跳转
   e.preventDefault()
})
```

### 2.3 serialize()快速获取表单中的数据 

> jQuery的serialize()方法可以快速获取表单中的所有数据(**只能获取纯文本数据**)

为了简化表单中数据的获取操作，jQuery 提供了 serialize() 函数，其语法格式如下 :

```js
$(selector).serialize()
```

serialize() 函数的好处：可以一次性获取到表单中的所有的数据。

```js
<form id="form1">
    <input type="text" name="username" />
    <input type="password" name="password" />
    <button type="submit">提交</button>
</form>

$('#form1').serialize()
// 调用的结果：
// username=用户名的值&password=密码的值
注意：在使用 serialize() 函数快速获取表单数据时，必须为每个表单元素添加 name 属性！
```

- 注意：这种内容格式可以通过$.get $.post $.ajax进行直接发送
- 注意表单元素如果没有name，数据是无法正确提交的

##3.模板引擎

> 模板引擎，可以根据程序员指定的模板结构和数据，自动生成一个完整的HTML页面。 

- 为什么要使用模板引擎
  - 传统方式的字符串拼接比较麻烦，html与js书写在一起不方便维护
- 模板引擎的作用：
  - 可以将生成结构的字符串拼接操作进行简化。
  - 使代码结构更清晰
  - 使代码更易于阅读与维护
- art-template模板引擎的安装
  - 安装：官网下载 <http://aui.github.io/art-template/zh-cn/docs/installation.html>

###3.1使用步骤

- 引入template-web.js
- 准备数据data(通常为请求得到的数据)
- 准备模板
  - 使用script标签，设置type为text/template，设置id
  - 内部书写需要的结构内容
  - 结合模板语法进行操作
- 调用template方法处理
  - template('id名', 数据)
  - 返回值为将数据和模板结合后得到的字符串

```js
<body>
  <!-- 例如，将需要生成的结构放入到box中 -->
  <div id="box"></div>

  <!-- 1 引入模板引擎的js文件 -->
  <script src="template-web.js"></script>
  
  <!-- 3 定义模板 -->
  <!-- 模板使用script标签，将type设置为非js格式即可，推荐书写为text/template -->
  <script type="text/template" id="template">
        <div>
          <p>{{name}}</p>
        </div>
        <div>
          <p>{{age}}</p>
        </div>
  </script>

  <!-- 2 在js中准备要使用的数据 -->
  <script>
        var data = {
          name: 'jack',
          age: 17,
        };

    // 4 在js中引入模板的结构内容
    // template()是art-template提供的一个全局函数
    // 参数1：模板的id名   参数2：要传入的数据
    // 返回值：将模板和数据结合后得到的结构字符串(相当于以前字符串拼接的结果)
    
    var htmlStr = template('template', data);

    document.getElementById('box').innerHTML = htmlStr;
  </script>
</body>
```

##4.模板引擎的语法

### 4.1 art-template 中标准语法

> art-template 提供了 {{ }} 这种语法格式，在 {{ }} 内可以进行变量输出，或循环数组等操作 。 

```js
{{}} 是模板的基本标记，标记中会进行模板语法的执行，标记外原样输出

{{$data}} 代表template()的参数2

{{$data.属性名}}  用于访问$data的属性
简写形式 {{$data的属性名}}  也表示访问$data的属性 
```

```js
{{$data}}     代表template()的参数2

{{$data.name}}   用于访问$data的属性
{{$data.age}}
{{name}}         简写
{{age}}
```

###4.2标准语法-输出

> 在 {{ }} 语法中，可以进行变量的输出、对象属性的输出、三元表达式输出、逻辑或输出、加减乘除等表达式输出。

```js
{{value}}
{{obj.key}}
{{obj['key']}}
{{a ? b : c}}
{{a || b}}
{{a + b}}
```

### 4.3标准语法-原文输出 

> 如果要输出的 value 值中，包含了 HTML 标签结构，则需要使用原文输出语法，才能保证 HTML 标签被正常渲染。 

```js
{{@ value }}
```

### 4.4标准语法-条件输出

> 如果要实现条件输出，则可以在 {{ }} 中使用 if … else if … /if 的方式，进行按需输出。 

```js
{{if value}} 
   按需输出的内容 
{{/if}}

{{if v1}} 
   按需输出的内容 
{{else if v2}} 
   按需输出的内容 
{{/if}}
```

```js
{{if age===17}}
    <p>此人17岁</p>
{{/if}}

 {{if age>=18}}
    <p>此人成年了</p>
 {{else}}
    <p>此人未成年</p>
 {{/if}}

{{if age===21}}
    <p>此人21岁</p>
{{else if age===20}}
    <p>此人20岁</p>
{{else}}
    <p>此人不知道多少岁</p>
{{/if}}
```

### 4.5标准语法-循环输出 

```
如果要实现循环输出，则可以在 {{ }} 内，通过 each 语法循环数组，
当前循环的索引使用 $index 进行访问，当前的循环项使用 $value 进行访问。
可以统一遍历数组和对象两种形式
```

```js
//在each中$index和$value是模板默认提供的名称， $index代表索引/属性名  $value代表元素值/属性值
{{each arr}}
    {{$index}} {{$value}}
{{/each}}

 {{each obj}}
    <p>这是p标签</p>  {{$index}}   {{$value}}
 {{/each}}
 {{each obj value key}}
    <p>这是p标签</p>  {{key}}   {{value}}      //可以通过自定义名称替换$index与$value
 {{/each}}
```

### 4.6标准语法-过滤器

> 过滤器的本质，就是一个 function 处理函数。

> 作用：是用来对模板中某些数据进行处理的一个方法

> 设置方式：**在调用模板功能前设置**

```js
template.defaults.imports.过滤器名称 = function (模板中书写的数据) {
  // 进行各种的内容处理
  return '处理结果';
};
```

- 过滤器的返回值，会作为模板中最终展示的数据
- 模板中的写法

```js
{{time}}  这是普通的输出方式

{{time|过滤器名称}} 这是通过过滤器处理后的输出方式
```

```js
<body>
  <!-- 例如，将需要生成的结构放入到box中 -->
  <div id="box"></div>

  <!-- 1 引入模板引擎的js文件 -->
  <script src="template-web.js"></script>
  
  <!-- 3 定义模板 -->
  <script type="text/template" id="template">
    {{time|dateFormat}}
  </script>

  <!-- 2 在js中准备要使用的数据 -->
  <script>
    var data = {
      time: 1575877610719
    };
    // 使用模板功能前，需要定义好过滤器的功能
    template.defaults.imports.dateFormat = function (time) {
      // 内部书写日期的格式化功能即可
        var time = new Date(time);
        var y = time.getFullYear();
        var m = time.getMonth() + 1;
        m = m > 9 ? m : '0' + m;
        var d = time.getDate();
        d = d > 9 ? d : '0' + d;
        var h = time.getHours();
        h = h > 9 ? h : '0' + h;
        var mm = time.getMinutes();
        mm = mm > 9 ? mm : '0' + mm;
        var s = time.getSeconds();
        s = s > 9 ? s : '0' + s;
        return y + '-' + m + '-' + d + ' ' + h + ':' + mm + ':' + s;
      // 通过返回值，将处理结果展示在模板中
    };
    
    // 4 在js中引入模板的结构内容
    var htmlStr = template('template', data);
    
    document.getElementById('box').innerHTML = htmlStr;
  </script>
</body>
```

##5.模板引擎的实现方式

### 5.1正则与字符串操作 

> 正则表达式：对字符串进行匹配、替换、提取操作

> 正则.test()    匹配：检测字符串是否满足某些规则

> 字符串.replace()  替换

> 字符串.match()  正则.exec()  提取：将满足规则的内容取出

###5.2 exec()提取

> exec() 正则提取方法

> 参数：要进行提取的字符串

> 返回值是提取到的内容所在的数组

> 规则：每次提取到一个新内容，再次调用再取新内容，取不到时返回null

```js
var str = '呵{{gender}}呵呵{{name}}嘿{{age}}嘿嘿';

var reg = /{{[a-z]+}}/g; // 基本使用     g表示global,全局，全部匹配

console.log(reg.exec(str)); // ["{{gender}}"]
console.log(reg.exec(str)); // ["{{name}}"]
console.log(reg.exec(str)); // ["{{age}}"]
```

```js
var str = '呵{{gender}}呵呵{{name}}嘿{{age}}嘿嘿';

var reg = /{{([a-z]+)}}/g; // 分组提取功能：()包裹的部分也会进行单独提取

console.log(reg.exec(str)); // ["{{gender}}" "gender"]
console.log(reg.exec(str)); // ["{{name}}" "name"]
console.log(reg.exec(str)); // ["{{age}}" "age"]
```

```js
// 如果希望提取所有满足规则的内容，可以进行while循环

var str = '呵{{gender}}呵呵{{name}}嘿{{age}}嘿嘿';

var reg = /{{[a-z]+}}/g; // 基本使用     g表示global,全局，全部匹配

var result;
while (result = reg.exec(str)) {
      console.log(result);
 }
 
["{{gender}}", index: 1, input: "呵{{gender}}呵呵{{name}}嘿{{age}}嘿嘿"]
["{{name}}", index: 13, input: "呵{{gender}}呵呵{{name}}嘿{{age}}嘿嘿"]
["{{age}}", index: 22, input: "呵{{gender}}呵呵{{name}}嘿{{age}}嘿嘿"]
```

###5.3 replace()替换功能

> replace() 替换功能,replace() 函数用于在字符串中用一些字符替换另一些字符 

> 参数1可以为普通字符串，也可以为正则表达式

```js
var str = 'a1v3b2c4n';    // 希望将所有的数字字符替换为|
var result = str.replace(/\d/g, '|');        \d表示匹配0-9之间任一数字
console.log(result);  ---->"a|v|b|c|n"
```

```js
    var str = '<div>{{name}}今年{{ age }}岁了</div>'
    var reg = /{{\s*([a-zA-Z]+)\s*}}/

    var res = reg.exec(str);
    console.log(res); //---->["{{name}}", "name"]
    str = str.replace(res[0], res[1]);
    console.log(str); //输出<div>name今年{{ age }}岁了</div>

    res = reg.exec(str);
    console.log(res); //---->["{{age}}", "age"]
    str = str.replace(res[0], res[1]);
    console.log(str); //输出<div>name今年age岁了</div>

    res = reg.exec(str);
    console.log(res);   // 输出 null
```

> 使用while循环replace

```js
var str = '<div>{{name}}今年{{ age }}岁了</div>'
var reg = /{{\s*([a-zA-Z]+)\s*}}/

var res;
while (res = reg.exec(str)) {
    str = str.replace(res[0], res[1])
}
console.log(str);  //<div>name今年age岁了</div>
```

> replace替换为data真值 

```js
var str = '<div>{{name}}今年{{ age }}岁了</div>'
var reg = /{{\s*([a-zA-Z]+)\s*}}/

var data = {
        name: '张三',
        age: 20
    }
var res;
while (res = reg.exec(str)) {
     str = str.replace(res[0], data[res[1]])
 }
console.log(str);    //输出<div>张三今年20岁了</div>
```

## 6.实现简易的模板引擎

### 6.1定义模板结构 

```js
<script type="text/template" id="test">
        <div>姓名：{{name}}年龄：{{age}}性别：{{gender}}住址：{{address}}</div>
</script>
```

### 6.2预调用模板引擎 

```js
// 调用模板函数
var  str  =  mytemplate('test', data); // 渲染HTML结构
document.getElementById('box').innerHTML  =  str;
```

### 6.3封装template函数 

```js
//自定义template
        function  mytemplate(id, data)  {  
            var  str  = document.getElementById(id).innerHTML;  
            var  reg =  /{{\s*([a-zA-Z]+)\s*}}/ ;
            var  res;  
            while  ((res  =  reg.exec(str)))  {    
                str  =  str.replace(res[0],  data[res[1]])  
            }
            return  str;
        }
```

## 7. match()提取

```js
    var str = '张三的邮箱zs@qq.com 李四的邮箱ls@qqq.com ';
    var reg = /(\w+)@(\w+\.\w+)/g;

    // match是字符串方法
    console.log(str.match(reg));

    // match和exec的小区别：
    //   - 用法区别
    //   - 功能区别:
    //      - match可以一次提取所有数据，但是没法分组
    //      - exec每次取一个，可以分组
```

# Ajax-day3

## 1. XMLHttpRequest 

> XMLHttpRequest（简称 xhr）是浏览器提供的 Javascript 对象，通过它，可以请求服务器上的数据资源。
>
> 之前所学的 jQuery 中的 Ajax 函数，就是基于 xhr 对象封装出来的.

## 2. get请求基本使用

> **步骤：**

1. 创建xhr对象
2. 调用xhr.open()：设置请求方式和请求地址
3. 调用xhr.send():   发送请求（这一步是异步操作）
4. 设置onreadystatechange事件，监听请求的各种状态
   - readyState是xhr的属性，用来表示请求发送的状态
     - 取值为4代表下载完毕
     - 必须确保readyState为4才能使用响应的数据
   - xhr.status 代表请求是否成功
     - 200代表请求是成功的
   - xhr.responseText 代表接收的响应内容

```js
    // 1 创建xhr对象
    var xhr = new XMLHttpRequest();
    // 2 调用xhr.open()：设置请求方式和请求地址
    xhr.open('GET', 'http://www.liulongbin.top:3006/api/getbooks');
    // 3 调用xhr.send(): 发送请求，这一步是异步操作
    xhr.send();
    // 4 设置事件，监听请求的各种状态
    // readyState是xhr的属性，用来表示请求发送的状态
    //    取值为4代表下载完毕
    //    必须确保readyState为4才能使用响应的数据
    // 进一步检测：
    //      xhr.status 代表请求是否成功
    //      200代表请求是成功的
    xhr.onreadystatechange = function () {
      // 4.1 检测xhr.readyState取值和xhr.status取值
      if (xhr.readyState === 4 && xhr.status === 200) {
        // 4.2 接收响应的数据即可
        // 原生接收的响应内容是JSON格式，需要自己进行转换
        // jQuery会自动转换
        console.log(xhr.responseText);
      }
    };
```

## 3.带有参数的get请求

书写方式：

- **位置：在xhr.open()的参数2 url后面书写参数内容**
- 名称：参数的形式称为**查询字符串**
- 格式：  ?名=值&名=值...
  - 其中  名=值&名=值...  称为**url编码格式，英文为urlencoded**

- jQuery的get请求和原生get请求的**本质是一样**的

```js
    // 1 创建xhr对象
    var xhr = new XMLHttpRequest();
    // 2 调用open：设置请求方式和请求地址
    // 如果希望设置get请求的请求参数，需要放置在open()参数2地址的最后位置
    // 书写方式为：  地址?名=值&名=值....
    // 名称说明： 名=值&名=值称为url编码格式  urlencoded
    xhr.open('GET', 'http://www.liulongbin.top:3006/api/getbooks?id=3&name=jack&age=18');
    // 3 调用send: 发送请求，这一步是异步操作
    xhr.send();
    // 4 设置事件，监听请求的各种状态
    xhr.onreadystatechange = function () {
      // 4.1 检测xhr.readyState取值和xhr.status取值
      if (xhr.readyState === 4 && xhr.status === 200) {
        // 4.2 接收响应的数据即可
        console.log(xhr.responseText);
      }
    };
```

## 4.xhr对象的readyState属性 

> XMLHttpRequest 对象的 readyState 属性，用来表示当前 Ajax 请求所处的状态。每个 Ajax 请求必然处于以下状态中的一个： 

```
值                状态                            描述
0               unsent                  XMLHttpRequest对象已被创建，但尚未调用open（）方法
1               opened                  open（）方法已经被调用
2               headers_received        send（）方法已经被调用，响应头也已经被接收
3               loading                 数据接收中
4                done                   Ajax请求完成，下载完毕
```

## 5.url编码

>URL 地址中，只允许出现英文相关的字母、标点符号、数字，因此，在 URL 地址中不允许出现中文字符。

> 如果 URL 中需要包含中文这样的字符，则必须对中文字符进行编码（转义）。

> URL编码的原则：使用安全的字符（没有特殊用途或者特殊意义的可打印字符）去表示那些不安全的字符。

> URL编码原则的通俗理解：使用英文字符去表示非英文字符。

- **url编码是url对地址的一种处理方式(将中文部分进行编码转换**)
- 浏览器会进行自动的url处理，无需我们自己操作
- 两个用来处理的函数
  - encodeURI() 编码
  - decodeURI() 解码

```js
// 使用encodeURI() 对内容进行编码
console.log(encodeURI('黑马程序员'));
console.log(encodeURI('传智播客'));

// 使用decodeURI() 对内容进行解码
console.log(decodeURI('%E9%BB%91%E9%A9%AC%E7%A8%8B'));
console.log(decodeURI('%E5%BA%8F%E5%91%98'));
```

## 6.post请求的发送方式

> 步骤：

1. 创建xhr对象
2. 调用xhr.open()
3. 设置Content-Type（内容格式、内容类型）
   - xhr.setRequestHeader('Content-Type', 'application/x-www-form-urlencoded')
4. 调用xhr.send(数据)
   - 数据为url编码格式
5. 设置readystatechange事件获取响应内容

```js
    // 1 创建xhr对象
    var xhr = new XMLHttpRequest();

    // 2 调用xhr.open()
    xhr.open('POST', 'http://www.liulongbin.top:3006/api/addbook');

    // 3 设置Content-Type内容格式(固定写法)
    xhr.setRequestHeader('Content-Type', 'application/x-www-form-urlencoded');

    // 4 调用xhr.send()
    //    - 如果具有请求参数，书写在send中，格式也是url编码格式（名=值&名=值...）
    xhr.send('bookname=老人与海&author=海明威&publisher=大海图书出版社');

    // 5 设置readystatechange事件，接收响应的数据
    xhr.onreadystatechange = function () {
      if (xhr.readyState === 4 && xhr.status === 200) {
        console.log(xhr.responseText);
      }
    };
```

## 7.get与post发送方式的区别

> **请求参数的书写位置不同：**

- get请求方式：在xhr.open()的url后面使用?连接
- post请求：在xhr.send()中书写

> **post请求需要设置Content-Type**

## 8.封装ajax函数

> 封装用来将对象转换为url编码的函数

```js
// 封装函数，用于将对象转换为url编码格式
    function urlencoded(obj) {
      var arr = []; // 声明数组用来保存结果
      // 遍历obj，获取所有属性
      for (var k in obj) {
        // k - 属性名 - 字符串类型
        // obj[k] - 属性值
        arr.push(k + '=' + obj[k]);
      }
      return arr.join('&');
    }
```

> 封装ajax函数

- **转换字符串为大小写的字符串方法**
  - 字符串.toUpperCase() 转换为大写字母
  - 字符串.toLowerCase() 转换为小写字母

```
 // 封装用来发送ajax请求的函数
    //  参数：
    //    对象
    //      - type 请求方式
    //      - url 请求地址
    //      - data 请求参数
    //      - success 回调函数
```

```js
     function ajax(options) {
      // 1 创建xhr对象
      var xhr = new XMLHttpRequest();
      // 2 设置请求的相关信息: 需要根据请求方式分别设置
      //  统一保存数据
      var data = urlencoded(options.data);
      //  2.1 将请求方式统一转换为大写(或小写)
      var type = options.type.toUpperCase();
      //  2.2 对请求方式进行检测
      if (type === 'GET') {
        xhr.open('GET', options.url + '?' + data);
        xhr.send();
      } else if (type === 'POST') {
        xhr.open('POST', options.url);
        xhr.setRequestHeader('Content-Type', 'application/x-www-form-urlencoded');
        xhr.send(data);
      }
      // 3 设置事件接收响应内容
      xhr.onreadystatechange = function () {
        // 3.1 检测
        if (xhr.readyState === 4 && xhr.status === 200) {
          // 3.2 将JSON格式的字符串转换为对象
          var res = JSON.parse(xhr.responseText);
          options.success(res);
        }
      };
    }

// 进行数据处理的函数
    function urlencoded(obj) {
      var arr = []; // 声明数组用来保存结果
      // 遍历obj，获取所有属性
      for (var k in obj) {
        // k - 属性名 - 字符串类型
        // obj[k] - 属性值
        arr.push(k + '=' + obj[k]);
      }
      return arr.join('&');
    }
```

```
可选：可以给ajax函数的options中的属性设置默认值

- type默认值为'GET'
- data默认为''
- success如果不存在，则不进行调用，避免报错
```

## 9. XMLHttpRequest Level2的新功能 

> 可以设置 HTTP 请求的时限

> 可以使用 FormData 对象管理表单数据

> 可以上传文件

> 可以获得数据传输的进度信息

### 9.1设置HTTP请求时限 

> 设置方式：

- 属性：  xhr.timeout = 超时时间; //  毫秒单位
- 时间：  xhr.ontimeout = function() { 请求超时后，触发的事件 };

```js
    var xhr = new XMLHttpRequest();
    xhr.open('GET', 'http://www.liulongbin.top:3006/api/getbooks');

    // 设置请求的超时时间(毫秒单位)
    xhr.timeout = 500;

    // 设置事件，对超时进行处理
    xhr.ontimeout = function () {
      console.log('网络开小差了，请稍后再试!~');
    };
    xhr.send();
    xhr.onreadystatechange = function () {
      if (xhr.readyState === 4 && xhr.status === 200) {
        console.log(xhr.responseText);
      }
    };
```

###9.2FormData管理表单数据

> FormData的作用：

- 可以快速处理表单的数据
- 可以进行文件上传

> **注意点：**

- **发送FormData需要使用POST请求方式**
- **不需要单独设置Content-Type**

> 使用方式：

> 1.单独发送数据:创建空FormData对象，添加数据后发送

```js
      // 1.1 创建FormData对象
      var fd = new FormData(); // 空的FormData对象
      // 1.2 向fd中添加一些数据
      fd.append('name', 'jack');
      fd.append('age', 18);
  
      // 1.3 使用POST方法将fd发送到对应接口（此处的接口为formdata）
      //  无需设置之前post的content-type
      var xhr = new XMLHttpRequest();
      xhr.open('POST', 'http://www.liulongbin.top:3006/api/formdata');
      xhr.send(fd); // 将fd放入在send()参数中即可
      xhr.onreadystatechange = function () {
        if (xhr.readyState === 4 && xhr.status === 200) {
          console.log(xhr.responseText);
        }
      };
```
> 2.处理表单数据:通过form表单获取数据后发送

```js
  <!-- 设置form标签，用来进行formdata操作 -->
    <form id="testForm">
      <!-- 如果要表单元素数据被请求发送，必须设置name -->
      <input type="text" name="username">
      <input type="password" name="password">
      <!-- 设置按钮，点击后，使用FormData处理表单数据 -->
      <button type="button" id="btn">ajax提交</button>
    </form>
  
  // 2 通过FormData对象管理表单元素，再发送(同时也可以添加数据)
      document.getElementById('btn').onclick = function () {
        // 2.1 创建FormData对象，传入DOM对象形式的form标签到参数中
        var testForm = document.getElementById('testForm');
        var fd = new FormData(testForm); // 空的FormData对象
  
        // 2.1.1 也可以在存在form的基础上，自己添加数据
        fd.append('name', 'rose');
        fd.append('age', 21);
  
        // 2.3 使用POST方法将fd发送到对应接口（此处的接口为formdata）
        //  - 无需设置之前post的content-type
        var xhr = new XMLHttpRequest();
        xhr.open('POST', 'http://www.liulongbin.top:3006/api/formdata');
        xhr.send(fd); // 将fd放入在send()参数中即可
        xhr.onreadystatechange = function () {
          if (xhr.readyState === 4 && xhr.status === 200) {
            console.log(xhr.responseText);
          }
        };
      }
```
### 9.3文件上传

- **1 准备结构(文件域)**

```html
<input type="file">
```

- **2 检测用户是否选择了文件**
  - 对DOM对象形式的input[type="file"]的**files**属性进行检测
    - 如果内部存储了任意的一个值，就说明选取了文件，否则就是没选
- 3 使用FormData保存文件信息
  - 使用fd.append()添加即可
- 4 通过ajax发送
- 5 响应处理，展示服务端获取到的图片

```js
    <input type="file" id="iptFile">
    <button type="button" id="btn">点击上传文件</button>
    <img src="" alt="" id="pic">
    
    // 1 给按钮设置点击事件
    var btn = document.getElementById('btn');
    var iptFile = document.querySelector('#iptFile');
    var pic = document.getElementById('pic');
    
    btn.onclick = function () {
      // 2 检测是否上传了文件，需要检测文件域的files属性
      //  files是一个伪数组，可以通过判断length，检测是否选择了文件
      //console.dir(iptFile);
      if (iptFile.files.length === 0) {
        // 说明没有选择文件
        alert('请选择文件后提交!~');
        return;
      }

      // 3 通过FormData保存文件信息
      var fd = new FormData();
      // avatar是接口中规定的请求参数名称
      // files[0]代表选择的文件的相关信息
      fd.append('avatar', iptFile.files[0]);

      // 4 发送post形式的ajax，将fd发送给服务端处理
      var xhr = new XMLHttpRequest();
      xhr.open('POST', 'http://www.liulongbin.top:3006/api/upload/avatar');
      xhr.send(fd);

      // 5 接收响应数据
      xhr.onreadystatechange = function () {
        if (xhr.readyState === 4 && xhr.status === 200) {
          var res = JSON.parse(xhr.responseText);
          // 5.1 检测上传是否成功
          if (res.status === 200) {
            // 5.2 将响应的图片在线地址，放入到img中展示
            pic.src = 'http://www.liulongbin.top:3006' + res.url
          }
        }
      }
    };
```

> jQuery使用FormData上传文件的注意点

- 必须设置两个属性
  - contentType: false 不指定内容类型
  - processData: false 不进行数据处理

###9.4上传进度条功能

> xhr.upload.onprogress     上传中实时触发事件

> 事件对象e的属性

- e.lengthComputable       是一个布尔值，表示当前上传的资源是否具有可计算的长度 
- e.loaded                            已传输的字节
- e.total                                 需传输的总字节 

> xhr.upload.onload         上传完毕时触发事件

```js
 /*
      1 检测上传过程的事件
        xhr.upload.onprogress = function(e) ...
      2 检测文件大小是否可用
        e.lengthComputable 布尔值
      3 计算进度
        e.loaded 已加载的大小
        e.total  总大小
      3.1 计算方式
        e.loaded / e.total 上传的进度

      制作进度条功能的思路：
        - 设置内外两个盒子，外部盒子定宽度，内部盒子宽度默认为0
        - 上传中，根据上传的进度设置内部盒子宽度对应改变即可

      xhr.upload.onload 上传完毕后触发的事件
    */

    var btn = document.getElementById('btn');
    var iptFile = document.querySelector('#iptFile');
    var pic = document.getElementById('pic');

    btn.onclick = function () {
      // 2 检测是否上传了文件，需要检测文件域的files属性
      if (iptFile.files.length === 0) {
        alert('请选择文件后提交!~');
        return;
      }

      // 3 通过FormData保存文件信息
      var fd = new FormData();
      fd.append('avatar', iptFile.files[0]);

      // 4 发送post形式的ajax，将fd发送给服务端处理
      var xhr = new XMLHttpRequest();

      // 设置上传文件的进度监测
      xhr.upload.onprogress = function (e) {
        // 判断e.lengthComputable是否为true，为true表示可以进行计算
        if (e.lengthComputable) {
          // 根据e.loaded和e.total计算进度比例
          var bili = e.loaded / e.total * 100 + '%';
          console.log(e);
          document.getElementById('percent').style.width = bili;
          document.getElementById('percent').innerText = bili;
        }
      };

      // 设置上传文件完成的事件(更改样式)
      xhr.upload.onload = function () {
        document.getElementById('percent').className = 'progress-bar progress-bar-success';
      }

      xhr.open('POST', 'http://www.liulongbin.top:3006/api/upload/avatar');
      xhr.send(fd);

      // 5 接收响应数据
      xhr.onreadystatechange = function () {
        if (xhr.readyState === 4 && xhr.status === 200) {
          var res = JSON.parse(xhr.responseText);
          // 5.1 检测上传是否成功
          if (res.status === 200) {
            // 5.2 将响应的图片在线地址，放入到img中展示
            console.log(res);
          }
        }
      }
    };
```

# Ajax-day4

## 1.JSON 

> 概念：JSON 的英文全称是 JavaScript Object Notation，即“JavaScript 对象表示法”。简单来讲，JSON 就是 Javascript 对象和数组的字符串表示法，它使用文本表示一个 JS 对象或数组的信息，因此，JSON 的本质是字符串。

> 作用：JSON 是一种轻量级的文本数据交换格式，在作用上类似于 XML，专门用于存储和传输数据，但是 JSON 比 XML 更小、更快、更易解析。

> 现状：JSON 是在 2001 年开始被推广和使用的数据格式，现在，JSON 已经成为主流的数据交换格式。

### 1.1 JSON的两种结构 

JSON 中包含对象和数组两种结构，通过这两种结构的相互嵌套，可以表示各种复杂的数据结构。

> 对象结构 
>
> 在 JSON 中表示为 { } 括起来的内容。数据结构为 { key: value, key: value, … } 的键值对结构。其中，key 必须是使用英文的双引号包裹的字符串，value 的数据类型可以是数字、字符串、布尔值、null、数组、对象6种类型。 

> 数组结构 
>
> 在 JSON 中表示为 [ ] 括起来的内容。数据结构为 [ "java", "javascript", 30, true … ] 。数组中数据的类型可以是数字、字符串、布尔值、null、数组、对象6种类型。

### 1.2 JSON语法注意事项 

```
属性名必须使用双引号包裹
字符串类型的值必须使用双引号包裹
JSON 中不允许使用单引号表示字符串
JSON 中不能写注释
JSON 的最外层必须是对象或数组格式
不能使用 undefined 或函数作为 JSON 的值
```

> JSON 的作用：在计算机与网络之间存储和传输数据。

> JSON 的本质：用字符串来表示 Javascript 对象数据或数组数据

### 1.3JSON和JS对象 

> JSON 是 JS 对象的字符串表示法，它使用文本表示一个 JS 对象的信息，本质是一个字符串。 

> 从 JSON 字符串转换为 JS 对象，使用 JSON.parse() 方法,
>
> 从 JS 对象转换为 JSON 字符串，使用 JSON.stringify() 方法 

>数据对象转换为字符串的过程，叫做序列化，   调用 JSON.stringify() 函数的操作，叫做 JSON 序列化。
>
>字符串转换为数据对象的过程，叫做反序列化，调用 JSON.parse() 函数的操作，叫做 JSON 反序列化。

###1.4 JSON的使用-深拷贝

> 常见使用场景:

> 1 本地存储

> 2 对象拷贝:对不具有方法的数据对象进行快速深拷贝操作

```js
var obj = {
            name: 'rose',
            age: 21,
            gender: '男',
            arr: [1, 2, 3],
            data: {
                a: 2,
                e: 3
            }
        };

        var obj2 = JSON.parse(JSON.stringify(obj));
        
        console.log(obj);    // {name: "rose", age: 21, gender: "男", arr: Array(3), data: {…}}
        console.log(obj2);    //{name: "rose", age: 21, gender: "男", arr: Array(3), data: {…}}
        
        obj.name = 'jack';
        obj.data.a = 200;
        console.log(obj);
        console.log(obj2);
```

> ajax
>
> 封装原生ajax函数时，需要自己将响应的JSON数据转换为js对象，使用JSON.parse()
>
> 如果使用js库进行ajax操作，例如jQuery，内部已经封装了JSON转换，就无需我们操作了

##2.jQuery的全局ajax处理器

> 作用：用来对页面中的ajax操作进行统一设置，简化操作
>
> 常见场景：加载资源的loading功能

> ajaxStart() 任意请求开始时触发内部回调

```js
//使用全局ajax处理器检测请求发送的操作，并将loading图展示
    $(document).ajaxStart(function () {
      // console.log('发送了ajax请求');
      $('img').show();
    });
```
> ajaxStop() 任意请求结束后触发内部回调

```js
//使用全局ajax处理器检测请求完毕的状态，并将loading图隐藏
$(document).ajaxStop(function () {
      $('img').hide();
    });
```
> 在ajax内部自己封装加载资源的loading功能

```js
$("#btn").on("click", function() {
            $("img").show();       //在请求开始之前将loading图展示
            $.ajax({
                url: "http://www.liulongbin.top:3006/api/getbooks",
                success: function(res) {
                    $(".box").html(JSON.stringify(res));
                    $("img").hide();      //请求完毕，并将loading图隐藏
                }
            })
        })
```

## 3. axios的使用

> Axios 是专注于网络数据请求的库。

> 相比于原生的 XMLHttpRequest 对象，axios 简单易用。

> 相比于 jQuery，axios 更加轻量化，只专注于网络数据请求。

###3.1 axios.get()的使用

```js
// axios.get('地址', {params: {数据。。。}}).then(成功时的处理函数);

 axios.get('http://www.liulongbin.top:3006/api/getbooks', {
      params: {
        id: 2
      }
    })
      .then(function (res) {
        // axios对响应的res部分进行了包装，之前jQuery中的res，相当于axios中的res.data
        //  - 刚开始使用时，可以使用以下操作
        res = res.data;
        console.log(res);
      }); 
```

###3.2 axios.post()的使用

```js
// axios.post('地址', {数据。。。}).then(成功时的处理函数)

    axios.post('http://www.liulongbin.top:3006/api/post', {
      name: 'jack',
      age: 18
    })
      .then(function (res) {
        console.log(res);
      });
```

###3.3 axios()的使用

> 发送get和post的区别：

- **设置请求参数的属性名不同**
  - get请求参数的属性名为params
  - post请求参数的属性名为data

####3.3.1 axios()发送get请求

```js
axios({
      method: 'GET',
      url: 'http://www.liulongbin.top:3006/api/get',
      params: {
        name: 'jack',
        age: 18
      }
    })
      .then(function (res) {
        console.log(res.data);
      });
```

####3.3.2 axios()发送post请求

```js
axios({
      method: 'POST',
      url: 'http://www.liulongbin.top:3006/api/post',
      data: {
        name: 'rose',
        age: 21
      }
    })
      .then(function (res) {
        console.log(res.data);
      });
```
##4.同源策略和跨域

###4.1同源(同源地址)

> 指的是两个页面地址的 **协议 域名 端口** 完全一样，这两个地址就是同源的，或者称为同源地址。

- 我们发现，在现代网站中(京东)一个公司可能具有很多的域名，也都不是同源地址，如果在公司内部都不能进行数据请求，是很不方便的。

### 4.2同源策略

> 同源策略（英文全称 Same origin policy）是浏览器提供的一个安全功能。 

>同源策略不允许和非同源的网站之间发送ajax请求

> 发送跨域请求时，请求发送是成功的，响应也是成功的，只不过浏览器将响应的信息拦截了，我们无法操作。

- 对我们操作的影响，无法对非同源的地址发送ajax请求(不能跨域)

### 4.3跨域

> 跨域指的是非同源网站之间发送ajax请求

> 现在，实现跨域数据请求，最主要的两种解决方案，分别是 JSONP 和 CORS。

> JSONP
>
> 兼容性好，但是只支持GET

>CORS
>
>兼容性不太好，但是支持GET、POST，并且是标准中提供的方式。

####4.3.1跨域方式-JSONP

> JSONP：出现的早，兼容性好（兼容低版本IE）。是前端程序员为了解决跨域问题，被迫想出来的一种临时解决方案。缺点是只支持 GET 请求，不支持 POST 请求。

> JSONP (JSON with Padding) 是 JSON 的一种“使用模式”，可用于解决主流浏览器的跨域数据访问的问题。 

>由于浏览器同源策略的限制，网页中无法通过 Ajax 请求非同源的接口数据。
>
>但是 <script> 标签不受浏览器同源策略的影响，可以通过 src 属性，请求非同源的 js 脚本。
>
>JSONP 的实现原理:
>
>通过 <script> 标签的 src 属性，请求跨域的数据接口，并通过函数调用的形式，接收跨域接口响应回来的数据。

####4.3.2跨域方式-CORS

CORS：出现的较晚，它是 W3C 标准，属于跨域 Ajax 请求的根本解决方案。支持 GET 和 POST 请求。缺点是不兼容某些低版本的浏览器。

#### 4.3.3JSONP的实现原理

> JSONP的实现原理：
>
> 同源策略不限制script标签对非同源地址进行请求
>
> 可以借助script标签进行JSONP实现

```js
<!-- 
    使用JSONP进行请求处理
      步骤:
        1 准备一个处理函数
        2 通过script标签的src属性，进行接口的请求
          - 因为同源策略不会限制script标签的功能
        3 请求时传入请求参数
          - callback 用来传递本地处理函数的函数名
          - 其他参数随便写
        4 当响应结束后，步骤1设置的处理函数会自动调用
          - 可以在处理函数中对响应数据进行后续处理
  -->
  <script>
    function fun(res) {
      console.log(res);
    }
  </script>
  <script src="http://ajax.frontend.itheima.net:3006/api/jsonp?callback=fun&name=jack"></script>

```

> 说明：

- JSONP和JSON没有本质关联
- **JSONP与ajax没有任何关联**
  - JSONP是使用script标签进行请求发送
  - ajax是通过浏览器提供的XMLHttpRequest对象发送

#### 4.3.4 jQuery发送JSONP请求的方式

> jQuery 中的 JSONP，也是通过 <script> 标签的 src 属性实现跨域数据访问的,
>
> 只不过，jQuery 采用的是动态创建和移除 <script> 标签的方式，来发起 JSONP 数据请求。

> 在发起 JSONP 请求的时候，动态向 <header> 中 append 一个 <script> 标签；
>
> 在 JSONP 请求成功以后，动态从 <header> 中移除刚才 append 进去的 <script> 标签；

> jQuery使用的是$.ajax()方法进行JSONP操作,

- **设置dataType属性为'jsonp'**

- 说明：
  - 可以从浏览器的network看到请求的类型为 script 
  - jQuery会将使用过的用于发送jsonp请求的script标签移除，打开页面也看不到

```js
	$.ajax({
      type: 'GET',
      url: 'http://ajax.frontend.itheima.net:3006/api/jsonp',
      data: {
        name: 'jack',
        age: 18
      },
      
      // 下面的两个属性作为了解即可，通常不会使用
      //jsonp: 'xyz',          // 将默认的请求参数名callback设置为其他名称
      //jsonpCallback: 'abc',  // 将处理函数名称设置为指定名称
    
      dataType: 'jsonp',      // 设置这句话后，jQuery就会使用JSONP的方式进行请求发送
      success: function (res) {
        console.log(res);
      }
    });
```

## 5.淘宝搜索框案例

###5.1 基本功能实现

>  1 通过keyup事件监听用户的输入操作
>
>  2 检测内容是否为空
>
>  3 通过JSONP请求方式，请求taobao的搜索建议
>
> 4  通过模板引擎根据数据进行结构创建

```js
    // 1 设置keyup事件监听用户的输入操作
    $('#ipt').on('keyup', function () {
      // 1.1 获取输入内容并进行检测
      var val = $(this).val().trim();
      if (val === '') {
        // 如果内容为空，可以将底部建议列表的内容清空，同时隐藏
        $('#suggest-list').empty().hide();
        return;
      }
      // 2 使用JSONP请求淘宝的数据
      $.ajax({
        url: 'https://suggest.taobao.com/sug',
        data: { q: val },     // 淘宝的这个接口指定了请求参数名为q,代表要查询的内容
        dataType: 'jsonp',    // 使用jsonp方式发送请求
        success: function (res) {
          // 3 检测是否获取到了可以展示的数据
          if (res.result.length === 0) {
            // 如果响应的数据为空，可以将底部建议列表的内容清空，同时隐藏
            $('#suggest-list').empty().hide();
            return;
          }
          // 3.1 通过模板引擎进行建议列表结构生成
          var htmlStr = template('suggest', res);
          $('#suggest-list').html(htmlStr).show();
        }
      });
    });
```

###5.2使用临时对象保存数据减少请求发送

> 原因：某些内容搜索后，一段时间内再次搜索时内容也不会有变化，我们就可以将每次取得的数据保存下来
>
> ​           下次再输入相同内容时，就无需再次请求了
>
>  1 创建一个用来保存临时数据的空对象
>
>  2 当搜索的内容响应接收成功后，保存在临时对象中
>
>  3 当以后输入内容时，先检测临时对象中是否存在对应数据
>
> ​        \- 如果有，取出来直接使用
>
> ​        \- 如果没有，再发送请求

```js
<!-- 设置用于进行建议列表生成的模板 -->
<script type="text/template" id="suggest">
  {{each result val}}
    <div class="suggest-item">{{val[0]}}</div>
  {{/each}}
</script>

<script>
     // -- 创建临时对象，用来存储搜索过的数据
     var cacheObj = {};

    //  - 可以设置定时器，过一段时间清空cacheObj
    setInterval(function () {
      cacheObj = {};
    }, 1 * 60 * 60 * 1000); // 例如设置每隔一小时更新一次

    // 1 设置事件
    $('#ipt').on('keyup', function () {
      // 1.1 获取输入内容并进行检测
      var val = $(this).val().trim();
      if (val === '') {
        // 如果内容为空，可以将底部建议列表的内容清空，同时隐藏
        $('#suggest-list').empty().hide();
        return;
      }
      // -- 检测临时对象中是否具有之前保存的数据 
      if (cacheObj[val]) {
        // - 根据临时对象中的数据进行结构创建
        renderList(cacheObj[val]);
        return;
      }
      // 2 使用JSONP请求淘宝的数据
      $.ajax({
        url: 'https://suggest.taobao.com/sug',
        data: { q: val },// 淘宝的这个接口指定了请求参数名为q,代表要查询的内容
        dataType: 'jsonp', // 使用jsonp方式发送请求
        success: function (res) {
          // 3 检测数据并创建结构(封装为函数，在多个地方使用)
          renderList(res);
        }
      });
    });

    // 封装函数，用来进行建议列表结构创建
    function renderList(res) {
      // 3 检测是否获取到了可以展示的数据
      if (res.result.length === 0) {
        // 如果响应的数据为空，可以将底部建议列表的内容清空，同时隐藏
        $('#suggest-list').empty().hide();
        return;
      }
      // 3.1 通过模板引擎进行建议列表结构生成
      var htmlStr = template('suggest', res);
      $('#suggest-list').html(htmlStr).show();
      // -- 将本次接收的数据保存在临时对象中，用于下次使用
      //  - 设置时：属性名为搜索的内容，属性值为响应的内容
      var val = $('#ipt').val().trim();
      cacheObj[val] = res;
    }
</script>
```

### 5.3 防抖处理

> 多次进行输入操作，每次都需要发送请求，有些请求是没有必要发送的
>
> 例如输入adidas, 过程中输入的a和ad和adi和adid和adida都没有必要搜索
>
> 设置防抖操作可以减少页面中不必要的请求次数

>设置方式：
>
>请求发送操作不是直接进行的，而是通过定时器控制 setTimeout
>
>设置一个指定的间隔时间，例如100ms(实际会更小)
>
> 当间隔时间中再次进行了输入，重置定时器（将旧的定时器清除，再开启新的定时器即可）
>
>简单来说：就是以满足间隔的最后一次输入为准

```js
    // -- 创建临时对象，用来存储搜索过的数据
    var cacheObj = {};

    // --- 设置防抖功能
    var timer = null; // 用来保存进行防抖操作的定时器id

    //  - 可以设置定时器，过一段时间清空cacheObj
    setInterval(function () {
      cacheObj = {};
    }, 1 * 60 * 60 * 1000); // 例如设置每隔一小时更新一次

    // 1 设置事件
    $('#ipt').on('keyup', function () {
      // --- 如果再次输入，将上次的定时器清除即可
      clearTimeout(timer);

      // 1.1 获取输入内容并进行检测
      var val = $(this).val().trim();
      if (val === '') {
        // 如果内容为空，可以将底部建议列表的内容清空，同时隐藏
        $('#suggest-list').empty().hide();
        return;
      }
        
      // -- 检测临时对象中是否具有之前保存的数据 
      if (cacheObj[val]) {
        // - 根据临时对象中的数据进行结构创建
        renderList(cacheObj[val]);
        return;
      }
        
      // 2 使用JSONP请求淘宝的数据
      // --- 通过定时器控制
      timer = setTimeout(function () {
        getData(val);
      }, 100);
    });
    // 防抖

    // 封装函数，用来进行数据请求
    function getData(val) {
      $.ajax({
        url: 'https://suggest.taobao.com/sug',
        data: { q: val },// 淘宝的这个接口指定了请求参数名为q,代表要查询的内容
        dataType: 'jsonp', // 使用jsonp方式发送请求
        success: function (res) {
          // 3 检测数据并创建结构(封装为函数，在多个地方使用)
          renderList(res);
        }
      });
    }
```

##6.防抖和节流

### 6.1防抖

> 防抖策略（debounce）是当事件被触发后，延迟 n 秒后再执行回调，如果在这 n 秒内事件又被触发，则重新计时。 

> 进行重复操作时，设置时间间隔，以最后一次满足间隔的操作为准进行执行。
>
> 简单来说：**就是以满足间隔的最后一次为准执行事件**
>
> 应用场景 ：用户在输入框中连续输入一串字符时，可以通过防抖策略，只在输入完后，才执行查询的请求，这样可以有效减少请求次数，节约请求资源。见淘宝搜索框案例

###6.2节流

> 节流策略（throttle），顾名思义，可以减少一段时间内事件的触发频率。 

> 概念：也可以称为函数节流，目的是减少某些操作的触发速度

> 节流的应用场景 :mousemove事件        scroll等事件
>
> 鼠标连续不断地触发某事件（如点击），只在单位时间内只触发一次 事件；
>
> 懒加载时要监听计算滚动条的位置，但不必每次滑动都触发，可以降低计算的频率，而不必去浪费 CPU 资源 

```js
//让操作以指定间隔执行
//通过定时器进行设置
//在指定的时间间隔内再次触发操作会被忽略
//直到本次操作完毕，才允许执行下一次
<body>
  <img src="./angel.gif" alt="" id="angel" />
  <script>
    // 我们希望mousemove事件执行间隔变大，至少为100ms，可以使用节流操作
    var flag = true; // 默认为true代表可以执行操作

    // 1 设置鼠标移动事件
    $(document).on('mousemove', function (e) {
      if (flag !== true) {
        return;
      }
      flag = false; // 设置下次无法触发
      setTimeout(function () {
        // 2 将鼠标的横纵坐标设置给img的left和top即可
        $('#angel').css({
          left: e.pageX,
          top: e.pageY
        });
        flag = true; // 本次间隔后操作执行后，允许进行下次操作
      }, 20);
    });
  </script>
</body>
```

###6.3节流和防抖的区别：

> 防抖是当指定间隔时间内再次触发，使用新触发的操作再次重新记时。
>
> 节流是在指定间隔时间内再次触发，新操作会被忽略。

> 防抖：如果事件被频繁触发，防抖能保证只有最后一次触发生效！前面 N 多次的触发都会被忽略！

> 节流：如果事件被频繁触发，节流能够减少事件触发的频率，因此，节流是有选择性地执行一部分事件！

##7.HTTP协议

### 7.1通信

> 通信，就是信息的传递和交换。
>
> 通信三要素：通信的主体       通信的内容       通信的方式

### 7.2通信协议 

>通信协议（Communication Protocol）是指通信的双方完成通信所必须遵守的规则和约定。
>
>通俗理解：通信双方采用约定好的格式来发送和接收消息，这种事先约定好的通信格式，就叫做通信协议。

> 客户端与服务器之间要实现网页内容的传输，则通信的双方必须遵守网页内容的传输协议。 
>
> 网页内容的传输协议又叫做超文本传输协议（HyperText Transfer Protocol） ，简称 HTTP 协议。

### 7.3 HTTP协议

> HTTP 协议即超文本传输协议 (HyperText Transfer Protocol) ，它规定了客户端与服务器之间进行网页内容传输时，所必须遵守的传输格式。 

> HTTP 协议采用了 请求/响应 的交互模型。 

### 7.4 HTTP请求消息 

>由于 HTTP 协议属于客户端浏览器和服务器之间的通信协议。因此，客户端发起的请求叫做 HTTP 请求，客户端发送到服务器的消息，叫做 HTTP 请求消息。
>
>注意：HTTP 请求消息又叫做 HTTP 请求报文。

##8.HTTP的请求报文和响应报文

> 内容传输格式分为**请求报文**和**响应报文**两种

###8.1请求报文

> 请求报文:客户端给服务端发送请求时发送的那些内容

> **请求报文由4部分组成**:

- **请求行**(request line )
  - 3部分组成：  请求方式           请求地址URL           HTTP协议版本
- **请求头**：**用来保存客户端的相关信息**(大部分是浏览器自动设置的)
  - Host：主机地址，服务器域名
  - User-Agent：用户代理字符串，客户端的一些浏览器和系统信息
  - Content-Type：发送的请求体的内容类型(数据格式)
- 空行：请求头字段的后面是一个空行，通知服务器请求头部至此结束，用来分隔请求头部与请求体。
- **请求体**：**就是通过 POST 方式发送的请求参数**
  - **get请求的参数在url中发送，请求体为空**，只有 POST 请求才有请求体，GET 请求没有请求体
  - **post请求的参数在请求体中**，所以需要设置Content-Type

###8.2响应报文

> 响应消息就是服务器响应给客户端的消息内容，也叫作响应报文。 

> 响应报文由4部分组成:

- **状态行**
  - 由3部分组成： HTTP 协议版本         状态码        状态码的描述文本
- **响应头**：用来**保存服务端的相关信息**(有的是服务端自动设置的，有的是后端自己设置的)
  - Content-Type: 响应体的内容类型
- 空行:分隔响应头部与响应体 
- **响应体**
  - **服务端发送给客户端的响应内容**（无论什么请求方式，响应的数据都在响应体中保存）
  - 例如我们在jQuery中接收的res就是响应体

## 9.HTTP请求方法 

> 最常用的是GET和POST

- GET 用来获取数据（查询）
- POST 用来发送数据（新增）
- PUT 用来修改数据（修改）
- DELETE  用来删除数据（删除）

## 10.HTTP响应状态码

> HTTP 响应状态码（HTTP Status Code），用来标识响应的状态。 
>
> 通过一些数字表示本次请求的状态：除了状态码还会配有状态文本

* **1xx** 信息，服务器收到请求，需要请求者继续执行操作

- **2xx 成功**，操作被成功接收并处理

  - 常见的是200，请求成功。
  - 201，已创建

- **3xx 重定向**，需要进一步的操作以完成请求

  - (我们请求a.html，服务端认为a.html有问题，没法给你看，将你的请求转给了b.html)
  - 常见：304 读取缓存的内容了
  - 301  永久重定向
  - 302  临时重定向

- **4xx 客户端错误**，请求包含语法错误或无法完成请求

  - 404    Not Found      服务器无法根据客户端的请求找到资源
  - 408    请求超时
  - 401     没有访问权限

- **5xx 服务器错误**，服务器在处理请求的过程中发生了错误

  - 500     服务器内部错误，无法完成请求
  - 501     服务器不支持该请求方法
  - 503     服务器由于超载或者系统维护，暂时无法处理客户端请求

  