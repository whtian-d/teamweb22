# vue第1天

## vue-介绍

Vue.js (view)是一套构建用户界面的前端框架技术（渐进式框架）。

内部集成了许多基础技术，例如html、css、javascript、ajax、node等，当然还有vue本身高级技术体现，例如组件、过滤器、指令、路由、webpack等等.

2012年由中国人尤雨溪开发，正式发布于2014年2月 ，2016年3月加入阿里巴巴公司(该事件助推了vue的发展)

> jquery：库  侵入性弱   (工具 库)，项目 对其进行 安装卸载 非常方便
>
> vue：框架   侵入性强    (框架)，项目 从内到外 都是vue，不可以随便拆卸

Vue只关注**视图**（页面）层的开发，文档非常丰富、易于上手，流行度高，拥抱经典的web技术、早期灵感来源于angular

vue.js兼具angular.js和react.js的优点，并剔除了它们的缺点

支持所有兼容ECMAScript 5的浏览器，IE9以上     Vue.js 不支持 IE8 及其以下版本

vue是前端的主流框架之一，和**Angular**、**React** 一起，并成为前端三大主流框架！

## MVVM设计模式

m: model  数据部分  data

v：view  视图部分  div容器

vm： view & model 视图和数据 的 结合体

## vue基本使用

 ```html
<!-- 2. 创建一个供vue操控的 标签容器(推荐是div) -->
  <div id="app">
    <!-- 输出vue实例的data数据,在HTML中使用data里面的数据不需要加this -->
    {{ city }}--------{{ weather }}
  </div>

 <!-- 1.引入vue文件包，此时系统增加了一个全局变量为Vue(类似引入jquery.js，系统增加$符号全局变量) -->
  <script src="./vue.js"></script>

  <script>
    // 3. 实例化Vue对象
    var vm = new Vue({
      // el:'选择器' ,// el固定名称，理解为element，使得 Vue实例 与 标签容器 联系
      el:'#app',
      // data固定名称，给 Vue实例 声明数据，用于使用
      data:{
        city:'北京',
        weather:'sunshine'
      }
    })
  </script>
 ```

## vue指令

### 插值表达式{{}}

```html
<标签> {{ 表达式 }} </标签>
```

> 表达式：变量、常量、算术运算符、比较运算符、逻辑运算符、三元运算符等等

如果{{}}使用中有冲突，想更换为其他标记，可以这样：

```js
delimiters:['${'，'}$']  // 标记符号变为${  }$了 
```

> 插值表达式只能用在html标签的**内容区域**；不能用在其他地方

插值表达式使用时，页面加载时出现会闪烁问题

解决方法：v-cloak

```css
<style type="text/css">
  /* 通过属性选择器 选择到 带有属性 v-cloak的标签  让他隐藏*/
  [v-cloak]{
    /* 元素隐藏    */
    display: none;
  }
  </style>
```

```html
<div id="app">
    <!-- 2、 让带有插值 语法的   添加 v-cloak 属性 
         在 数据渲染完成之后，v-cloak 属性会被自动去除，
         v-cloak一旦移除也就是没有这个属性了  属性选择器就选择不到该标签
		 也就是对应的标签会变为可见
    -->
    <div  v-cloak  >{{msg}}</div>
</div>
```

### v-text

v-text与{{}}的作用是一样的，都是操控标签的**内容区域**信息

```html
<标签 v-text="表达式"> </标签>
```

>v-text 是通过标签的**属性**形式呈现
>
>如果 标签 内容区域 有默认信息，则会被v-text覆盖掉
>
>v-text 可以进行 变量、常量、算术符号、比较符号、逻辑符号、三元运算符号等运算

### v-html

v-html 与 v-text、{{ }} 的作用一样，都是操控 标签的**内容区域**

```html
<标签 v-html="表达式"> </标签>
```

> v-html、v-text、{{ }}的异同：

