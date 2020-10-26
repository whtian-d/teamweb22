# JS高级-day01

## 1.两大编程思想：

### 1.1面向过程

**面向过程：POP(Process-oriented programming)**

> 面向过程就是分析出解决问题所需要的步骤，然后用函数把这些步骤一步一步实现，使用的时候再一个一个的依次调用就可以了。

​	**大象放到冰箱：打开冰箱==》放入大象==》关上冰箱**

![img](file://E:/%E5%89%8D%E7%AB%AF%E5%B0%B1%E4%B8%9A%E7%8F%AD92%E6%9C%9F/%E5%B0%B1%E4%B8%9A%E7%8F%AD/images/%E8%BF%87%E7%A8%8B.jpg?lastModify=1577265193)

### 1.2面向对象

**面向对象：OOP (Object Oriented Programming)**

> 面向对象是把事务分解成为一个个对象，然后由对象之间分工与合作。

​     大象，冰箱：都看成对象功能

**面向对象和过程区别**

​	面向过程：小项目

​	面向对象：多人合作大项目

​	 **比如：**

​	一个人盖小狗窝，直接和泥，方砖，修饰既可

​	但是盖高楼的话，需要打地基，需要运输材料，需要财务结算等，此时不需要等，个做个的，效率高【模块完成】

### 1.3面向过程与面向对象对比

|      | 面向过程                                                     | 面向对象                                                     |
| ---- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| 优点 | 性能比面向对象高，适合跟硬件联系很紧密的东西，例如单片机就采用的面向过程编程。 | 易维护、易复用、易扩展，由于面向对象有封装、继承、多态性的特性，可以设计出低耦合的系统，使系统 更加灵活、更加易于维护 |
| 缺点 | 不易维护、不易复用、不易扩展                                 | 性能比面向过程低                                             |

> 简单程序用面向过程，复杂程序用面向对象.

### 1.4面向对象三大特性

> 封装性: 封装就是把抽象出来的数据和对数据的操作封装成一个类. 

> 继承性: 对象b可以继承对象a中的属性和方法。可以减少代码冗余 .

> 多态性: 多个形态，各个功能互不影响。

## 2. ES6中的类和对象

> 类抽象了对象的公共部分，它泛指某一大类（class）,抽取，把对象的属性和行为封装成一个类

> 对象特指某一个，通过类实例化一个具体的对象,类中的具体的某个实例(属性和方法的集合体)

**面向对象的思维特点:**

​	 1.抽取（抽象）对象共用的属性和方法组织(封装)成一个类(模板)

​	 2.对类进行实例化, 获取类的对象

### 2.1 ES6中的类

> 在ES6中新增加了类的概念，可以使用class关键字声明一个类，之后以这个类来实例化对象。
>
> 【构造函数实例化对象】

- 类抽象了对象的公共部分，它泛指某一大类（class）

#### 2.1.1创建类

```js
语法：class 类名 {属性和方法}【构造函数语法糖】
class Person {}
注意类名首字母大写
类要抽取公共属性方法，定义一个类
```

示例

```js
 // 1. 创建类 class  创建一个 明星类
 class Star {
	// 类的共有属性放到 constructor 里面
 	constructor(name, age) {
 	this.name = name;
 	this.age = age;
	 }
 }

 // 2. 利用类创建对象 new实例化对象
 var ldh = new Star('刘德华', 18);
 console.log(ldh);    
```

#### 2.1.2类constructor构造函数

```js
class Star {
	constructor (uname,age){
		this.uname = uname;
		this.age = age;
  		}
  }

  //属性：放到constructor，构造函数里面
  //注意：类里面的方法不带function，直接写既可
  //类里面要有属性方法，属性方法要是想放到类里面，我们用constructor构造器
  //构造函数作用：接收参数，返回实例对象，new的时候主动执行，主要放一些公共的属性
```

> constructor() 方法是类的构造函数(默认方法)，用于传递参数,返回实例对象，通过new命令生成对象实例时，自动调用该方法。
>
> 注意：每个类里面一定有构造函数，如果没有显示定义, 类内部会自动给我们创建一个constructor() ，
>
> 注意：this代表当前实例化对象，谁new就代表谁

#### 2.1.3类创建添加方法

```js
 class Star {
 	constructor () {}
  		sing () {}
  		tiao () {}
  }           

//注意:方法和方法之间不能加逗号
```

```js
class 类名 { 
	constructor(){}   
	方法名(){} 
	 }              

//注意：类中定义属性，调用方法都得用this
//this.属性    this.方法()
```

> 注意：方法之间不能加逗号分隔，同时方法不需要添加function 关键字

> **总结：类有对象的公共属性和方法，用class创建，class里面包含constructor和方法，我们把公共属性放到constructor里面，把公共方法直接往后写既可，但是注意不要加逗号**

#### 2.1.4类的继承extends

```js
// 父类
class Father{
} 
// 子类继承父类
class  Son  extends Father { 
}       
```

示例

```js
class Father {
	constructor(surname) {
		this.surname= surname;
		}
	say() {
		console.log('你的姓是' + this.surname);
		}
  }                                       
```

```js
class Son extends Father{  // 这样子类就继承了父类的属性和方法
}
var damao= new Son('刘');
damao.say();      //结果为 你的姓是刘
```

#### 2.1.5 子类使用super关键字访问父类的方法

我们应用的过程中会遇到父类子类都有的属性，此时，没必要再写一次，可以直接调用父类的方法就可以了

> super关键字用于访问和调用对象父类上的函数。
>
> 可以调用父类的构造函数，也可以调用父类的普通函数

```js
当子类没有constructor的时候可以随意用父类的
但是如果子类也含有constructor的话，constructor会返回实例，this的指向不同，不可以再直接使用父类的东西
super：调用父类的方法（普通方法，构造方法）
```

**调用父类构造函数**

```js
//定义了父类
class Father {
   constructor(x, y) {
      this.x = x;
      this.y = y;
   }
   sum(){
       console.log(this.x + this.y);
   }
}

//子元素继承父类
class Son extends Father{
    constructor(x, y){
         super(x, y); //使用super调用了父类中的构造函数
    }
}

var son = new Son(1, 2);
son.sum(); //结果为3    
//注意: 子类在构造函数中使用super, 必须放到this 前面(必须先调用父类的构造方法,在使用子类构造方法)
```

**调用父类普通函数**

```js
  class Father {
      constructor (uname, age){
           this.uname = uname;
           this.age = age;
      }
      qian (){
          console.log('一个亿');
      }
  }   

// 让Son继承Father
class Son extends Father{
    // 再写自己的构造函数
    constructor (uname, age, score){
        // 实例对象：子类的实例对象
        // 如果子类也有自己的构造函数，同时还想继承父类的构造函数的话,那么就要用super
        //子类在构造函数中使用super, 必须放到this 前面(必须先调用父类的构造方法,在使用子类构造方法)
         super(uname, age);
         this.score = score;
    }
    qian () {
        // super：调用父类的方法
        super.qian();
        console.log('2毛钱');
    }
}        

var obj = new Son('儿子', 16, 99);
console.log(obj);
obj.qian();                
```

注意：如果子类也有相同的方法，优先指向子类，就近原则

**总结：super调用父类的属性和方法，那么查找方法的原则就近原则**

属性和方法：

> 属性：如果子类既想有自己的属性，又想继承父类的属性，那么我们用super【super(参数，参数)】

> 方法：如果子类和父类有相同的方法，假如子类依旧想用父类的方法，那么用super调用【super.方法()】

> 如果子类不写东西，那么直接继承父类就可以用 

> 如果子类有自己的构造函数和父类同名的方法，此时不可以直接用父类的东西，需要用super调用父类的方法和构造函数

**注意:** 

1. 继承中,如果实例化子类输出一个方法,先看子类有没有这个方法,如果有就先执行子类的
2. 继承中,如果子类里面没有,就去查找父类有没有这个方法,如果有,就执行父类的这个方法(就近原则)
3. 如果子类想要继承父类的方法,同时在自己内部扩展自己的方法,利用super 调用父类的构造函数,super 必须在子类this之前调用

```js
// 父类有加法方法
 class Father {
   constructor(x, y) {
   this.x = x;
   this.y = y;
   }
   sum() {
   console.log(this.x + this.y);
   }
 }
 // 子类继承父类加法方法 同时 扩展减法方法
 class Son extends Father {
   constructor(x, y) {
   // 利用super 调用父类的构造函数 super 必须在子类this之前调用,放到this之后会报错
   super(x, y);
   this.x = x;
   this.y = y;
  }
  subtract() {
  console.log(this.x - this.y);
  }
}
var son = new Son(5, 3);
son.subtract(); //2
son.sum();//8
```

### 2.2三个注意点

> 1.在ES6中类没有变量提升，所以必须先定义类，才能通过类实例化对象.

> 2.类里面的共有属性和方法一定要加this使用.【this，对象调用属性和方法】

> 3.类里面的this指向问题. 
>
> constructor 里面的this指向实例对象, 
>
> 方法里面的this 指向这个方法的调用者

```js
class Button {
    constructor () {
        var btn = document.querySelector('input');
        btn.onclick = this.cli;
    }
    cli () {
        console.log('点击了');
    }
}

var anniu = new Button();
```

### 2.3 类里面的this指向

- 构造函数的this指向实例对象
- 普通函数的this是调用者，谁调用this是谁

```js
<body>
    <input type="button" value="点击1" id="btn1">
    <input type="button" value="点击2" id="btn2">
    <script type="text/javascript">
        // 构造函数里面的this指向：实例对象
        // 方法里面的this指向：调用者
        class Btn {
            constructor (id) {
                this.id = document.querySelector(id);
                // 点击按钮调用cli
                // 添加：点击调用方法，注意不要给这个方法加括号,加括号会直接执行方法
                // this.id ,this.cli;
                this.id.onclick = this.cli;
                // console.log(this);
            }

            cli () {
                // console.log('这是一个方法');
                console.log(this);
            }
        }

        var obj = new Btn('#btn1');
        obj.cli();
        // console.log(obj);
        // obj.cli();
    </script>
</body>

```

### 2.4对象

对象是由属性和方法组成的：是一个无序键值对的集合,指的是一个具体的事物

- 属性：事物的特征，在对象中用属性来表示（常用名词）
- 方法：事物的行为，在对象中用方法来表示（常用动词）

#### 2.4.1创建对象

- 在ES5中创建对象可以通过以下三种方式：

> 对象字面量

```js
//字面量创建对象
var obj = {
            // 属性和方法
            // 键值对
            // 对象：成员
            uname : '阿飞',
            age : 22,
            sex : '男',
            fei : function () {
                console.log('飞飞飞');
            }
        };

// 访问属性和方法
// console.log( obj.uname );
// console.log( obj['age'] );
// obj.fei();

// 遍历对象
    for ( var key in obj ) {
        // 遍历对象的时候，千万不要用对象.属性
        console.log( obj[key] );
    }
```

> new Object()【构造函数】

```js
// 构造函数
   var obj = new Object();
// instanceof  -----------------判断是不是属于什么数据类型
// arr instanceof Array     
// console.log(obj instanceof Object);
// 添加属性
   obj.uname = '张三丰';
   obj.age = 22;
   obj.sex = '男'; 
   obj.taiji = function () {
    console.log('太极');
   }
// console.log(obj);
```

> 自定义构造函数 

```js
// 自定义构造函数
        function Person (uname, age) {
            // 属性
            this.uname = uname;
            this.age = age;

            // 方法
            this.say = function () {
                console.log('说话');
            }
        }

        var n = new Person('阿飞', 22);
        console.log(n);
        n.say();
      
        var m = new Person('带土', 23);
        console.log(m);
```

## 3.面向对象案例-tab 栏切换

### 3.1tab 栏切换

```js
1.tab栏切换的主要思路是：

2.点击当前li 添加liactive类,其余li移除类

3.根据当前li的索引号,当前section 添加类，其余section 删除类

4.这里可以把添加放入切换函数里面

5.新增一个清除类函数，专门移除其余li和section 类

6.注意里面this 指向问题
```

### 3.2tab 栏切换添加功能

```js
1.点击+ 可以实现添加新的选项卡和内容

2.第一步: 创建新的选项卡li 和新的内容section

3.第二步: 把创建的两个元素追加到对应的父元素中.

4.以前的做法:  动态创建元素createElement, 但是元素里面内容较多, 需要innerHTML赋值,在appendChild追加到父元素里面.

5.现在高级做法:   利用insertAdjacentHTML() 可以直接把字符串格式元素添加到父元素中

6.appendChild不支持追加字符串的子元素, insertAdjacentHTML支持追加字符串的元素

7.insertAdjacentHTML(追加的位置,‘要追加的字符串元素’)  

8.追加的位置有: beforeend插入元素内部的最后一个子节点之后

9.该方法地址:  https://developer.mozilla.org/zh-CN/docs/Web/API/Element/insertAdjacentHTML
```

# JS高级-day02

## 1.构造函数和原型

```js
在典型的OOP 的语言中（如Java），都存在类的概念，类就是对象的模板，对象就是类的实例，但在ES6之前，JS 中并没用引入类的概念。

ES6，全称ECMAScript6.0 ，2015.06 发版。但是目前浏览器的JavaScript 是ES5 版本，大多数高版本的浏览器也支持ES6，不过只实现了ES6 的部分特性和功能。

在ES6之前，对象不是基于类创建的，而是用一种称为构建函数的特殊函数来定义对象和它们的特征。
```

## 2.构造函数

```js
构造函数是一种特殊的函数，主要用来初始化对象，即为对象成员变量赋初始值，它总与new一起使用。我们可以把对象中一些公共的属性和方法抽取出来，然后封装到这个函数里面。
function Fn () {}
```

**在JS 中，使用构造函数时要注意以下两点：**

> 1.构造函数用于创建某一类对象，其首字母要大写

> 2.构造函数要和new 一起使用才有意义

```js
function Fn (uname, age) {
            this.uname = uname;
            this.age = age;
        }
        
new Fn('阿飞',22);
```

## 3.**new在执行时会做四件事情**

> 1.在内存中创建一个新的空对象。

> 2.让this指向这个新的对象。

> 3.执行构造函数里面的代码，给这个新对象添加属性和方法。

> 4.返回这个新对象（所以构造函数里面不需要return）。

## 4.静态成员和实例成员

```js
JavaScript 的构造函数中可以添加一些成员，可以在构造函数本身上添加，称为静态成员
也可以在构造函数内部的this上添加,称为实例成员。
```

静态成员：在构造函数本身上添加的成员称为静态成员，只能由构造函数本身来访问

实例成员：在构造函数内部创建的对象成员称为实例成员，只能由实例化的对象来访问

```js
function Person (uname, age) {
            // 实例成员
            this.uname = uname;
            this.age = age;
        }
     // 静态成员
     Person.sex = '男';

     var ldh = new Person('刘德华', 23);

     // console.log( ldh.sex );      ---->undefined
     console.log( Person.sex );     // 静态成员只能有构造函数访问
     console.log( ldh.uname );      // 实例成员只能由实例对象访问
```

## 5.构造函数原型对象prototype

**构造函数存在小问题：**

> 当实例化对象的时候，属性好理解，属性名属性值，那么方法是函数，函数是复杂数据类型
>
> 那么保存的时候是保存地址，又指向函数，而每创建一个对象，都会有一个函数，
>
> 每个函数都得开辟一个内存空间，此时浪费内存了，那么如何节省内存呢，我们需要用到原型
>
> 方法放到构造函数里面，如果多次实例化，会浪费内存

```js
function Star (uname, age) {
    this.uname = uname;
    this.age = age;
    this.sing = function () {
        console.log(this.name + '在唱歌');
    }
}

var ldh = new Star('周星驰', 22);
var ldh = new Star('刘德华', 22);
```

<img src="images/内存.jpg"> 

**构造函数原型对象prototype**

> 原型对象：就是一个属性，是构造函数的属性，这个属性是一个对象，也称呼prototype 为原型对象。

> 每一个构造函数都有一个属性，prototype

> 作用：是为了共享方法，从而达到节省内存

> 构造函数通过原型分配的函数是所有对象所共享的。
>
> JavaScript 规定，每一个构造函数都有一个prototype 属性，指向另一个对象。
>
> 这个prototype 就是一个对象，对象的所有属性和方法，都会被构造函数所拥有。
>
> 把那些不变的方法，直接定义在prototype 对象上，这样所有对象的实例就可以共享这些方法。

```js
function Star (uname, age) {
        this.uname = uname;
        this.age = age;
        // this.sing = function () {
        //  console.log(this.name + '在唱歌');
        // }
    }

    Star.prototype.sing = function () {
        console.log(this.uname + '在唱歌');
    }

    var zxc = new Star('周星驰', 22);
    var ldh = new Star('刘德华', 22);
    // console.log( Star.prototype );
    ldh.sing();
    zxc.sing();
```

> **总结：所有的公共属性写到构造函数里面，所有的公共方法写到原型对象prototype里面**

 疑问：为何创建一个对象，都可以自动的跑到原型对象上找方法

 因为每一个对象都有一个属性，对象原型，执行原型对象

## 6.对象原型：____proto____

> 主要作用：指向prototype【对象原型（____proto____）作用是为了指向原型对象（prototype）】

> 对象原型：是对象的一个属性

构造函数和原型对象都会有一个属性**proto** 指向构造函数的prototype 原型对象，之所以我们对象可以使用构造函数prototype 原型对象的属性和方法，就是因为对象有**proto** 原型的存在。

```
__proto__是一个非标准属性，不可以拿来赋值或者设置，（只读属性）
```

> 1.____proto____对象原型和原型对象prototype 是等价的

> 2.____proto____对象原  型的意义就在于为对象的查找机制提供一个方向，或者说一条路线，但是它是一个非标准属性，因此实际开发中，不可以使用这个属性，它只是内部指向原型对象prototype

![img](file://E:/%E5%89%8D%E7%AB%AF%E5%B0%B1%E4%B8%9A%E7%8F%AD92%E6%9C%9F/%E5%B0%B1%E4%B8%9A%E7%8F%AD/images/%E5%85%B3%E7%B3%BB%E5%9B%BE.jpg?lastModify=1577270558)

**总结：每一个对象都有一个原型，作用是指向原型对象prototype**

**统一称呼：____proto____原型，prototype成为原型对象**

## 7.constructor  构造函数

> **记录是哪个构造函数创建出来的**
>
> constructor是一个属性：原型对象的一个属性，
>
> 作用：指回构造函数本身

原型（**proto**）和构造函数（prototype）原型对象里面都有一个属性constructor属性，constructor 我们称为构造函数，因为它指回构造函数本身。constructor 主要用于记录该对象引用于哪个构造函数，它可以让原型对象重新指向原来的构造函数。一般情况下，对象的方法都在构造函数的原型对象中设置。如果有多个对象的方法，我们可以给原型对象采取对象形式赋值，但是这样就会覆盖构造函数原型对象原来的内容，这样修改后的原型对象constructor  就不再指向当前构造函数了。此时，我们可以在修改后的原型对象中，添加一个constructor 指向原来的构造函数。

**总结：constructor  主要作用可以指回原来的构造函数**本身

> 构造函数、实例、原型对象三者之间的关系

![img](file://E:/%E5%89%8D%E7%AB%AF%E5%B0%B1%E4%B8%9A%E7%8F%AD92%E6%9C%9F/%E5%B0%B1%E4%B8%9A%E7%8F%AD/images/%E6%9E%84%E9%80%A0%E5%87%BD%E6%95%B0%EF%BC%8C%E5%8E%9F%E5%9E%8B%E5%AF%B9%E8%B1%A1%EF%BC%8C%E5%AF%B9%E8%B1%A1%E5%AE%9E%E4%BE%8B%E5%85%B3%E7%B3%BB.jpg?lastModify=1577270558)

**思考：如果传入一个对象给原型对象添加方法呢**

```js
Star.prototype = {
    sing : function () {},
    dance: function () {}
};
此时会覆盖原先prototype中的内容，传入一个新的对象，那么此时就不知道构造函数是哪个了
所以我们要指回构造函数：constructor：构造函数
```

```js
       function Star (uname, age) {
			this.uname = uname;
			this.age = age;
		}

		// 原型对象：方法
		// Star.prototype.chang = function () {
		// 	console.log('唱歌');
		// }
		// Star.prototype.tiao = function () {
		// 	console.log('跳舞');
		// }

		Star.prototype = {
			constructor : Star,
			chang : function () {},
			tiao : function () {},
			rap : function () {}
		}

		// 实例对象
		var obj = new Star('阿飞', 23);

		// console.log(Star.prototype.constructor);
		console.log( Star.prototype );
	</script>
```

## 8.原型链

```
原型链：由原型所串起来的一个链式

作用：提供一个成员的查找机制，或者查找规则
```

<img src="images/原型链.jpg">

## JavaScript 的成员查找机制(规则)

```
当访问一个对象的属性（包括方法）时，首先查找这个对象自身有没有该属性。

如果没有就查找它的原型（也就是__proto__指向的prototype 原型对象）。

如果还没有就查找原型对象的原型（Object的原型对象）。

依此类推一直找到Object 为止（null）。

__proto__对象原型的意义就在于为对象成员查找机制提供一个方向，或者说一条路线。

// console.log(Star.prototype.__proto__.__proto__);
// console.log(Object.prototype);
```

## 9.扩展内置对象

```
可以通过原型对象，对原来的内置对象进行扩展自定义的方法。比如给数组增加自定义求偶数和的功能。

```

```js
console.log( Array.prototype );
	// 添加求和方法
	Array.prototype.sum = function () {
		var sum = 0;
		for (var i = 0; i < this.length; i++) {
			sum += this[i];
		}
		return sum;
	}

	var arr = [1,2,3];
	console.log( arr.sum() );

	var newArr = [6,7,8,9];
	console.log( newArr.sum() );
```

## 10.上午回顾：

​			创建对象：

​				字面量：var obj = {};

​				构造函数：var obj = new Object();

​				自定义构造函数：var obj = new Star();

​			new执行过程：创建新的对象，this指向这个对象，函数执行，返回这个对象

​			成员：静态成员，实例成员

​			原型对象：构造函数一个属性，共享方法

​			对象原型：每一个对象一个属性，指向原型对象

​			constructor：构造函数，指回构造函数本身

​			原型链：提示一个查找方向

属性==>构造函数

方法==>原型对象

## 11.继承-组合继承

```
ES6之前并没有给我们提供extends继承。我们可以通过构造函数+原型对象模拟实现继承，被称为组合继承。

```

```
call()
调用这个函数, 并且修改函数运行时的this 指向

fun.call(thisArg, arg1, arg2, ...);call把父类的this指向子类

thisArg ：当前调用函数this 的指向对象

arg1，arg2：传递的其他参数

```

**利用构造函数实现子类的继承：**

### 11.1**属性的继承**

组合继承：构造函数和原型对象

```js
function Father (uname,age) {
    // this指向父类的实例对象
    this.uname = uname;
    this.age = age;
    // 只要把父类的this指向子类的this既可
}

function Son (uname, age,score) {
    // this指向子类构造函数
    // this.uname = uname;
    // this.age = age;
    // Father(uname,age);
    Father.call(this,uname,age);
    this.score = score;
}

Son.prototype.sing = function () {
    console.log(this.uname + '唱歌')
}
var obj = new Son('刘德华',22,99);
console.log(obj.uname);
console.log(obj.score);
obj.sing();
```

### **11.2方法的继承：**

> **实现方法:把父类的实例对象保存给子类的原型对象**

```
一般情况下，对象的方法都在构造函数的原型对象中设置，通过构造函数无法继承父类方法。核心原理：

将子类所共享的方法提取出来，让子类的prototype 原型对象= new 父类()  

本质：子类原型对象等于是实例化父类，因为父类实例化之后另外开辟空间，就不会影响原来父类原型对象

将子类的constructor 

方法继承：把父类的实例对象赋值给子类的原型对象，再用contructor指回子类构造函数本身

```

```js
function Father () {

		}
		Father.prototype.chang = function () {
			console.log('唱歌');
		}

		function Son () {

		}
		// Son.prototype = Father.prototype;
		Son.prototype = new Father();
		var obj = new Son();
		obj.chang();

		Son.prototype.score = function () {
			console.log('考试');
		}

		// obj.score();
		// console.log(Son.prototype);
		console.log(Father.prototype);
```

**注意：一定要让Son指回构造函数**

```js
实现继承后，让Son指回原构造函数

Son.prototype = new Father();

Son.prototype.constructor = Son;
```

**总结：用构造函数实线属性继承，用原型对象实线方法继承**

ES5：组合继承，构造函数和原型对象

属性继承：调用父类函数，用call改变this指向

方法继承；把父类的实例对象赋值给子类的原型，用contructor指回子类构造函数本身

## 12.类的本质

```
class本质还是function

类的所有方法都定义在类的prototype属性上

类创建的实例,里面也有__proto__ 指向类的prototype原型对象

所以ES6的类它的绝大部分功能，ES5都可以做到，
新的class写法只是让对象原型的写法更加清晰、更像面向对象编程的语法而已。

所以ES6的类其实就是语法糖.

语法糖:语法糖就是一种便捷写法简单理解, 
有两种方法可以实现同样的功能, 但是一种写法更加清晰、方便,那么这个方法就是语法糖

```

```js
	class Star {}
	console.log( typeof Star );
	var obj = new Star();
	console.log(obj.__proto__);
	console.log(Star.prototype);
```

## 13.ES5 中的新增方法

> ES5 中给我们新增了一些方法，可以很方便的操作数组或者字符串，这些方法主要包括：
>
> 数组方法:  迭代(遍历)方法:   forEach()     filter()       some()    map()    every()
>
> 字符串方法:  trim()

### 13.1 **forEach()**-遍历

```
array.forEach(function(currentValue, index, arr))

currentValue：数组当前项的值
index：数组当前项的索引
arr：数组对象本身

```

```js
var arr = ['red','blue','yellow','orange'];

arr.forEach(function (elm,i,arrAbc) {
	console.log(elm,i,arrAbc);
});
```

### 13.2 **filter()**-筛选

```
array.filter(function(currentValue, index, arr))

filter() 方法创建一个新的数组，新数组中的元素是通过检查指定数组中符合条件的所有元素,主要用于筛选数组

注意它直接返回一个新数组

currentValue: 数组当前项的值
index：数组当前项的索引
arr：数组对象本身回调函数里面添加return添加返回条件

```

```js
var arr = [100,66,99,123,333,33,44,66];
	var reArr = arr.filter(function (elm, a, n) {

	// console.log(elm,a, n);
	return elm % 2 == 0;

	});
	console.log(reArr);
```

### 13.3 **some()**-查找

```
array.some(function(currentValue, index, arr)) 【注意：找到或者满足条件立刻停止】

some() 方法用于检测数组中的元素是否满足指定条件. 通俗点查找数组中是否有满足条件的元素

注意它返回值是布尔值, 如果查找到这个元素, 就返回true , 如果查找不到就返回false.

如果找到第一个满足条件的元素,则终止循环. 不在继续查找.

currentValue: 数组当前项的值
index：数组当前项的索引
arr：数组对象本身

```

```js
var arr = [100,200,300,400];
var re = arr.some(function (elm,i,arr) {
		// console.log(elm,i,arr);
		console.log(i);
		return elm >= 200;
	});
console.log(re);
```

### 13.4 trim()-删除两侧空白符

```js
var str = '   hello   '
console.log(str.trim()）  //hello   删除字符串两侧的空白符
var str1 = '   he l l o   '
console.log(str.trim()）  //he l l o  删除字符串两侧的空白符
```

## 14.课程回顾

​		**创建对象：字面量，构造函数，自定义构造函数****

​		new的执行：创建一个新对象，this指向这个对象，执行函数，返回这个对象

​		成员：静态成员，实例成员

​		构造函数：属性

​		原型对象：构造函数的一个属性，prototype，【共享方法】

​		对象原型：对象的一个属性，____proto____，【指向原型对象】

​		constructor：属性，【指回构造函数本身】

​		原型链：提供查找成员的机制，方向

​		继承：组合继承：构造函数和原型对象

​			属性：调用父类执行，用call改变this指向

​			方法：把父类的实例对象赋值给子类的原型对象，用constructor指回子类构造函数本身

​		数组方法：forEach()，filter()，some()

# JS高级-day03

## 1.查询商品案例

> 1.把数据渲染到页面中(forEach)

```js
var tbody = document.querySelector('tbody');
data.forEach(function (ele,  i) {
   // console.log(ele);
 var tr = '<tr><td>' + ele.id +'</td><td>' + ele.pname + '</td><td>' + ele.price + '</td></tr>';
 tbody.insertAdjacentHTML('beforeend',tr);
        });
```

```js
insertAdjacentHTML   将指定的文本解析为HTML或XML，并将结果节点插入到DOM树中的指定位置

element.insertAdjacentHTML(position, text);

position是相对于元素的位置，并且必须是以下字符串之一：
beforebegin:   元素自身的前面。
afterbegin:    插入元素内部的第一个子节点之前。
beforeend:     插入元素内部的最后一个子节点之后。
afterend:      元素自身的后面。

text是要被解析为HTML或XML,并插入到DOM树中的字符串。
```

> 2.根据价格显示数据

```js
var btn = document.querySelector('.search-price');
var start = document.querySelector('.start');
var end = document.querySelector('.end');
btn.onclick = function () {
    var reArr = data.filter(function (ele, i) {
    return start.value <= ele.price && ele.price <= end.value;
       });
     tbody.innerHTML = '';s
     reArr.forEach(function (ele) {
 var tr = '<tr><td>' + ele.id +'</td><td>' + ele.pname + '</td><td>' + ele.price + '</td></tr>';
       tbody.insertAdjacentHTML('beforeend',tr);
      });
    };
```

> 3.根据商品名称显示数据

```js
var sele = document.getElementById('sele');
        sele.onchange = function () {
       		var n = [];
        	var id = sele.value;
        	data.some(function (ele) {
        		if (id == 0) {
        			n = data;
        			return true;
        		}else if (ele.id == id) {
        			n.push(ele);
        			return true;
        		}
        	});
        	
 tbody.innerHTML = '';
 n.forEach(function (ele, i) {
	   // console.log(ele);
var tr = '<tr><td>' + ele.id +'</td><td>' + ele.pname + '</td><td>' + ele.price + '</td></tr>';
	  tbody.insertAdjacentHTML('beforeend',tr);
        });
   }
```

## 2.函数的定义和调用

### 2.1函数的定义

> 1.函数声明方式 function 关键字 (命名函数)

```js
function fn(){
    console.log(this);
}
fn();
```

> 2.函数表达式(匿名函数、自调用函数)

```js
// 匿名函数
var fun = function () {
	console.log('哇哈哈');
}
fun();

// 自调用函数
(function (a, b) {
	console.log('内容');
	console.log(a,b);
})('aaa', 'bbb');
```

> 3.创建对象 new Function() 

```js
var f = new Function('a', 'b', 'console.log(a + b)');
f(1, 2);

var fn = new Function('参数1','参数2'..., '函数体')

注意:
Function 里面参数都必须是字符串格式
第三种方式执行效率低，也不方便书写，因此较少使用
所有函数都是 Function 的实例(对象)  
函数也属于对象
```

### 2.2函数的调用

```js
// 普通函数
 function fn () {}
 fn();

// 方法
 var obj = {
   taiji : function () {}
 }
 obj.taiji();

// 构造函数
function Person () {}
 new Person();
			
// 绑定事件
 btn.onclick = function () {}

// 定时器
 window.setInterval(function () {},1000);

// 自调用函数
 (function () {})();
```

## 3.this

### 3.1函数内部的this指向

> 这些 this 的指向，是当我们调用函数的时候确定的。调用方式的不同决定了this 的指向不同

> 一般指向我们的调用者.

<img src="E:/%E5%89%8D%E7%AB%AF%E5%B0%B1%E4%B8%9A%E7%8F%AD92%E6%9C%9F/%E5%B0%B1%E4%B8%9A%E7%8F%AD/images/this.png"/>

### 3.2改变函数内部 this 指向

> JavaScript 为我们专门提供了一些函数方法来帮我们更优雅的处理函数内部this的指向问题，常用的有call()、apply()、bind() 三种方法。

#### 3.2.1 call()方法

call()方法调用一个对象。简单理解为调用函数的方式，但是它可以改变函数的 this 指向

应用场景:  经常做继承. 

```js
fun.call(thisArg, arg1, arg2, ...)

thisArg：在fun 函数运行时指定的this 值
arg1，arg2：传递的其他参数

返回值就是函数的返回值，因为它就是调用函数

function Father () {
	this
}

function Son () { 
   Father.call(this,1,2) 
}

因此当我们想改变this 指向，同时想调用这个函数的时候，可以使用call，比如继承
```

示例：

```js
 function fn (a, b) {
 	console.log(this, a, b);
 }

 var obj = {name : '阿飞', age : 22};

 fn();
 fn.call(obj, 123, 456);
```

```js
var obj = {
			name : '阿飞',
			age : 22,
			fei : function () {
				console.log(this);
			}
		}

		var objN = {name : '带土',age : 22};

		obj.fei();
		console.log( obj.fei );
		obj.fei.call(objN);
```

#### 3.2.2 apply()方法

apply() 方法调用一个函数。简单理解为调用函数的方式，但是它可以改变函数的 this 指向。

应用场景:  经常跟数组有关系

```js
fun.apply(thisArg, [argsArray]):调用函数

thisArg：在fun函数运行时指定的this值
argsArray：传递的值，必须包含在数组里面

返回值就是函数的返回值，因为它就是调用函数

因此apply 主要跟数组有关系，比如使用Math.max() 求数组的最大值

var arr = [1,2,3,66,44,7];

var n = Math.max.apply(arr, arr);
console.log(n);
```

示例：

```js
var obj = {
	name: 'andy'
}

function fn(a, b) {
      console.log(this);
      console.log(a+b)
};

fn()                 //此时的this指向的是window 运行结果为3
fn.apply(obj,[1,2])  //此时的this指向的是对象obj,参数使用数组传递,运行结果为3
```

#### 3.2.3 bind()方法

bind() 方法不会调用函数,但是能改变函数内部this 指向,返回的是原函数改变this之后产生的新函数

如果只是想改变 this 指向，并且不想调用这个函数的时候，可以使用bind

应用场景:不调用函数,但是还想改变this指向

```js
 var obj = {
 name: 'andy'
 };

function fn(a, b) {
	console.log(this);
	console.log(a + b);
};
var f = fn.bind(obj, 1, 2); //此处的f是bind返回的新函数
f();//调用新函数  this指向的是对象obj 参数使用逗号隔开
```

#### 3.2.4 call、apply、bind三者的异同

- 共同点 : 都可以改变this指向
- 不同点:
  - call 和 apply  会调用函数, 并且改变函数内部this指向.
  - call 和 apply传递的参数不一样,call传递参数使用逗号隔开,apply使用数组传递
  - bind  不会调用函数, 可以改变函数内部this指向.
- 应用场景
  1. call 经常做继承. 
  2. apply经常跟数组有关系.  比如借助于数学对象实现数组最大值最小值
  3. bind  不调用函数,但是还想改变this指向. 比如改变定时器内部的this指向. 

## 4.严格模式-strict

### 4.1什么是严格模式

> JavaScript 除了提供正常模式外，还提供了严格模式（strict mode）。
>
> ES5 的严格模式是采用具有限制性 JavaScript变体的一种方式，即在严格的条件下运行 JS 代码。
>
> 严格模式在 IE10 以上版本的浏览器中才会被支持，旧版本浏览器中会被忽略。

- 严格模式对正常的 JavaScript 语义做了一些更改： 
  - 1.消除了 Javascript 语法的一些不合理、不严谨之处，减少了一些怪异行为。
  - 2.消除代码运行的一些不安全之处，保证代码运行的安全。
  - 3.提高编译器效率，增加运行速度。
  - 4.禁用了在 ECMAScript 的未来版本中可能会定义的一些语法，为未来新版本的 Javascript 做好铺垫。比如一些保留字如：class,enum,export, extends, import, super 不能做变量名

### 4.2开启严格模式

严格模式可以应用到整个脚本或个别函数中。因此在使用时，我们可以将严格模式分为为脚本开启严格模式和为函数开启严格模式两种情况。

> 1.为脚本开启严格模式

- 有的 script 脚本是严格模式，有的 script 脚本是正常模式，这样不利于文件合并，所以可以将整个脚本文件放在一个立即执行的匿名函数之中。这样独立创建一个作用域而不影响其他script 脚本文件。

  ```js
  (function (){
    //在当前的这个自调用函数中有开启严格模式，当前函数之外还是普通模式
  　　　　"use strict";
         var num = 10;
  　　　　function fn() {}
  })();
  
  //或者 
  <script>
    　"use strict"; //当前script标签开启了严格模式
  </script>
  
  <script>
    			//当前script标签未开启严格模式
  </script>
  ```

> 1. 为函数开启严格模式

- 要给某个函数开启严格模式，需要把“use strict”;  (或 'use strict'; ) 声明放在函数体所有语句之前。

  ```js
  function fn(){
  　　"use strict";
  　　return "123";
  } 
  //当前fn函数开启了严格模式
  ```

### 4.3严格模式中的变化

严格模式对 Javascript 的语法和行为，都做了一些改变。

> 变量规定: 变量申明必须加var，而且不准删除变量

在正常模式中，如果一个变量没有声明就赋值，默认是全局变量。

严格模式禁止这种用法，变量都必须先用var命令声明，然后再使用。

```js
'use strict'

 num = 10 
 console.log(num)//严格模式后使用未声明的变量--------Uncaught ReferenceError: n is not defined
```

严禁删除已经声明变量。例如，delete x; 语法是错误的。

```js
var num2 = 1;
delete num2;  //严格模式不允许删除变量
```

> 严格模式下this 指向问题

正常模式中全局作用域函数中的this 指向window 对象。
严格模式下全局作用域中函数中的this是undefined。

```
function fn() {
 console.log(this);   //严格模式下全局作用域中函数中的 this指向 是 undefined
}
fn();  

```

以前构造函数时不加new也可以调用,当普通函数，this 指向全局对象
严格模式下,如果构造函数不加new调用, this 指向的是undefined 如果给他赋值则会报错
new 实例化的构造函数指向创建的对象实例。
定时器this 还是指向window 。
事件、对象还是指向调用者。

```js
function Star() {
	 this.sex = '男';
}
// Star();严格模式下,如果 构造函数不加new调用, this 指向的是undefined 如果给他赋值则 会报错.
var ldh = new Star()
console.log(ldh.sex);

setTimeout(function() {
  console.log(this); //c，定时器 this 还是指向 window
}, 2000);  
```

> 函数变化:参数不能重名

```
function fn (a, a) {
			// var a = 2;
			console.log(a+a);
		}
fn(1,2);    //正常模式中,结果是4
fn(1,2);   //严格模式 Uncaught SyntaxError: Duplicate parameter name not allowed in this context

```

函数必须声明在顶层.新版本的JavaScript 会引入“块级作用域”（ES6 中已引入）。为了与新版本接轨，不允许在非函数的代码块内声明函数。【if，for等里面定义函数也不可以，但是现在不可以】

更多严格模式要求参考：https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Strict_mode

## 5.高阶函数

> 高阶函数是对其他函数进行操作的函数，它接收函数作为参数或将函数作为返回值输出。

> 把函数作为参数，或者把函数作为返回值的的函数，称为高阶函数

```
// 把函数当做参数的函数，称为高阶函数，
		// function fn (n) {                   此时fn就是一个高阶函数
		// 	// n = num;
		// 	// n = function () {console.log('哇哈哈')};
		// 	// console.log(n);
		// 	// n();
		// 	// 逻辑与
		// 	// console.log(n);
		// 	n && n();
		// }

		// var num = function () {console.log('哇哈哈')};
		// fn(num);

```

```js
//把函数当做返回值的函数，也叫高阶函数
function fun () {
			var n = function () {console.log('内容')};
			return n;
		}

		var re = fun();
		// re = n
		console.log(re);
		re();
```

> 函数也是一种数据类型，同样可以作为参数，传递给另外一个参数使用。最典型的就是作为回调函数。同理函数也可以作为返回值传递回来

## 6.闭包

### 6.1变量作用域

变量根据作用域的不同分为两种：全局变量和局部变量。

1. 函数内部可以使用全局变量。
2. 函数外部不可以使用局部变量。
3. 当函数执行完毕，本作用域内的局部变量会销毁。

### 6.2什么是闭包

> 闭包（closure）指有权访问另一个函数作用域中变量的函数。

> 简单理解就是 ，一个作用域可以访问另外一个函数内部的局部变量。 

<img src="E:/%E5%89%8D%E7%AB%AF%E5%B0%B1%E4%B8%9A%E7%8F%AD92%E6%9C%9F/%E5%B0%B1%E4%B8%9A%E7%8F%AD/images/%E9%97%AD%E5%8C%85.png"/>

### 6.3闭包的作用

> 作用：延伸变量的作用范围。

```js
 function fn() {
   var num = 10;
   function fun() {
       console.log(num);
 	}
    return fun;
 }
var f = fn();
f();
```

### 6.4闭包的案例

1.利用闭包的方式得到当前li 的索引号

```js
// 以前：
         var lis = document.querySelectorAll('li');
         for (var i = 0; i < lis.length; i++) {
         	lis[i].index = i;     //设置自定义属性保存i
         	lis[i].onclick = function () {
         		// console.dir(this);     dir，打印所有属性和方法
        		console.log(this.index);
         	}
         }

//闭包：
for (var i = 0; i < lis.length; i++) {
// 利用for循环创建了4个立即执行函数
// 立即执行函数也成为小闭包,因为立即执行函数里面的任何一个函数都可以使用它的i这变量
(function(index) {
    lis[index].onclick = function() {
      console.log(index);
    }
 })(i);
}
```

2.闭包应用-3秒钟之后,打印所有li元素的内容

```js
 for (var i = 0; i < lis.length; i++) {
   (function(i) {
     setTimeout(function() {
     console.log(lis[i].innerHTML);
     }, 3000)
   })(i);
}
```

```js
 var name = "The Window";
   var object = {
     name: "My Object",
     getNameFunc: function() {
     return function() {
     return this.name;
     };
   }
 };
console.log(object.getNameFunc()())    不是闭包
-----------------------------------------------------------------------------------
var name = "The Window";　　
  var object = {　　　　
    name: "My Object",
    getNameFunc: function() {
    var that = this;
    return function() {
    return that.name;
    };
  }
};
console.log(object.getNameFunc()())
```

## 7.递归

### 7.1什么是递归

> **递归：**如果一个函数在内部可以调用其本身，那么这个函数就是递归函数。
>
> 简单理解:函数内部自己调用自己, 这个函数就是递归函数

> **注意：**递归函数的作用和循环效果一样，由于递归很容易发生“栈溢出”错误（stack overflow），
>
> 所以必须要加退出条件return。

### 7.2利用递归求1~n的阶乘

```js
//利用递归函数求1~n的阶乘 1 * 2 * 3 * 4 * ..n
 function fn(n) {
     if (n == 1) { //结束条件
       return 1;
     }
     return n * fn(n - 1);
 }
 console.log(fn(3)); -----6
```

### 7.3利用递归求斐波那契数列

```js
// 利用递归函数求斐波那契数列(兔子序列)  1、1、2、3、5、8、13、21...
// 用户输入一个数字 n 就可以求出 这个数字对应的兔子序列值
// 我们只需要知道用户输入的n 的前面两项(n-1 n-2)就可以计算出n 对应的序列值
function fb(n) {
  if (n === 1 || n === 2) {
        return 1;
  }
  return fb(n - 1) + fb(n - 2);
}
console.log(fb(3));
```

### 7.3遍历数据

```js
<script type="text/javascript">
		var data = [ 
			{
				id : 1,
				name : '家电',
				goods : [
					{
						id : 11,
						name : '冰箱',
						goods : [
							{
								id : 111,
								name : '海尔'
							},{
								id : 112,
								name : '美的'
							}
						]
					},{
						id : 12,
						name : '洗衣机 '
					}
				]
			},
			{
				id : 2,
				name : '服饰'
			}
		];

		// var data = [{},{}];
		// 写一个函数，根据给出得到id去能够获取指定的数据
		// 获取数据
		function getId (arr, id) {
			// 定义一个变量
			var obj = {};
			// 遍历
			arr.forEach(function (val, index) {
				if (val.id == id) {
					obj = val;
				} else if (val.goods && val.goods.length > 0) {
					obj = getId(val.goods, id);
				}
			});
			return obj;
		}

		console.log( getId(data,111) );
	</script>
```

# JS高级-day04

## 1.拷贝

**拷贝不能直接赋值，对象赋值的是地址**

```js
//对象是复杂数据类型，直接赋值，赋值的是地址
var obj = {
		name : '张三丰',
		age : 22
	};
var newObj = obj;
obj.name ="李寻欢";
console.log(newObj.name);   ----->李寻欢
```

## 2.浅拷贝assign()

> 浅拷贝: 只拷贝最外面一层

> es6：新方法
>
> Object.assign(target, sources);

```js
<script type="text/javascript">
    var obj = {
        name : '张三丰',
        age : 22,
        color : ['red','blue','yellow'],
        message : {sex : '男',score : 99}
    };

var newObj = {};

// 遍历
// for (var key in obj ) {
// 	newObj[key] = obj[key];
// }
// obj有什么,newObj就有什么
// newObj.name = obj.name;
// newObj.age = obj.age;

//es6：新方法assign()
Object.assign(newObj, obj);

obj.name = '李寻欢';
console.log(newObj.name);    ----->张三丰
obj.message.sex = '女';
console.log(newObj.message.sex);    ----->女
</script>
```

## 3.深拷贝

> 数据里面的所有层次都拷贝

```js
<script type="text/javascript">
    var obj = {
        name : '张三丰',
        age : 22,
        color : ['red','blue','yellow'],
        message : {sex : '男',score : 99}
    };

var newObj = {};

// 封装
function kaobei (newObj, obj) {
    // 要把obj拷贝给newObj
    // 我们发现，obj[key]可能是数组，还能是对象，具有复杂数据
    // 那么此时直接拷贝，又会变成复杂数据类型传递
    for (var key in obj ) {
        // newObj[key] = obj[key];
        if ( obj[key] instanceof Array ) {      // obj[key]是数组，就在遍历
            // newObj[key] = obj[key]
            newObj[key] = [];
            kaobei(newObj[key], obj[key]);
        } else if ( obj[key] instanceof Object ) { // obj[key]是对象，就在遍历
            // newObj[key] = obj[key]
            newObj[key] = {};
            kaobei(newObj[key], obj[key]);
        } else {
            newObj[key] = obj[key];
        }
    }
}

kaobei(newObj, obj);

obj.name = 'aaa';
obj.message.sex = '女';

console.log(obj);
console.log(newObj.name);  ------->张三丰
console.log(newObj.message.sex);  ------->男
</script>
```

## 4.正则表达式

### 4.1正则表达式概述

```
正则表达式（ Regular Expression ）是用于匹配字符串中字符组合的模式。

在JavaScript中，正则表达式也是对象。

作用：检索关键字，过滤敏感字符，表单验证

正则表通常被用来检索、替换那些符合某个模式（规则）的文本，
例如验证表单：用户名表单只能输入英文字母、数字或者下划线， 昵称输入框中可以输入中文(匹配)。
正则表达式还常用于过滤掉页面内容中的一些敏感词(替换)，或从字符串中获取我们想要的特定部分(提取)等 。

其他语言也会使用正则表达式，本阶段我们主要是利用JavaScript 正则表达式完成表单验证。

```

### 4.2正则表达式的特点

```js
1. 灵活性、逻辑性和功能性非常的强。

2. 可以迅速地用极简单的方式达到字符串的复杂控制。

3. 对于刚接触的人来说，比较晦涩难懂。比如：^\w+([-+.]\w+)@\w+([-.]\w+).\w+([-.]\w+)*$

4. 实际开发,一般都是直接复制写好的正则表达式. 
   但是要求会使用正则表达式并且根据实际情况修改正则表达式.   比如用户名:   /^[a-z0-9_-]{3,16}$/
```

### 4.3正则表达式在js中的使用

> **创建正则表达式**

在 JavaScript 中，可以通过两种方式创建一个正则表达式。

> 1.通过调用RegExp对象的构造函数创建 

```js
  var regexp = new RegExp(/123/);   //含义：只要包含123就可以
  console.log(regexp);
```

> 2.利用字面量创建 正则表达式

```js
var reg = /abc/;     //含义：只要包含abc就可以
```

### 4.4正则表达式测试test()

```js
test() 正则对象方法，用于检测字符串是否符合该规则，该对象会返回 true 或 false，其参数是测试字符串

注意正则里面没有引号
regexObj.test(str);
regexObj：正则表达式
str：用户输入字符串

var rg = /123/;
console.log(rg.test(123));   //匹配字符中是否出现123  出现结果为true
console.log(rg.test('abc')); //匹配字符中是否出现123  未出现结果为false
```

### 4.5正则表达式的组成

> 正则表达式中的特殊字符

```js
正则表达式可以由简单的字符构成，比如 /abc/，也可以是简单和特殊字符的组合，比如 /ab*c/ 。
其中特殊字符也被称为元字符，在正则表达式中是具有特殊意义的专用符号，如 ^ 、$ 、+ 等。

正则表达式：简单字符 和 特殊字符【元字符】

特殊字符非常多，可以参考： 
MDN：https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Regular_Expressions

jQuery 手册：正则表达式部分

正则测试工具 ： http://tool.oschina.net/regex
```

#### 4.5.1边界符

```js
正则表达式中的边界符（位置符）用来提示字符所处的位置，主要有两个字符

^ : 表示匹配行首的文本（以谁开始）【/^abc/：以abc为开头】

$ ： 表示匹配行尾的文本（以谁结束）【/^abc$/：只能是abc】

```

```js
// ^：以XXX开头

 var reg = /^abc/;     ----以abc开头

// 测试
 console.log( reg.test('abdabcdefabc') );  false
 console.log( reg.test('123abc') );        false
 console.log( reg.test('ABcabcabc') );     false
 console.log( reg.test('abcdefgabcd') );   true
```

```js
// $：以XXX结尾

 var reg = /abc$/;    ----以abc结尾

// 测试
 console.log( reg.test('abcdefg') );     false
 console.log( reg.test('123abc') );      true
 console.log( reg.test('123abcdABC') );  false
 console.log( reg.test('abcdefgabc') );  true
```

> **如果 ^和 $ 在一起使用，表示必须是精确匹配。**

```js
// 注意：如果^和$一起使用的话，那么就会精确匹配
var reg = /^abc$/;

// 测试
console.log( reg.test('abcdefg') );   false
console.log( reg.test('abcabc') );    false
console.log( reg.test('ABc') );       false
console.log( reg.test('abc') );       true
console.log( reg.test('a&b&c') );     false
```

#### 4.5.2字符类[] 方括号

> ```
> 字符类表示有一系列字符可供选择，只要匹配其中一个就可以了。所有可供选择的字符都放在方括号内。
> 
> ```

```js
// []：多选一
 var reg = /[abc]/;
// 测试
 console.log( reg.test('red') );     false
 console.log( reg.test('blue') );    true
 console.log( reg.test('yellow') );  false
 console.log( reg.test('color') );   true

// 注意：边界符加上中括号
 var reg = /^[abc]$/;                    // /^[abc]$/==必须是a或b或c
 console.log( reg.test('abcd') );   false
 console.log( reg.test('A') );      false
 console.log( reg.test('aa') );     false
 console.log( reg.test('c') );      true

// 匹配a到z中的任意一个
 var reg = /^[a-z]$/;
// 测试
 console.log( reg.test('ab') );   false
 console.log( reg.test('aa') );   false
 console.log( reg.test('D') );    false
 console.log( reg.test('o') );    true
 console.log( reg.test('9') );    false
 console.log( reg.test('6Aa') );  false
		
// 匹配a到z和A到Z中的任意一个
 var reg = /^[a-zA-Z]$/;
 console.log( reg.test('A') );   true
 console.log( reg.test('Aa') );  false
 console.log( reg.test('aa') );  false
 console.log( reg.test('H') );   true
 console.log( reg.test('abc') ); false
 console.log( reg.test('K') );   true
 console.log( reg.test('-') );   false
		
// 字符组合
 var reg = /^[a-zA-Z0-9_-]$/;
 console.log( reg.test('A') );  true
 console.log( reg.test('-') );  true
 console.log( reg.test('6') );  true
 console.log( reg.test('33') ); false
 console.log( reg.test('A3') ); false
 console.log( reg.test('*') );  false
 console.log( reg.test('@') );  false
		
// 取反
var reg = /^[^a-zA-Z0-9_-]$/;
console.log( reg.test('A') );  false
console.log( reg.test('6') );  false
console.log( reg.test('aa') ); true
console.log( reg.test('%') );  true
console.log( reg.test('**') ); true
console.log( reg.test('abc') ); true
```

#### 4.5.3量词符

> ```
> 量词符用来设定某个模式出现的次数。
> 
> ```

```
量词		说明

*		重复0次或更多次【>=0次】/^[a-z]*$/

+		重复1次或更多次【>=1次】【/^[a-z]+$/】

?		重复0次或1次

{n}		重复n次

{n,}	重复n次或更多次

{n,m}	重复n到m次

注意：{n,m}n和m之间不准有空格

边界符：^，$
中括号：[]：被中括号包含的东西只能选1个
量词符：*，+，?，{n,m}

```

```js
// *：重复0次或更多次

// var reg = /^[a-z]*$/;
// console.log( reg.test('abc') );    true
// console.log( reg.test('ABcdef') ); false
// console.log( reg.test('aaa') );    true
// console.log( reg.test('123') );    false
// console.log( reg.test('abcd123') ); false
// console.log( reg.test('') );        true

// + 重复1次或更多次
// var reg = /^[a-z]+$/;
// console.log( reg.test('') );      false
// console.log( reg.test('aa') );    true
// console.log( reg.test('abc') );   true
// console.log( reg.test('a') );     true
// console.log( reg.test('AA') );    false
// console.log( reg.test('ABCabc') );false
	
// ?重复0次或1次
// var reg = /^[a-z]?$/;            
// console.log( reg.test('') );   true
// console.log( reg.test('a') );  true
// console.log( reg.test('ab') ); false
// console.log( reg.test('A') );  false
// console.log( reg.test('AB') ); false
// console.log( reg.test('aaa') );false
		
// {n}重复n次
// var reg = /^[a-z]{3}$/; 
// console.log( reg.test('a') );  false
// console.log( reg.test('aa') ); false
// console.log( reg.test('aaa') );true
// console.log( reg.test('aaaa') );false
// console.log( reg.test('abcdefg') );false
// console.log( reg.test('abc') ); true

// {n,}重复最少n次
// var reg = /^[a-z]{3,}$/;
// console.log( reg.test('a') ); false
// console.log( reg.test('ab') );false
// console.log( reg.test('abc') );true
// console.log( reg.test('abcd') );true
// console.log( reg.test('abcdefg') );true
// console.log( reg.test('AA') );false
		
// {n,m}重复n次到m次
var reg = /^[a-z]{3,6}$/;
console.log( reg.test('a') );    false  
console.log( reg.test('ab') );   false
console.log( reg.test('abc') );  true
console.log( reg.test('abcd') ); true
console.log( reg.test('abcde') ); true
console.log( reg.test('abcdef') ); true
console.log( reg.test('abcdefg') );false
```

### 4.6用户名表单验证

功能需求:

1. 如果用户名输入合法, 则后面提示信息为:  用户名合法,并且颜色为绿色
2. 如果用户名输入不合法, 则后面提示信息为:  用户名不符合规范, 并且颜色为红色

```js
// 获取元素
var txt = document.querySelector('#txt');
// 创建正则
var reg = /^[a-zA-Z0-9]{6,8}$/;
// 添加事件
txt.onblur = function () {
	if ( reg.test(this.value) ) {
			this.nextElementSibling.className = 'right';
			this.nextElementSibling.innerHTML = '你写对了';
	} else {
			this.nextElementSibling.className = 'error';
			this.nextElementSibling.innerHTML = '错了我告诉你';
		}

	}
```

### 4.7括号总结

```
1.大括号  量词符.  里面表示重复次数{}

2.中括号 字符集合。匹配方括号中的任意字符. []

3.小括号表示优先级()

正则表达式在线测试 ： https://c.runoob.com

```

## 5.预定义类

```
预定义类指的是某些常见模式的简写方式.

```

<img src="E:/%E5%89%8D%E7%AB%AF%E5%B0%B1%E4%B8%9A%E7%8F%AD92%E6%9C%9F/%E5%B0%B1%E4%B8%9A%E7%8F%AD/08-JS%E9%AB%98%E7%BA%A7/%E5%B0%B1%E4%B8%9A%E7%8F%AD%E7%AC%AC24%E5%A4%A9%20JS%E9%AB%98%E7%BA%A7/%E7%AC%94%E8%AE%B04/img3.png">

上午回顾：

​	遍历数据：递归 

​	浅拷贝：只拷贝最外面一层【Object.assign(newObj，obj)】

​	深拷贝：所有层都拷贝

正则：规则，字符串组合规则

​	创建正则：var reg = new RegExp(/abc/); var reg = /abc/;

​	测试：reg.test(str);

​	特殊字符：^，$，[]，*，+，？，{n}，{n,}，{n,m}

## 6.验证案例

**手机验证**

```js
var tel = document.getElementById('tel');
var regtel = /^[1][3|4|5|7|8][0-9]{9}$/;
tel.onblur = function () {

	if (regtel.test(tel.value)) {
		this.nextElementSibling.className = 'success';
		this.nextElementSibling.innerHTML = '手机输入正确<i class="success_icon"></i>';
		console.log(123);
	} else {
		tel.nextElementSibling.className = 'error';
		tel.nextElementSibling.innerHTML = '手机输入错误<i class="error_icon"></i>';
		console.log(456)
	}
}
```

**QQ验证：**

```js
var regqq = /^[1-9][0-9]{4,}$/;
var regtel = /^1[3|4|5|7|8][0-9]{9}$/;
var regqq = /^[1-9][0-9]{4,}$/;
	
function jiance (obj, reg) {
	obj.onblur = function () {
		if (reg.test(this.value)) {
			this.nextElementSibling.className = 'success';
			this.nextElementSibling.innerHTML = '<i class="success_icon"></i> 手机输入正确';
		} else {
			this.nextElementSibling.className = 'error';
			this.nextElementSibling.innerHTML = '<i class="error_icon"></i> 手机输入错误';
		}
	}
}

jiance(tel,regtel);
jiance(qq,regqq);
```

**昵称验证：**

```js
var nikName = /^[\u4e00-\u9fa5]{2,8}$/;
```

**短信验证：**

```js
var regmsg = /^[0-9]{6}$/;
```

## 7.replace替换

> /表达式/[修饰符]

> g：全局匹配

> i：忽略大小写

> gi：全局+忽略

屏蔽敏感字符

```
var str = 'abcdefBgabcd';
// 语法：str.replace('b', '哇哈哈');
var n = str.replace(/b/gi,'*');
console.log(n);  -----a*cdef*ga*cd

```

# JS高级-day05

## 1.ES6新增语法

### 1.1 let

> ES6 中新增了用于声明变量的关键字 let

> let声明的变量只在所处于的块级有效

```javascript
 if (true) { 
     let a = 10;
     console.log(a);-----10
 }
console.log(a) // a is not defined
```

**注意：**使用let关键字声明的变量才具有块级作用域，使用var声明的变量不具备块级作用域特性。

> 不存在变量提升

```javascript
console.log(a); // a is not defined 
let a = 20;

console.log(a); // undefined    var声明的变量存在变量提升
var a = 20;
```

> 防止循环变量变成全局变量

```js
for(var i=0;i<2;i++){
    
}
console.log(i) ------2

for(let i=0;i<2;i++){
    
}
console.log(i) ------i is not defined 
```

> 暂时性死区

利用let声明的变量会绑定在这个块级作用域，不会受外界的影响

```javascript
 var tmp = 123;
 if (true) { 
     tmp = 'abc';
     let tmp; 
 } 
```

> 经典面试题

```javascript
 var arr = [];
 for (var i = 0; i < 2; i++) {
     arr[i] = function () {
         console.log(i); 
     }
 }
 arr[0](); ----2
 arr[1](); ----2
```

![](F:/web%E5%89%8D%E7%AB%AF2019/%E8%AF%BE%E4%BB%B62019/10-JavaScript%E9%AB%98%E7%BA%A7%E8%B5%84%E6%96%99/JavaScript%20%E9%AB%98%E7%BA%A7_day05/4-%E7%AC%94%E8%AE%B0/images/let%E9%9D%A2%E8%AF%95%E9%A2%98.png)

**经典面试题图解：**此题的关键点在于变量i是全局的，函数执行时输出的都是全局作用域下的i值。

```javascript
 let arr = [];
 for (let i = 0; i < 2; i++) {
     arr[i] = function () {
         console.log(i); 
     }
 }
 arr[0]();  -----0
 arr[1]();  -----1

```

![](F:/web%E5%89%8D%E7%AB%AF2019/%E8%AF%BE%E4%BB%B62019/10-JavaScript%E9%AB%98%E7%BA%A7%E8%B5%84%E6%96%99/JavaScript%20%E9%AB%98%E7%BA%A7_day05/4-%E7%AC%94%E8%AE%B0/images/let%E9%9D%A2%E8%AF%95%E9%A2%982.png)

**经典面试题图解：**此题的关键点在于每次循环都会产生一个块级作用域，每个块级作用域中的变量都是不同的，函数执行时输出的是自己上一级（循环产生的块级作用域）作用域下的i值.

> 小结

- let关键字就是用来声明变量的
- 使用let关键字声明的变量具有块级作用域
- 在一个大括号中 使用let关键字声明的变量才具有块级作用域     var关键字是不具备这个特点的
- 防止循环变量变成全局变量
- 使用let关键字声明的变量没有变量提升
- 使用let关键字声明的变量具有暂时性死区特性

### 1.2const

> 声明常量，常量就是值（内存地址）不能变化的量

> 具有块级作用域

```javascript
 if (true) { 
     const a = 10;
 }
console.log(a) // a is not defined
```

> 声明常量时必须赋值

```javascript
const PI; // Missing initializer in const declaration
```

> 常量赋值后，值（内存地址）不能修改

```javascript
//基本数据类型
const PI = 3.14;
PI = 100; // Assignment to constant variable.

//复杂数据类型
const ary = [100, 200];
ary[0] = 'a';       //复杂数据类型里面的值可以更改
ary[1] = 'b';
console.log(ary); // ['a', 'b']; 
ary = ['a', 'b']; // Assignment to constant variable.对复杂数据类型不可以直接赋值，会改变内存地址
```

> 小结

- const声明的变量是一个常量
- 既然是常量不能重新进行赋值，如果是基本数据类型，不能更改值，如果是复杂数据类型，不能更改地址值
- 声明 const时候必须要给定值

### 1.3let、const、var 的区别

- 使用 var 声明的变量，其作用域为该语句所在的函数内，且存在变量提升现象
- 使用 let 声明的变量，其作用域为该语句所在的代码块内，不存在变量提升
- 使用 const 声明的是常量，在后面出现的代码中不能再修改该常量的值

![](F:/web%E5%89%8D%E7%AB%AF2019/%E8%AF%BE%E4%BB%B62019/10-JavaScript%E9%AB%98%E7%BA%A7%E8%B5%84%E6%96%99/JavaScript%20%E9%AB%98%E7%BA%A7_day05/4-%E7%AC%94%E8%AE%B0/images/var&let&const%E5%8C%BA%E5%88%AB.png)

## 2.解构赋值

> ES6中允许从数组中提取值，按照对应位置，对变量赋值，对象也可以实现解构

### 2.1数组解构

```javascript
 let [a, b, c] = [1, 2, 3];
 console.log(a)//1
 console.log(b)//2
 console.log(c)//3
//如果解构不成功，变量没有对应的值，变量的值为undefined
```

### 2.2对象解构

```javascript
 let person = { name: 'zhangsan', age: 20 }; 
 let { name, age } = person;        变量的名字匹配对象的属性名
 console.log(name); // 'zhangsan'   匹配成功，将对象的属性值赋值给变量
 console.log(age); // 20

 let {name: myName, age: myAge} = person; // myName myAge 属于别名  
 //   name属性匹配成功，将属性值'zhangsan'赋值给myName
 console.log(myName); // 'zhangsan' 
 console.log(myAge); // 20
```

### 2.3小结

- 解构赋值就是把数据结构分解，然后给变量进行赋值
- 如果解构不成功，变量跟数值个数不匹配的时候，变量的值为undefined
- 数组解构用中括号包裹，多个变量用逗号隔开，对象解构用花括号包裹，多个变量用逗号隔开
- 利用解构赋值能够让我们方便的去取对象中的属性跟方法

## 3.箭头函数

ES6中新增的定义函数的方式。是用来简化函数定义语法的。

```javascript
() => {} 
//()：代表是函数； 
// =>：必须要的符号，指向哪一个代码块；
// {}：函数体
const fn = () => {}//代表把一个函数赋值给常量fn
fn();              //调用
```

函数体中只有一句代码，且代码的执行结果就是返回值，可以省略大括号

```javascript
 function sum(num1, num2) { 
     return num1 + num2; 
 }
 //es6写法
 const sum = (num1, num2) => num1 + num2; 
 sum(10,20)
```

如果形参只有一个，可以省略小括号

```javascript
 function fn (v) {
     return v;
 } 
//es6写法
 const fn = v => v;
```

箭头函数不绑定this关键字，箭头函数中的this，指向的是函数定义位置中的this

```javascript
const obj = { name: '张三'} 
 function fn () { 
     console.log(this);//this 指向 是obj对象
     return () => { 
         console.log(this);//this 指向的是箭头函数定义的位置的this，那么这个箭头函数定义在fn里面，而这个fn指向是的obj对象，所以这个this也指向是obj对象
     } 
 } 
 const resFn = fn.call(obj);  //使用call()方法改变fn的指向为obj
 resFn();
```

### 3.1小结

- 箭头函数中不绑定this，箭头函数中的this指向是它所定义的位置的this，可以简单理解成，定义箭头函数中的作用域的this指向谁，它就指向谁
- 箭头函数的优点在于解决了this执行环境所造成的一些问题。比如：解决了匿名函数this指向的问题（匿名函数的执行环境具有全局性），包括setTimeout和setInterval中使用this所造成的问题

> 面试题

```javascript
var age = 100;

var obj = {       //对象不能产生作用域
	age: 20,
	say: () => {
		alert(this.age)     //this指向window
	}
}

obj.say();//箭头函数this指向的是被声明的作用域里面，而对象没有作用域的，所以箭头函数虽然在对象中被定义，但是this指向的是全局作用域
```

> 剩余参数

箭头函数不能使用arguments

剩余参数语法允许我们将一个不定数量的参数表示为一个数组，不定参数定义方式，这种方式很方便的去声明不知道参数情况下的一个函数

```javascript
function sum (first, ...args) {
     console.log(first); // 10
     console.log(args); // [20, 30] 
 }
 sum(10, 20, 30)
```

```js
 const sum = (...args) => {
 	let total = 0;
 	args.forEach(item => total += item);
 	return total;
 };

 console.log(sum(10, 20));    ---30
 console.log(sum(10, 20, 30));---60
```

> 剩余参数和解构配合使用

```javascript
let students = ['wangwu', 'zhangsan', 'lisi'];
let [s1, ...s2] = students; 
console.log(s1);  // 'wangwu' 
console.log(s2);  // ['zhangsan', 'lisi']
```

## 4.ES6 的内置对象扩展

### 4.1Array 的扩展方法

> 扩展运算符（展开语法） ...

> 扩展运算符可以将数组或者对象转为用逗号分隔的参数序列

```javascript
 let ary = [1, 2, 3];
 ...ary  // 1, 2, 3
 console.log(...ary);    // 1 2 3,相当于下面的代码
 console.log(1,2,3);
```

> 扩展运算符可以应用于合并数组

```javascript
// 方法一 
 let ary1 = [1, 2, 3];
 let ary2 = [3, 4, 5];
 let ary3 = [...ary1, ...ary2];

 // 方法二 
 ary1.push(...ary2);
```

> 将伪数组或可遍历对象转换为真正的数组

```javascript
let oDivs = document.getElementsByTagName('div'); 
oDivs = [...oDivs];
```

### 4.2构造函数方法：Array.from()

> 将伪数组或可遍历对象转换为真正的数组

```javascript
//定义一个伪数组
let arrayLike = {
    '0': 'a',
    '1': 'b',
    '2': 'c',
    length: 3
}; 
//转成数组
let arr2 = Array.from(arrayLike); // ['a', 'b', 'c']
```

方法还可以接受第二个参数，作用类似于数组的map方法，用来对每个元素进行处理，将处理后的值放入返回的数组

```javascript
//定义一个伪数组
let arrayLike = { 
     "0": 1,
     "1": 2,
     "length": 2
 }
 let newAry = Array.from(arrayLike, item => item *2)//[2,4]
```

注意：如果是对象，那么属性需要写对应的索引

### 4.3实例方法：find()

用于找出第一个符合条件的数组成员，如果没有找到返回undefined

```javascript
let ary = [{
     id: 1,
     name: '张三'
 }, { 
     id: 2,
     name: '李四'
 }]; 

 //找数组里面符合条件的值，当数组中元素id等于2的查找出来，注意，只会匹配第一个
 let target = ary.find((item, index) => item.id == 2);
 let target = ary.find(item => item.id == 2);
```

### 4.4实例方法：findIndex()

用于找出第一个符合条件的数组成员的位置，如果没有找到返回-1

```javascript
let ary = [1, 5, 10, 15];
let index = ary.findIndex((value, index) => value > 9); 
let index = ary.findIndex(value => value > 9); 
console.log(index); // 2
```

### 4.5实例方法：includes()

判断某个数组是否包含给定的值，返回布尔值。

```js
[1, 2, 3].includes(2) // true 
[1, 2, 3].includes(4) // false
```

## 5.String 的扩展方法

### 5.1模板字符串

> ES6新增的创建字符串的方式，使用反引号定义

```javascript
let name = `zhangsan`;
```

> 模板字符串中可以解析变量

```javascript
let name = '张三'; 
let sayHello = `hello,my name is ${name}`; // hello, my name is zhangsan
```

> 模板字符串中可以换行

```javascript
 let result = { 
     name: 'zhangsan', 
     age: 20,
     sex: '男' 
 } 
 let html = ` <div>
     <span>${result.name}</span>
     <span>${result.age}</span>
     <span>${result.sex}</span>
 </div> `;
```

> 在模板字符串中可以调用函数

```javascript
const sayHello = function () { 
    return '哈哈哈哈 追不到我吧 我就是这么强大';
 }; 
 let greet = `${sayHello()} 哈哈哈哈`;
 console.log(greet); // 哈哈哈哈 追不到我吧 我就是这么强大 哈哈哈哈
```

### 5.2实例方法：startsWith() 和 endsWith()

- startsWith()：表示参数字符串是否在原字符串的头部，返回布尔值
- endsWith()：表示参数字符串是否在原字符串的尾部，返回布尔值

```javascript
let str = 'Hello world!';
str.startsWith('Hello') // true 
str.endsWith('!')       // true
```

### 5.3实例方法：repeat()

repeat方法表示将原字符串重复n次，返回一个新字符串

```javascript
'x'.repeat(3)      // "xxx" 
'hello'.repeat(2)  // "hellohello"
```

## 6.Set 数据结构

ES6 提供了新的数据结构  Set。它类似于数组，但是成员的值都是唯一的，没有重复的值。

Set本身是一个构造函数，用来生成  Set  数据结构

```javascript
const s = new Set();
```

Set函数可以接受一个数组作为参数，用来初始化。

```javascript
const set = new Set([1, 2, 3, 4, 4]);//{1, 2, 3, 4}
```

### 6.1实例方法

- add(value)：添加某个值，返回 Set 结构本身
- delete(value)：删除某个值，返回一个布尔值，表示删除是否成功
- has(value)：返回一个布尔值，表示该值是否为 Set 的成员
- clear()：清除所有成员，没有返回值

```javascript
 const s = new Set();
 s.add(1).add(2).add(3); // 向 set 结构中添加值 
 s.delete(2)             // 删除 set 结构中的2值   
 s.has(1)                // 表示 set 结构中是否有1这个值 返回布尔值 
 s.clear()               // 清除 set 结构中的所有值
 //注意：删除的是元素的值，不是代表的索引
```

### 6.2遍历

Set 结构的实例与数组一样，也拥有forEach方法，用于对每个成员执行某种操作，没有返回值。

```js
s.forEach(value=>console.log(value))
```

