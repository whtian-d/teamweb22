# ES6 介绍

- [ECMAScript](https://baike.baidu.com/item/ECMAScript/1889420) 6，简称ES6 ,目标是使JavaScript语言可以用来编写复杂的大型应用程序，成为企业级开发语言。
- ES6与javascript的关系：ECMAScript是一种语言标准，Javascript实现了这个标准。
- ES6 与 ECMAScript2015的关系
  - ECMAScript2015 是具体到2015年6月发布的那一版。
  - **ES6有两层含义**
    - 特指ECMAScript2015
    - 泛指ES2015及之后的新增特性，虽然之后的版本应当称为ES2018，ES2019...但可统称为ES6。

> 学习内容

ES6新增了很多强大的语法，如下是比较常使用的：

1. let 和 const
2. 解构赋值
3. 函数扩展
4. 字符串扩展
5. 数组扩展
6. 对象的简写

> 学习参考

1. 各种环境中对es6的支持程度： <http://kangax.github.io/compat-table/es6/>
2. ES6电子书： <http://es6.ruanyifeng.com/#docs/intro>

# let 变量

> let作用：定义变量。（var也是用来定义变量）

> 我们之前定义变量的关键字是`var`，它定义的变量有很多奇怪的特点，如下有两点比较突出：

- 变量先使用再定义------ 变量提升。

  ```js
  console.log(a);  //undefined
  var a = 1;
  console.log(a)   //1
  ```

- 缺少块级作用域。

  ```js
  // 此处为了使用循环，定义一个循环变量i。
  for(var i=1; i<10;i++){}
  // i在循环体之外也能使用。
  console.info(i);   //10
  ```

这两点都容易让初学者混淆，也容易让从其它语言转过来的程序员混淆。为了解决这些问题，ES6中新增了let。

## let基本使用

格式： let 变量名 = 变量值；

它用来定义变量，基本使用格式与var关键字一样。在可以在使用var 的地方改成let。

## 与var的区别

- 不能重复定义

  ```js
  // let不能进行重复定义
      let num = 100;
      console.log(num);   //100
  
      let num = 300;   // 报错Uncaught SyntaxError: Identifier 'num' has already been declared
      console.log(num); 
  ```

- 没有变量提升（var定义的变量是有变量提升的），必须先定义再使用

  ```js
  // let不会进行变量提升
  console.log(num); // 报错 Uncaught ReferenceError: Cannot access 'num' before initialization
  let num = 100; 
  ```

- 全局变量不会附加到window对象的属性中

  ```js
  //let声明的变量不会成为window的成员
      let num = 100;
      console.log(num,window.num);  //100 undefined
  ```

- 具有块级作用域

  ```js
   // let声明的变量具有块作用域
   // 所有的代码块都具有作用域
   // 注意：对象字面量{}不是代码块！
  
       if (true) {
        let num = 100;
      }
      console.log(num);      // 报错，num is not defined
  
        for (let i = 0; i < 10; i++) {
         console.log(i);
       }
       console.log(i, 'for执行之后，外面书写的i的访问');   // 报错： i is not defined
  
      // ES6提供了一种单独的块作用域书写形式
      {
         let num1 = 100, num2 = 200;
         console.log(num1 + num2);
       }
       console.log(num1, num2); // num1 is not defined
  
       (function () {
           var num = 100;
         })();
  ```

## 点击li，输出索引值 

```js
<ul>
    <li>这是li</li>
    <li>这是li</li>
    <li>这是li</li>
    <li>这是li</li>
</ul>

  <script>
    // 需求：点击li，输出索引值
    var lis = document.getElementsByTagName('li');
    for (let i = 0; i < lis.length; i++) {
      // lis[i].setAttribute('data-index', i);
      // lis[i].dataset.index = i;
      // lis[i].index = i;
      lis[i].onclick = function () {
        // 输出索引值
        console.log(i);
        // console.log(this.getAttribute('data-index'));
        // console.log(this.dataset.index);
        // console.log(this.index);
      };
    }

    console.log(i);
  </script>
```

# const 常量

> ES6引入const的原因是，因为ES5中并没有提供`常量`的功能。

> 使用场景

程序员在协同开发项目时，会遇到一种场景：有一些数据大家都需要用到，但是都不能修改，即数据是只读的。

举个例子：在开发公司的网站时，公司的基本信息：地址，公司名，电话等等信息可以在多个地方都需要使用，但不允许去修改。 显然，使用变量来保存这些信息是不适合的，因为变量不是只读的。这种情况下， 我们就可以把这些数据保存在常量中。

> 语法格式及命名规范

作用：定义一个只读的常量。

格式： const  常量名 = 常量值;

示例：var COMPANY_NAME = "XXX公司"

注意：区别于变量名，常量名**推荐采用全大写**的方式，多个单词之间**使用_下划线分隔**。

##const特点

所谓常量，就是不能修改，即：

- 一旦定义就不能修改,不能进行重新赋值 ；

  ```js
  const num = 100;
  console.log(num);  //100
  
  num = 300;      // Uncaught TypeError: Assignment to constant variable.
  ```

- 一旦声明，就必须立即初始化；

```javascript
// 2 声明常量时必须设置初始值
const num;        // Uncaught SyntaxError: Missing initializer in const declaration
```

其它与let相似的特点

- 具有块级作用域
- 不能重复声明 
- 没有变量提升，必须先定义再使用,声明之前不能访问 
- 常量也是独立的，定义后不会添加为window对象的属性

##const本质

> 基本数据类型在内存单元中保存的是具体值(值本身)
>
> 复杂数据类型在内存单元中保存的是地址

const实际上保证的，并不是变量的值不得改动，而是变量指向的那个内存单元中保存的数据不得改动

```js
// 1 保存了基本类型的常量完全不能修改
    const NUM = 100;
    console.log(NUM);
    NUM = 2;      //Uncaught TypeError: Assignment to constant variable.

// 2 保存了复杂类型的常量不能重新赋值为其他值，但是内部属性可以修改
     const obj = {
      name: 'jack',
      age: 18
    };
    obj = 3;           // 不能直接修改obj中保存的数据

    obj.name = 'rose';     //内部属性可以修改
    console.log(obj);  
```

- 对于简单类型数据（数值、字符串、布尔值），值就保存在变量指向的那个内存单元，因此等同于常量值。

- 对于复杂类型数据（如对象和数组），变量指向的内存单元，保存的只是一个指向实际数据的指针，const只能保证这个指针是固定的（即总是指向另一个固定的地址），至于它指向的数据结构是不是可变的，就不能控制了。因此，将一个对象声明为常量必须非常小心,它的属性是可以修改的。

  <img src="images/const数据保存.png"/>

**定义一个不能修改的对象**（属性不能添加，修改，删除），可以使用Object.freeze()。

```javascript
//冻结操作：可以让某个对象的属性无法修改
// 如果希望某个对象完全无法修改，可以使用const+冻结操作
// 注意：冻结只是对象的属性无法修改，属性的属性还是可以修改
// 需要通过递归来对某个对象进行冻结操作即可
// 封装用于深冻结的函数：
        function deepFreeze(obj) {
            // 1 先通过Object.freeze()对对象的属性进行冻结
            Object.freeze(obj);

            // 2 遍历obj获取所有属性
            for (var k in obj) {
                // 3 检测当前属性值是否为复杂类型
                if (typeof obj[k] === 'object' && obj[k] !== null) {
                    // console.log(k + '是复杂类型值');
                    // 4 进行递归调用
                    deepFreeze(obj[k]);
                }
            }
        }

// 声明要冻结的对象
const obj = {
  name: 'jack',
  age: 18,
  hobbies: {
    eat: '吃',
    drink: '喝',
    run: '跑步',
    playBall: ['篮球', '弹球', '悠悠球']
  }
};

// 调用函数冻结对象obj
deepFreeze(obj);
obj.name = 'rose';
obj.hobbies.eat = '各种吃';
obj.hobbies.playBall[2] = '各种弹';
console.log(obj); // obj没有变化，说明冻结完成
```

## let和const小结

| 关键字 | 变量提升 | 块级作用域 | 是否必设初始值 | 是否可更改 | 是否是顶级对象属性 |
| :----: | :------: | :--------: | :------------: | :--------: | :----------------: |
|  let   |    ×     |     √      |       -        |    Yes     |         No         |
| const  |    ×     |     √      |      Yes       |     No     |         No         |
|  var   |    √     |     ×      |       -        |    Yes     |        Yes         |

# 解构赋值

```js
// 为什么需要解构赋值呢？
var arr = [98, 87, 86, 78];
// 如果希望多次使用数组中的某个元素，可以声明变量保存，但是书写较为繁琐。
var a = arr[1];
var b = arr[2]
console.log(a,b); 
```

解构赋值可以让数组的取值和变量的声明操作简化 

ES6提供了一个更加方便的方式从对象中取出属性值来，这就是解构赋值。

> ES6 允许按照一定**模式**，从数组和对象中提取值，对变量进行赋值，这被称为解构（Destructuring）。
>
> 它有两个动作：

```
解构：意思是把有结构的数据分解开成为一个一个的值
赋值：把解构之后的值保存到变量
```

##解构赋值的基本使用

```js
let [变量1=默认值1, 变量2=默认值2, 变量n=默认值n] = [数组元素1, 数组元素2, 数组元素n];
```

> 注：默认值是可选的，可以设置，也可以不设置；

规则：

- 赋值符号左右两边都是数组，把右边的数组按下标从小到大取出来，放入左边的数组中。
- 如果左边的变量并没有分配到某一个值：
  - 有默认值，使用其默认值。
  - 无默认值，其值是undefined
- 最开始的let可选，也可写成var或省略，与解构赋值功能无关，仅代表变量的声明方式。

##数组的解构赋值

它能够快速从数组中取出值保存到变量中。它的本质是给变量赋值。

```js
// 1.左右的结构需要对应，左侧表示要声明的变量，赋值给右侧对应的元素值
//常规使用:变量个数等于数组长值
var arr = [98, 87, 86, 78];
var [a, b, c, d] = arr;

console.log(a, b, c, d);    //98, 87, 86, 78
// 2 左右数据个数不对应
    var arr = [98, 87, 86, 78];
    var [a, b] = arr;        //变量个数小于数组长度
    console.log(a, b);   //98, 87

    var arr3 = [98, 87, 86, 78];
    var [a, b, c, d, e, f] = arr3;    //变量个数大于数组长度
    console.log(a, b, c, d, e, f);    //98 87 86 78 undefined undefined

// 3 通过跳项，跳过某个元素取值
    var arr = [98, 87, 86, 78];
    var [a, , , c] = arr;      //用空跳过不需要的值
    console.log(a, c);     // 98 78 

// 4 解构赋值的默认值
    //设置默认值后，如果可以取到值，就使用取到的值，
    // 如果没有取到值，使用默认值
    var arr = [98, 87, 86, 78];
    var [a, b = 1000, c, d, e, f = 200, g] = arr;
    console.log(a, b, c, d, e, f, g);    //98 87 86 78 undefined 200 undefined

// 5 剩余值
    //在解构左侧的最后一个名称前设置...，表示获取剩余值
    //指的是将剩下的数据保存在一个新数组中
    //如果剩余值功能不在最后使用，会报错  
    //Uncaught SyntaxError: Rest element must be last element
    //                      rest element 剩余值元素
    var arr = [1, 5, 4, 6, 8, 2, 3];
    // let [a, b, ...c, d] = arr; // 报错写法
    var [a, b, ...c] = arr;    //... 只能用在最后一个变量上。这个变量一定是一个数组
    console.log(a, b, c);   //1 5 (5) [4, 6, 8, 2, 3]
    
    var arr = [1, 2, 3, 4];
    let [, , a] = arr;
    console.log(a);   //3

    var arr = [1, 2, [3, 4, [5, 6, 7]]];
    let [, a, [, b, [, c]]] = arr;      //复杂嵌套场景
    console.log(a, b, c);    //2   4   6
```

##解构赋值的面试题

如何交换两个变量的值？

```javascript
let a = 1, b = 2;
// 写代码,实现互换a,b的值
 
[a, b] = [b, a];

console.log(a,b); // 要求输出 2, 1
```

## 对象的解构赋值

> 作用：快速从对象中获取值保存到变量中。它的本质是给变量赋值。

```javascript
let {"属性名1"：变量名1=默认值1, "属性名2"：变量名2=默认值2,... } = {"属性名1"：属性值1,"属性名2"：属性值2,...}
```

解析规则：

- 默认值是可选的。你可以指定默认值，也可以不指定。
- 右边的"属性名"与左边的“属性名” 一致，则把右边的属性值赋值给左边的变量名。
- 如果右边的匹配不成立，看看是否有使用默认值，有默认值就使用默认值，没有就是undefined。

> 如果左侧对象中属性名与变量名相同，则可左侧合并：

```javascript
let {变量名1=默认值1，变量名2=默认值2} = {"属性名1"：属性值1,"属性名2"：属性值2,...}
```

解析规则：右边的"属性名"与左边的变量名 一致，则把右边的属性值赋值给左边的变量名。

> 基本使用

```js
    // 1.基本使用
    // 对象是无序的存储方式，进行解构时，默认按照属性名进行取值
    // 注意：进行解构时，只要属性名称对应即可，顺序无所谓

    var obj = {
      username: 'jack',
      age: 18,
      password: '123456'
    };
    var { username, password, age } = obj;
    console.log(username, age, password);     //jack 18 123456

    // 2 个数不对应
    // 无需使用逗号进行分割，直接书写要获取的属性名即可
    var obj = {
      username: 'jack',
      age: 18,
      password: '123456',
      gender: '男'
    };
    var { gender, age } = obj;
    console.log(gender, age);    //男 18
    var { school, username, gf } = obj;
    console.log(school, username, gf);  //undefined "jack" undefined
 
    // 3 属性别名
    // 一定注意，冒号后面的名称才是变量名称
    var obj = {
      username: 'jack',
      age: 18,
      password: '123456',
      gender: '男'
    };

    let { username: uName, age, password: uPsw } = obj;
    // 此时username与password只是属性查找方式，不是变量名
    console.log(username, password);    //username is not defined
    // 需要使用:后的值进行变量访问
    console.log(uName, uPsw, age);    //jack 123456 18

    // 4 默认值
    var obj = {
      username: 'jack',
      age: 18,
      password: '123456',
      gender: '男'
    };
    let { gf = 'rose', age = 200, school, username } = obj;
    console.log(gf, age, school, username);    //rose 18 undefined jack

    // 4.1 属性名设置别名和默认值的写法
    // 注意顺序，先写别名，再写默认值
    var obj = {
       // username: 'jack',
       age: 18,
       password: '123456',
       gender: '男'
     };
     let { username: uName = 'admin' } = obj;
     console.log(uName);    //admin

    // 5 剩余值
    //  对象解构赋值的剩余值结果为对象结构，同样必须设置在最后位置，否则报错
    var obj = {
      username: 'jack',
      age: 18,
      password: '123456',
      gender: '男'
    };
    let { username: uName, ...other } = obj;
    console.log(uName, other);    //jack {age: 18, password: "123456", gender: "男"}   
```

```js
// 复杂的嵌套，只要符合模式，即可解构
 var obj = {
      username: 'jack',
      age: 18,
      gf: {
        school: '黑马1',
        class: '92期'
      },
      bf: {
        school: '黑马2',
        class: '92期'
      },
      gender: '男'
    };

// 写法1：只获取gf内的属性，gf没有获取
    let { age, gf: { school } } = obj;

    console.log(age, school);   //18 "黑马1"
    console.log(gf); // 报错  gf is not defined

// 写法2：获取gf属性，同时也获取gf本身
    let { age, gf: { school }, gf } = obj;
    console.log(age, school);  18 "黑马1"

    console.log(gf); // 可以取值    {school: "黑马1", class: "92期"}
```

```js
// 假设从服务器上获取的数据如下
let response = {
    data: ['a', 'b', 'c'],
    meta: {
        code: 200,
        msg: '获取数据成功'
    }
}
// 如何获取到 code 和 msg
let { meta: { code, msg } } = response;
console.log(code, msg); // 200 '获取数据成功'
```

# 对象的简写方式

> ES6将对象的写法进行了简化，分为属性和方法两种简化形式 

> 1 属性简写

```js
// 前提条件，已经与属性同名的变量，保存了属性值
    var name = 'jack';
    var age = 18;

    var obj = {
      name, // 相当于 name:name,
      age
    };
    console.log(obj);  //age:18,name:"jack"

// 下面是示例：
    var username = $('#ipt').val().trim();
    var password = $('#ipt2').val().trim();
    $.ajax({
      url: '...',
      data: {
        username,
        password
      },
      success: function (res) {

      }
    }) 
```

> 2 方法简写

```js
var obj = {
      name: 'rose',
      age: 18,
      // sayHi是传统写法
      sayHi: function () {
        console.log('你好，我叫' + this.name);
      },
      // sayHehe是ES6的简写形式，功能没区别
      sayHehe() {
        console.log('呵呵，我叫' + this.name)
      }
    };

    obj.sayHi();
    obj.sayHehe();
```

#逻辑运算符回顾

>逻辑运算符的短路运算（逻辑中断操作）
>&&      ||       !

```js
//逻辑运算符使用的两种场景
//1 操作数均为布尔值（基本规则）
//2 某个操作数为非布尔值（&& || 规则相同）
    // 从左往右查看操作数
    // 当操作数为非布尔值时，隐式转换
    // 哪个操作数可以决定式子结果，就返回这个操作数(原值)

    console.log(3 && 'abc'); // 'abc'
    console.log(0 && true); // 0
    console.log(undefined || 200); // 200
    console.log('xyz' || 123); // 'xyz' 
```

# 函数的拓展

## 参数默认值

在定义一个函数时，我们可以给形参设置默认值：当用户不传入对应实参时，我们有一个保底的值可以使用。这个特性在ES6之前，是不支持的，我们以前会通过一些变通的方式来实现。

### 传统的默认值设置方式

参数的默认值在之前的课程内容已经涉及，例如在`xhr.open(请求类型,请求地址,是否异步) `方法中，第3个参数默认是true，即表示异步ajax。

- 默认值的意思是：
  - 如果传入对应实参，就用你传的值。
  - 如果不传，就使用某个特殊的、事先定义好的值。这个值也就是默认值。
- 示例代码：（以ajax课程中的ajax函数封装为示例）

```js
// ES5 中给参数设置默认值的变通做法，以ajax函数部分封装为示例：
function ajax (type, url, isAsync) {
	// 基本写法：  
  if(isAsync === undefined){
      isAsync = true;
  }
  // 简化写法：
	// isAsync = isAsync || true;
  
  console.log(type, url, isAsync);
	//.. 其他代码略
}
// 下面这两句是等价的
open("get","common/get"); // 参数3使用默认值true
open("get","common/get",true);

open("get","common/get",false);
```

以上代码是利用了形参的一个特点：没有传入对应实参的话，其默认值是undefined。

观察后发现，代码是可以工作的，但是显得很累赘，es6提供了更简单的实现。

### ES6的实现

格式

```
function 函数名 (参数名1=默认值1，参数名2=默认值2，参数名3=默认值3){
    // 函数体
}
```

示例

```js
function open(type, url, isAsync = true) {
    console.log(type, url, isAsync);
}
// 下面这两句是等价的
open("get","common/get")；// // 参数3使用默认值true
open("get","common/get",true);

open("get","common/get",false); 
```

思考与回忆：

- 能否跳过isAsync,url，而只给type设置默认值？

注意:

- 带默认值的形参放在形参列表的最右边。

### 练习

```javascript
function f(a = 1,b = 2){
	console.log(a, b);
}
f(10);
f(10,20);
f();

function f2(a = 1,b){
	console.log(a, b);
}
f2(10);
f2(10,20);
f2(,3); // 报错：Uncaught SyntaxError: Unexpected token
f2(); 

// 与解析赋值一起使用:
function f1({a = 1, b = 2} = {}){
   console.log(a, b);
}	

f1({a:10,b:20});
f1({a:20});
f1({c:1});
f1(); // 注意：如果形参位置不设置 = {}，会出现报错
```



## rest 参数

rest （其它的，剩余的）参数 用于获取函数多余参数，把它们放在一个数组中。

语法格式

> rest参数不能设置默认值，且必须设置在参数列表最后位置

在定义函数时，在最后一个参数前面加上`...`， 则这个参数就是剩余参数；

```javascript
let fn = function(参数1，参数2，...rest参数){}

let fn = (参数1，参数2，...rest参数) => { }; // 箭头函数具体使用，见下一小节。
```

只是在定义函数时，在形参列表中区别一下，而在调用函数时并无区别。

示例

回答如下问题

```javascript
function f2 (x,...y){
    console.log(x,y)
}
f2(1,2);
f2(2,3,4);

function f1 (x,y){
    console.log(x,y)
}
f1(1,2);
f1(2,3,4);
```

### 应用--代替arguments

问题：编写一个函数，求所有参数之和；

方法一：arguments

方法二：rest参数

```javascript
function getSum (){
    //  在这里写你的代码
    var sum = 0 ; 
    for(var i = 0; i < arguments.length; i++){
        console.info( arguemnts[i])
        sum += arguments[i];
    }
}
```

如果以箭头函数 的方式去定义这个函数，则内部不可以使用arguments这个对象了。此时，我们就可以使用

rest 参数，它可以替代 arguments 的使用。 代码如下：

```js
// 参数很多，不确定多少个，可以使用剩余参数
const  getSum = (...values) => {
    var sum = 0 ; 
    for(var i = 0; i < values.length; i++){
        console.info( values[i])
        sum += values[i];
    }
}
// 调用
console.log(fn(6, 1, 100, 9, 10));
```

与arguments相比，它是一个真正的数组，可以使用全部的数组的方法。

#箭头函数

> 箭头函数能让代码更简洁，效率更高；能看懂别人写的代码 ；

```javascript
let fn3 = x => x * 2;    //let fn3=(x)=>{x*2}
```

> 箭头函数本质上是 **匿名函数**的简化写法

```js
let 函数名 = (形参1，...形参n) => {
    // 函数体
};
```

前面学习的定义一个函数有两种方式:

1. 函数声明式

   ```js
   // 1. 函数声明式
   function fu1(x){
       return x * 2;
   }
   ```

2. 函数表达式

   ```js
   // 2. 函数表达式
   let fn2 = function (x) {
       return x * 2;
   };
   ```

ES6 中允许使用箭头函数的方式来定义一个函数:

   3. 箭头函数

```js
// 3. 箭头函数 (赋值给变量，作为函数表达式使用)
let fn3 = (x) => {
    return x * 2;
};
```

>对比前两种写法会发现，箭头函数的写法要比传统匿名函数简洁。

##箭头函数小结

1. 去除function关键字
2. 在形参和函数体之间设置 =>

注意：

```
=>是一个整体，不要加空格
箭头函数只在书写格式上有些区别，但在函数调用方式上，是没有区别的。
```

##箭头函数简化写法

- 当形参有且只有一个，可以省略小括号

  ```js
  let f = (x) => {console.log(x)}
  // 可以简化成：
  let f = x => {console.log(x)}
  ```

- 当函数体只有一条语句，可以省略大括号; 

  ```js
  let f = x => {console.log(x);}
  // 可以简化成：
  let f = x => console.log(x);
  ```

- 当函数体只有一条语句，并且就是return语句，则可以省略return和大括号。

  - 如果省略了大括号，则必须省略return，否则报错

  ```js
  let f = x => {return x*2; }
  // 可以简化成：
  let f = x => x*2;
  ```

- 注意如果返回值是一个对象，要加()

  ```js
  let f = x => { return {a:1};  }
  // 可以简化成：
  let f = x => {a:1}; // 如果不加，{}会被认为是函数的代码块，不会被解析器当成对象处理
  let f = x => ({a:1});
  ```

##箭头函数与普通函数的区别

- 内部没有this
- 内部没有arguments（了解）
- 不能作为构造器（了解）

###内部的`this`对象，指向定义时所在的对象，而不是使用时所在的对象。

```js
// 箭头函数中this的问题：
let obj = {
  name: 'jack',
  age: 18,
  sayHi() {
    // 方法中直接访问this：
    console.log(this); // 对象obj

    // 普通调用的函数中的this：
    var f1 = () => {
      console.log(this); // 对象obj
    };
    f1();

    // 同上：
    setTimeout(() => {
      console.log(this); // 对象obj
    }, 0);

    // 另一个对象的方法中的this
    let obj2 = { name: 'rose' };
    obj2.sayHehe = () => {
      console.log(this); // 对象obj
    };
    obj2.sayHaha = function () {
      console.log(this); // 对象obj2，因为没有使用箭头函数
    };
    obj2.sayHehe();
    obj2.sayHaha();

  }
};
obj.sayHi();
```

###没有 arguments

- 因为es6中提供了函数的rest剩余值功能，可以替代arguments

```js
let fn = (a,b) => {
    console.log(arguments); // 报错，arguments is not defined
};
fn(1, 2);
```

###箭头函数不能作为构造函数

```js
let Person = () => {
	// ..代码
};
let obj = new Person(); // 报错，Person is not a constructor
// 换个角度理解，箭头函数中都没有自己的this，无法处理成员，所以不能当构造函数
```

在javascript中，函数的功能太多了，除了起到最基本的封装代码之外，还可以当做构造器来使用。ES6中提出的箭头函数让函数减负了，只适合代码的封装操作。



# 数组的扩展

数组对象是js中非常重要的对象，它本身提供了非常多的方法，例如：push，pop，shift，unshift，splice，concat，sort，indexOf，join，map，forEach，filter，every，some，reduce... 。由于前端的主要工作内容之一是与后端进行数据交互，而数据交互的载体大多是数组和对象，所以我们对数组的操作要求也非常高。

曾经有一道面试题：写出10个你用过的与数组相关的方法。

这一小节的学习会让我们多掌握几个数组的方法。

## 扩展运算符

功能：它的作用是把数组中的元素一项项地展开：把一个整体的数组拆开成单个的元素。

格式：`...数组`

基本用法

```javascript
console.log(...[1,2,3]);
```

应用1：数组拷贝

```js
 //数组拷贝
    let arr1 = [1, 2, 3, 4];
    let arr2 = arr1; 
    console.log(arr2);   //[1,2,3,4]
    arr2.push(5)
    console.log(arr1);   //[1,2,3,4,5]
    console.log(arr2);   //[1,2,3,4,5]
    // arr1和arr2指向的内存空间是一致的，只要一个修改，另一个也会同时改变
    
    let arr1 = [1, 2, 3, 4];
    let arr2 = [...arr1];     //赋值给arr2的是arr1的值，而不是数组
    console.log(arr2);    //[1,2,3,4]
    arr2.push(5);
    console.log(arr1);   //[1,2,3,4]
    console.log(arr2);   //[1,2,3,4,5]
```

应用2： 数组合并

从把一个数组中的值全取出来，放在另一个数组中的

```javascript
var arr0 = ['a', 'b'];
var arr1 = [1, 2, 3];
var arr2 = [...arr1];
var arr3 = [...arr0, ...arr1];
```

应用3：Math.max()

```javascript
Math.max(1,3,4,6);
var arr = [1,3,4,6];
Math.max(...arr);
// 或者 Math.max.apply(this, [1, 2, 3, 566]);
```

## Array.from()

功能：把其它伪数组的对象转成数组。

格式： `数组 = Array.from(伪数组对象)`

它的实参有三种情况：

1. 自定义的，类似数组格式的对象。

```js
let fakeArr = {
  0: 'a',
  1: 'b',
  2: 'c',
  length: 3
};
```

就是为了演示，并无实际应用价值。

1. arguments对象
2. DOM 操作返回的 NodeList 集合

## find方法

在实际的开发中，我们经常会遇到一种场景：从一个数组中找出符合条件的元素。我们要讨论的重点是如何从数组中找出符合条件的元素，当然，我们可以通过手写循环的方式来实现这个功能，但是现在es6中提供了现成的功能。find/findIndex

> 作用：从数组中找出我们符合条件的第一个元素（或者是下标）。

find和findIndex的格式是一致的。

```javascript
let result = [].find(function(item,index,self){ 
    //...
    // 如果满足查找的条件
    return true;
});
```

- 回调函数有三个参数，分别表示：数组元素的值、索引及整个数组
- 如果某次循环返回的是true，find和findIndex方法的返回值就是满足这个条件的第一个元素或索引

> 执行流程

- find和findIndex方法，会遍历传递进来的数组
- 如果在回调函数体内，某个时刻return true，则表示查找过程结果，返回值就是本轮循环中的元素（或者是下标）；如果全部的循环结束，也没有return true，则表示没有找到，没有找到会返回undefined。
- **findIndex** 找到数组中**第一个满足条件**的成员并**返回该成员的索引**，如果找不到返回 **-1**。

```js
let arr = [1, 2, 4, 0, -4, 3, -2, 9];
arr.find(function (item, index, self) {
    console.log(item); // 数组中的每个值
    console.log(index); // 数组中的每个索引/下标
    console.log(self); // 当前的数组
});
```

```js
// 用法：找数组中第一个小于0的数字
let arr = [1, 2, 4, 0, -4, 3, -2, 9];
let result = arr.find(function (item) {
    return item < 0; //遍历过程中，根据这个条件去查找
});
console.log(result); // -4
```

注意通过箭头函数来简化代码。

> 从一个复杂的对象数组中找出符合条件的对象。

```javascript
let data = [
    {id:2,name:'严高',age:15},
    {id:3,name:'徐阶',age:17},
    {id:4,name:'高拱',age:18},
    {id:1,name:'张居正',age:12},
];
```

## findIndex()

findIndex 的使用和 find 类似，只不过它查找的不是数组中的元素，而是元素的下标。



## includes()

功能：判断数组是否包含某个值，返回 true / false

格式：`数组.includes(参数1，参数2)`

- 参数1，必须，表示查找的内容
- 参数2，可选，表示开始查找的位置，0表示从第一个元素开始找。默认值是0。

```js
let arr = [1, 4, 3, 9];
console.log(arr.includes(4)); // true
console.log(arr.includes(4, 2)); // false， 从2的位置开始查，所以没有找到4
console.log(arr.includes(5)); // false
```

> 字符串也有这个方法，功能也是相似的。

# Set对象

Set是集合的意思。是ES6 中新增的内置对象，它类似于数组，但是成员的值都是唯一的，即没有重复的值。使用它可以方便地实现用它就可以实现数组去重的操作。

## 创建set对象

- 创建空set；

  ```js
  // 1. 基本使用
  let set = new Set();
  // 得到一个空的Set对象
  ```

- 根据已有数组创建set

```js
let set = new Set([1,2,3])
```

## Set 的成员方法

- `size`：属性，获取 `set` 中成员的个数，相当于数组中的 `length`
- `add(value)`：添加某个值，返回 Set 结构本身。
- `delete(value)`：删除某个值，返回一个布尔值，表示删除是否成功。
- `has(value)`：返回一个布尔值，表示该值是否为`Set`的成员。
- `clear()`：清除所有成员，没有返回值。
- ` forEach`:遍历

## 应用-数组去重

```javascript
let arr = [1,1,2,3,3];
console.log([...new Set(arr)])
```

# String的扩展

es6中对字符串提供了新的特性，我们介绍其中几个方法：

- 模板字符串
- includes
- startsWith
- endsWith
- repeat

## 模板字符串

在做字符串拼接时，使用+来拼接复杂内容是很麻烦的，而模板字符串可以解决这个问题。

格式：\``${变量}` `${表达式}`\`

语法：

- 模板字 符串使用反引号 **`** 把内容括起来，类似于普通字符串的""。
- ${}充当界定符的作用，其中可以写变量名，表达式等。
- 允许字符串内部进行换行，代码更好读更好的体验

```javascript
let name = 'zs';
let age = 18;
// 拼接多个变量，在模板字符串中使用占位的方式，更易懂
let str = `我是${name}，今年${age}`;

// 内容过多可以直接换行
let obj = [{name: 'flex', age: 20},{name: 'james', age: 21}];

let arr = ['175cm', '60kg'];
let html = `
	<div>
		<ul>
			<li>${obj.name}</li>
			<li>${obj.age}</li>
			<li>${arr[0]}</li>
			<li>${arr[1]}</li>
		</ul>
	</div>`;
```

## includes()

- 格式：`str.includes(searchString, [position])`		
- 功能：返回布尔值，表示是否找到了参数字符串
  - position: 从当前字符串的哪个索引位置开始搜寻子字符串，默认值为0。

## startsWith()

- 格式：`str.startsWidth(searchString, [position])`         
- 功能：返回布尔值，表示参数字符串是否在原字符串的头部或指定位置
  - position: 在 `str` 中搜索 `searchString` 的开始位置，默认值为 0，也就是真正的字符串开头处。

## endsWith()

- 格式：`str.endsWith(searchString, [len])`            
- 功能：返回布尔值，表示参数字符串是否在原字符串的尾部或指定位置.
  - len:可选。作为 `str` 的长度。默认值为 `str.length`。

## repeat()

`repeat`方法返回一个新字符串，表示将原字符串重复`n`次。

语法:`str.repeat(n)`

```js
let html = '<li>itheima</li>';
html = html.repeat(10);
```



# ECMAScript 6 降级处理

## ES 6 的兼容性问题

- ES6 (2015年10月)虽好，但是有兼容性问题，IE7-IE11 基本不支持 ES6

  [ES6 兼容性列表](http://kangax.github.io/compat-table/es6/)

- 在最新的现代浏览器、移动端、Node.js 中都支持 ES6

- 后续我们会讲解如何处理 ES6 的兼容性

## ES 6 降级处理

因为 ES 6 有浏览器兼容性问题，可以使用一些工具进行降级（把ES6的代码转成ES5的代码·），例如：**babel**

![](C:/Users/Administrator/Desktop/01-ES6.assets/babel%E8%BD%AC%E7%A0%81.gif)

babel官网](https://www.babeljs.cn/)

实时转码：https://babeljs.io/repl