1. v-html对 **html标签** 和 **普通文本** 内容都可以设置显示
2. v-text、{{ }}  只针对  **字符串** 起作用，如果数据中有html标签，那么标签的箭头符号要做字符实体转换，进而使得浏览器上直接"显示箭头"等标签内容，等同于不解析html标签内容
   * <  变为  \&lt;       // less than
   * \> 变为  \&gt;       // great than
3. v-html和v-text没有闪烁问题
4. 它们都可以进行 **变量**、**常量**、**算术运算**、**比较运算**、**逻辑运算**、**三元运算**等技术应用

> 应用场景

如果服务器返回的数据中，包含有HTML标签(例如富文本编辑器内容)，可以使用 v-html 来渲染,(v-text和 {{}}都不行)

> 默认内容

```html
<p>{{score}}默认内容</p>
<p v-text="score">默认内容</p>
<p v-html="score">默认内容</p>
```

> 以上三者，v-text和v-html标签有默认内容，但是都会被覆盖掉，而 插值表达式 不会覆盖

注意：

1. v-html尽量避免使用(除非完全掌控)，否则会带来危险(XSS攻击 跨站脚本攻击)
2. 标签的默认内容会被v-html覆盖

###  v-bind(冒号)

####属性绑定-基本使用

使用 v-bind指令 对标签属性进行绑定

```html
<标签 v-bind:属性名称="表达式" ></标签>
<标签 :属性名称="表达式"></标签>  // 简易方式设置，推荐使用
```

> 如果有需要，绑定的内容可以进行 **变量**、**常量**、**算术运算**、**比较运算**、**逻辑运算**、**三元运算**等技术应用

通过v-bind对img标签的src、width、height属性进行绑定

```html
  <div id="app">
    <p>
      <img v-bind:src="mysrc" alt="" :width="wh" :height="ht" />
    </p>
  </div>
  <script src="./vue.js"></script>

  <script>
    var vm = new Vue({
      el:'#app',
      data:{
        mysrc:'./laofu.jpg',
        wh:280,
        ht:190
      }
    })
  </script>
```

####4.4.2属性绑定-class属性

> 使用 v-bind 对标签的class属性进行绑定

class属性较比其他属性不一样的地方是，其既可以接收一个值，也可以通过空格分隔接收多个值

```html
<tag class="apple"></tag>				   <!--接收一个值-->
<tag class="apple pear orange"></tag>		<!--接收多个值-->
```

> class属性绑定的语法:

```html
1) 对象方式
	<tag :class="{xx:true, xx:false}"></tag>
	<!--true: 设置   false:不设置-->

2) 数组方式
	<tag :class="['xx','yy','zz']"></tag>
	<!--数组元素值如果不是vue的data成员 就要通过单引号圈选，代表是普通字符串-->
```

```html
<style>
    .apple{color:blue;}
    .pear{font-size:25px;}
    .orange{background-color:hotpink;}
</style>

<div id="app">
    <h2>属性绑定</h2>
    <!-- <p class="apple pear orange">学习Vue课程</p> -->
    <!-- 通过vue方式给class绑定如上3个信息 -->
    <!-- 1. 对象方式 -->
    <p :class=" {apple:true, pear:true, orange:true, banana:false} ">学习Vue课程</p>
    <!-- 2. 数组方式 -->
    <p :class=" ['apple','pear','orange'] ">学习Vue课程</p>
</div>
```

#### 4.4.3属性绑定-style属性

> 使用v-bind指令操控style属性

style样式属性较比普通属性也比较特殊，其也可以接收多个值

```html
<p style="color:red; font-size:25px; background-color:lightgreen;"></p>
```

> style属性绑定语法：

```html
1) 对象方式
	<tag :style="{xx:yy,xx:yy.....}"></tag>
	<!--xx:样式名称，yy:样式的值-->
2) 数组方式
	<tag :style="[{xx:yy},{xx:yy.....}]"></tag>
	<!--根据需要，数组的每个元素都是一个对象，每个对象包含一对或多对css样式-->
```

```html
<p style="color:blue;font-size:25px;background-color:hotpink;">学习Vue课程-style绑定</p> 
```

```html
  <div id="app">
    <h2>属性绑定</h2>
    <!-- 通过vue实现给style绑定多个css样式信息 -->
    <!-- 1. 对象方式 -->
    <p :style=" {'color':'blue','fontSize':'25px','background-color':'hotpink'} ">学习Vue课程-style绑定</p>
    <!-- 2. 数组方式 -->
    <p :style=" [{'color':'blue','fontSize':'25px','background-color':'hotpink'}] ">学习Vue课程-style绑定</p>
    <p :style=" [{'color':'blue'},{'fontSize':'25px','background-color':'hotpink'}] ">学习Vue课程-style绑定</p>
    <p :style=" [{'color':'blue'},{'fontSize':'25px'},{'background-color':'hotpink'}] ">学习Vue课程-style绑定</p>
  </div>
```

1. 数组方式绑定style属性，每个数组元素可以包含**一个**或**多个**css样式对
2. 复合属性带中横线(例如background-color)的需要通过**单引号**圈选，或变为**驼峰**名称

> 通过传统方式也可以操作class或style属性，但是Vue的操控会更加**灵活** 和 **精准**，可以针对**某一个值**进行设置

###4.5 v-on(@)

####事件绑定-基本使用

使用v-on给标签绑定事件

web端网页应用程序开发，事件是一个不不可或缺的技术

> 在vue中给元素进行**事件**绑定，需要通过v-on:指令实现，也使用@符号，@是v-on:的简写，使用更方便

事件类型：

> 鼠标事件：onclick  ondblclick onmouseenter onmouseleave onmouseover onmousedown等等
>
> 键盘事件：onkeyup  onkeydown  onkeypress 等等

注意：

1. 事件处理驱动 需要通过methods定义
2. 被绑定的事件类型可以是 click、dblclick、keyup、keydown等等，**不要**设置on标志了

```html
<div id="app">
    <h2>事件操控</h2>
    <!--@是 v-on: 的简写，推荐使用，记住-->
    <button v-on:click="say()">说</button>
    <button @click="say()">说</button>
  </div>

  <script src="./vue.js"></script>
  <script>
    var vm = new Vue({
      el:'#app',
      data:{
      },
      // 给Vue实例 声明方法，该方法可以给事件使用
      methods:{
        say(){
          console.log('hello,北京')
        }
      }
    })
  </script>
```

####事件绑定-传递参数

vue“单击”事件参数的3种类型：

1. 有声明()，也有传递实参，形参就代表被传递的**实参**
2. 有声明(),但是没有传递实参，形参就是**undefined**
3. 没有声明()，第一个形参就是**事件对象**   [object MouseEvent/鼠标事件对象]

####事件绑定-访问data成员

根据业务需要，事件在执行过程中需要对Vue实例的data数据进行操作，通过**this关键字**实现

this代表Vue实例对象，并且针对data或methods成员都可以直接进行调用

####事件绑定-this是谁

在Vue实例内部包括不限于methods方法中，**this关键字** 是**Vue实例化对象**，具体与 **new Vue()** 是一样的

并且其可以对 **data** 和 **methods**成员进行直接访问

> 可以理解为this和vm是同一个对象的两个不同名字，this ===  vm 

> this指向:

1. this就是window对象

   ```js
   var age = 20
   function getInfo(){
     console.log(this)  // window
     console.log(this.age)
   }
   getInfo()  // 20
   ```

2. this代表调用该方法的当前对象

   ```js
   const tiger = {
     name:'东北虎', 
     act:'猛虎扑食', 
     say(){
       console.log('我的名字是'+this.name+'，我的招牌动作是'+this.act)
       // this代表tiger对象
     }
   }
   tiger.say()
   ```

3. this代表元素节点对象

   ```html
   <button onclick="this.style.color='red'" />确定</button>
   ```

注意：**this**在不同情况下代表不同对象，不用强记，通过console.log输出查看便知

####事件绑定-方法简易设置

根据es6标准，可以给methods各个成员方法做简易设置如下：

方法名称:function(){}     简易设置为：   方法名称(){}

###4.6 v-model

v-model，其被称为**双向数据绑定**指令，就是Vue实例对数据进行修改，页面会立即感知，相反页面对数据进行修改，Vue内部也会立即感知.

v-model是vue中 唯一实现双向数据绑定指令

> v-bind(单向)数据绑定，Vue实例修改数据，页面会感知到，相反页面修改数据Vue实例**不能**感知

> v-model(双向)数据绑定，页面修改数据，Vue实例会感知到，Vue实例修改数据，页面也会感知到

#### 基本使用

```html
<标签 v-model="data成员"></标签>
```

注意：

1. v-model只针对**value属性**可以绑定，因此经常用在form表单标签中，例如input(输入框、单选按钮、复选框)/select(下拉列表)/textarea(文本域)，相反div、p标签不能用
2. v-model只能绑定**data成员**，不能设置其他表达式，否则错误
3. v-model绑定的成员需提前在data中声明好

```html
 <div id="app">
    <p>{{ city }}</p>
    <p><input type="text" :value="city"></p>
    <p><input type="text" v-model="city"></p>
  </div>
  <script src="./vue.js"></script>

  <script>
    var vm = new Vue({
      el:'#app',
      data:{
        city:'北京'
      },
    })
  </script>
```

> v-model对应的city发生变化后，其他的{{ }} 和 :value的值也会发生变化

#### 4.6.2响应式

> v-model数据双向绑定步骤：

1. 页面初始加载，vue的data数据渲染给div容器
2. 通过v-model修改数据，修改的信息会直接反馈给vue内部的data数据
3. vue的data数据发生变化，页面上(也包括Vue实例本身)用到该数据的地方会重新编译渲染。
   * 2和3 步骤在条件满足情况下会**重复**执行

> 响应式：

vue实例的data数据如果发生变化，那么页面上(或Vue实例内部其他场合)用到该数据的地方会重新编译执行，这样就把更新后的内容显示出来了，这个过程就是“响应式”，即上面步骤3

* 如果Vue实例内部对变化的数据有使用，也会同步更新编译执行

注意：响应式 是Vue中非常重要的机制

#### v-model实现原理

给input输入框中定义oninput事件，在该事件中把用户输入的信息都给随时获得到，并对data成员进行赋值

data成员变化了，页面上用到数据的地方就重新渲染，达成简易双向绑定的效果

> oninput：是事件，可以随时感知输入框输入的信息

> $event:在vue的事件被绑定元素的行内部，代表事件对象

> event.target: 触发当前事件的元素节点dom对象

注意：

1. 事件声明没有小括号()，**第一个形参**就是 事件对象
2. 在元素行内事件驱动中可以直接使用**$event**,其也是事件对象

### 4.7v-for

> 使用v-for指令，遍历数组信息

```html
<标签 v-for="成员值 in 数组"></标签>
<标签 v-for="(成员值,下标) in 数组"></标签>
```

```html
<div id="app">
  <ul>
    <li v-for="item in color">{{item}}</li>
  </ul>
  <ul>
    <li v-for="(item,k) in color">{{k}}-----{{item}}</li>
  </ul>
</div>

<script src="./vue.js"></script>

<script>
  var vm = new Vue({
    el:'#app',
    data:{
      color:['red','yellow','pink']
    },
    methods:{
    }
  })
</script>
```

注意：使用v-for指令的html标签，由于遍历机制，本身标签会被**创建多份**出来

在vue中v-for做遍历应用时，都需要与:key一并进行使用

在2.2.0+版本里边，v-for使用的同时必须使用:key，以便vue能准确跟踪每个节点，从而重用和重新排序现有元素，你需要为每个数据项提供一个唯一的、代表当前项目的属性值赋予给key

```html
<tr v-for="(item,k) in brandsList" :key="item.id">
```

注意：

1. :key不设置，也是存在的，默认绑定每个项目下标序号信息
2. key是一个普通属性，前边设置**:冒号**，代表属性绑定

# vue第2天

## 1.vue指令

###1.1 v-if 和 v-show

在vue中，v-if 和 v-show 会根据接收  **true/false**  信息使得页面上元素达到显示或隐藏的效果

```html
<标签 v-if="true/false"></标签>

<标签 v-show="true/false"></标签>

<!--true:显示   false:隐藏-->
```

> 原理：

v-if：通过 **创建**、**销毁** 方式达到显示、隐藏效果的(销毁后有一个占位符<!---->)

v-show：其是通过css控制达成显示、隐藏效果的

> display:none;  隐藏
>
> display:block; 显示

> 特点：

v-if 有更高的**切换消耗** 、v-show有更高的**渲染消耗**

如果需要**频繁**切换 则v-show 较合适，如果运行条件不大可能改变 则v-if 较合适。

> 注意：

v-if使得元素被**隐藏**后，这个元素的物理位置有一个名称为"<!---->"的占位符，其与html的注释信息**没有关系**

简单案例：通过按钮控制，使得元素内容在 显示 和 隐藏 之间切换

```html
<style>
    #one{width: 300px;height: 40px;background-color:orange;}
    #two{width: 300px;height: 40px;background-color:lightgreen;}
  </style>
</head>
<body>
  <div id="app">
    <h2>v-if和v-show</h2>
    <button @click="flag=!flag">切换</button>
    <!--xxxxxxxxxxxx-->
    <p id="one" v-if="flag">学习vue第二天---v-if</p>
    <p id="two" v-show="flag">学习vue第二天---v-show</p>
  </div>
  <script src="./vue.js"></script>
  <script>
    var vm = new Vue({
      el:'#app',
      data:{
        flag:false // 控制标签是否显示true/false
      },
      methods:{
      }
     });
  </script>
```

> 注意：事件驱动不仅可以是**methods方法**，也可以是简单的**js语句**

### 1.2 v-if 和 v-else

在Vue中，v-if 、v-else-if 和 v-else 三个指令结合可以实现多路分支结构

- v-if可以**单独**使用，形成单路分支结构
- v-if  和 v-else 也可以合作使用，实现**双路**分支结构
- v-if  、v-else-if 和 v-else 也可以合作使用，实现**多路**分支结构

```html
<标签 v-if="true/false"></标签>

<标签 v-else-if="true/false"></标签>

<标签 v-else-if="true/false"></标签>

<标签 v-else></标签>
```

> 以上4个标签分支结构，最终只会走一个，第一个为true的那个标签会执行  或 执行v-else

`案例应用`：

判断品牌信息是否存在，并显示对应内容

```html
<table v-if="brandList.length>0">
  ……
</table>
<table v-else>
  <tr><td>没有任何记录！</td></tr>
</table>
```

注意：v-if和v-else一并使用，页面没有<!---->占位符了

## 2.品牌管理

###2.1品牌管理-删除

> 步骤：

1. 制作删除按钮和事件  @click="del(序号)"，把单元序号作为参数进行传递
2. 制作methods方法  del()，通过splice()方法对目标数组元素进行删除操作

>代码：

设置单击删除事件

```html
<tr v-for="(item,k) in brandsList" :key="item.id">
  <td><input type="checkbox"></td>
  <td>{{ item.id }}</td>
  <td>{{ item.name }}</td>
  <td>{{ item.ctime }}</td>
  <td><button @click="del(k)">删除</button></td>
</tr>
```

Vue的methods方法：

```js
   // 删除品牌
   // index:被删除品牌的下标信息
   del(index){
    if(!window.confirm('确定要删除该元素么？')){return false}
    // 数组.splice(下标,长度) 删除数组的元素
    // 该方法会使得目标数组直接发生变化
    // 该方法会把被删除的元素以数组方式给返回
    this.brandList.splice(index,1)
   },
```



# vue第3天

## 1.生命周期

> 生命周期是指vue实例(或者组件)从诞生到消亡所经历的各个阶段的总和

生命周期分为3个阶段，分别是[创建]()、[运行]()、[销毁]()

- 创建阶段：由空白期、data/methods初始化、模板挂载、模板渲染等组成
- 运行阶段：分为 更新前 和 更新后 两部分
- 销毁阶段：分为 销毁前 和 销毁后

> 成员方法：

各个阶段在Vue实例内部都有对应的成员方法，可以定义、执行、感知

​	创建：beforeCreate    **created**   beforeMount   mounted

​	运行：beforeUpdate  updated

​	销毁:  beforeDestroy    destroyed

不同阶段完成不同的任务，开发者可以利用各个阶段的特点完成业务需要的相关功能

### 1.1创建阶段

创建阶段一共有4个方法，它们与 el、data都是并列关系的，重点记住created方法

```js
new Vue({
  beforeCreate(){   },
    
  created(){  },
  
  beforeMount(){   },
    
  mounted(){  },
})
```

> beforeCreate：此时Vue对象刚创建好，没有任何成员，data、methods等都没有，只有this
>
> **created**：此时vue对象已经长大一点，内部已经完成了data、methods等成员的设置，也是data初始化的最好时机
>
> beforeMount：此时vue实例已经把div容器给获得到了，但是内部的vue指令等信息还没有被编译处理
>
> mounted：此时，vue获取到的div容器内部的原生指令已经被编译处理好了，并且也完成了容器的渲染工作，此时模板中已经看不到vue原始指令了



> 重点关注是 created ：

created: 一般用于页面"首屏"数据的获取操作(获取好的数据可以直接赋予给data使用，此方法已经把data做好了，其可以做到**第1 时间**就把数据赋予给data，供后续使用)



> 注意：创建阶段各个方法不设置则以，设置后就会**自动**执行，并且会**顺序**只执行**一次**

### 1.2运行和销毁阶段

> 运行阶段：

```js
new Vue({
	beforeUpdate(){ 可以感知到data数据变化之前页面上关于该数据的样子 }
    
	updated(){ 可以感知到data数据变化之后页面上该数据的样子 }
})
```

> 运行阶段方法**不会**自动执行，当data成员数据发生变化，才会执行，并且数据变化多次，方法也会**重复**执行多次



> 销毁阶段：

```js
new Vue({
	beforeDestroy(){ vue实例销毁之前 }
    
	destroyed(){ vue实例销毁之后 }
})
```

> 当vue实例被销毁后，就要执行以上两个方法，vm.$destroy()



完整应用示例：

```html
<body>
  <!--创建一个div容器，vue对该容器进行控制，设置要显示的内容-->
  <div id="app">
    <h2>{{ msg }}</h2>
  </div>
  
  <script src="./vue.js"></script>
  <script>
    var vm = new Vue({
      // 1) 生命周期创建阶段(4个函数),会自动执行
      beforeCreate(){
        // Vue实例已经创建完毕，但是相关的成员都没有，el、methods、data等等都没有
        console.group('--------beforeCreate发生调用--------')
        console.log('%c%s','color:red','el现在的样子：'+this.$el)     // undefined
        console.log('%c%s','color:red','data现在的样子：'+this.$data) // undefined
        console.log('%c%s','color:red','getDate现在的样子：'+this.getDate)  // undefined
      },
      created(){
        // 该阶段是一个【重要】阶段，此时data 和 methods已经准备好了，但是还没有去找div容器
        // 此阶段可以用于页面首屏数据获取操作，获取回来的数据存储给data的某个成员即可
        console.group('--------created发生调用--------')
        console.log('%c%s','color:red','el现在的样子：'+this.$el)      // undefined
        console.log('%c%s','color:red','data现在的样子：'+this.$data)  // 实体
        console.log('%c%s','color:red','getDate现在的样子：'+this.getDate)  // 实体
      },
      beforeMount(){
        // 此阶段完成了Vue实例对象 与 div容器联系的过程(本质是div容器已经被Vue实例获取到了)
        // 但是div容器的内容还是没有编译前的原生内容
        console.group('--------beforeMount发生调用--------')
        console.log('%c%s','color:red','el现在的样子：'+this.$el)      // 实体
        console.log(document.getElementsByTagName('h2')[0])  // 
      },
      mounted(){
        // 此阶段 Vue实例已经完成了div容器的内容的编译，并且编译好的内容也渲染给div容器了
        console.group('--------mounted发生调用--------')
        console.log('%c%s','color:red','el现在的样子：'+this.$el)      // 实体
        console.log(document.getElementsByTagName('h2')[0])  // 容器编译【后】实体内容
      },

      // 2) 生命周期运行阶段(2个函数),data数据变化后才会执行
      beforeUpdate() {
        console.group('---------beforeUpdate调用--------')
        console.log(
            '%c%s',
            'color:red',
            'h2数据更新【前】的效果：' + document.querySelector('h2').innerHTML
        )
      },
      updated() {
        console.group('---------updated调用--------')
        console.log(
          '%c%s',
          'color:red',
          'h2数据更新【后】的效果：' + document.querySelector('h2').innerHTML
        )
      },
      
      // 3) 生命周期销毁阶段(2个函数),只有vm调用$destroy()方法后才执行
      beforeDestroy() {
        console.group('---------beforeDestroy调用--------')
        console.log('%c%s', 'color:red', 'el现在的样子：' + this.$el)
      },
      destroyed() {
        console.group('---------destroyed调用--------')
        console.log('%c%s', 'color:red', 'el现在的样子：' + this.$el)
      },
      
      el: '#app',
      data: {
        msg: '生命周期学习篇'
      },
      methods: {
        getDate(){
          console.log('Sunday')
        }
      }
    })
  </script>
</body>
```

`注意`：

生命周期的各个方法与 el、data、methods 等成员都是并列的，它们有固定的执行顺序，与设置顺序没有关系

## 2.VirtualDOM

> VirtualDOM：div容器在Vue实例中存在的状态，就是 VirtualDOM(虚拟dom内容)，具体是**内存信息**的体现

Vue实例运行期间，该VirtualDOM始终存在



> VirtualDOM作用：

1. 编译解析div容器，并渲染给浏览器
2. 响应式体现

## 3.Promise

> Promise:是一个对象，是用来处理**异步**操作的，可以让我们写异步调用的代码更加优雅、美观、有利于阅读。



> 相关异步操作：

1. axios(ajax)
2. setTimeout     定时器
3. fs.readFile()     文件读取



> Promise的三种状态：

1. pending（进行中）
2. resolved（完成）
3. rejected（失败） 



> 异步：在同一个时间中，可以发送**多个**进程进行执行
>
> 同步：在同一个时间点，只有**一个**进程在执行



> Promise的作用：

1. 解决了异步调用彼此嵌套的**回调地狱**问题
2. 解决了多个异步过程**顺序执行**问题



### 3.1Promise的使用方法

```js
// 1. 创建Promise对象
var p = new Promise(function(resolve,reject){
  if(异步操作成功){
  	resolve(res)
  }else{
    reject(cuo)
  }
})

// 2. 对Promise对象结果进行处理
p
  .then(
  	function(data){
    	// data 与 res一致，代表成功输出结果
  	}
	)
  .catch(
  	function(err){
      // err 与 cuo一致，代表失败输出结果
    }
	)
```

> resolve: 异步操作成功的回调函数
>
> reject：异步操作失败的回调函数

> 以后遇到Promise对象，就调用then、catch方法即可

