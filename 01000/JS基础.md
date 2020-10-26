# js基础day01

## 01-js输入输出

```js
  // 记住：只要是文字，字母 必须加单引号 或者双引号，只能用一种
  // 1.输入信息
  // prompt('请输入您的银行卡密码：');
  // prompt接收到的是字符串   接受数据类型：string类型；

  // 2.输出：
  // alert:警告,不点击的话，后面的代码不会执行；
  // alert("这个是弹窗");

  // 3.控制台输出
  // console.log("这是控制台输出");
  // 输出数字
  // console.log(123);
  // 多个输出：语法 用 , 隔开，注意只是console.log()
  // console.log("这是哪里？", "92期前端");
  // console.log("<h1>这是哪里？92期前端</h1>");

  // 在页面文档中输出：
  // 往HTML页面输出，
  // 特点：识别HTML代码，只是 document.write
  // document.write("这是哪里？92期前端");
  // document.write("<h1>这是哪里？92期前端</h1>");
```

##02-js基本数据类型

```js
  1.number 类型
  // var a = 10.1;
  // var b = NaN;
  // NaN：不是某个数，泛指，不确定；

  2.String 类型：字符串
  // 规则：只要两边有单双引号的一种，这个就是String 类型，就是个字符串；
  // var a = "10.1";
  // 转译字符：特殊的字符；" ' \
  // 转一下：JS认为这些特殊的字符，是正常的字符；
  // 语法:  \"，特点必须写在字符串内；
  // var info = '我说：\"xxxxxxx\" ;  他说:\'xxxxxxxxx1\';     她说：\\  ';
  // 字符串遇见 + ，把临近字符串的数据类型 转化为 String类型，形成字符串拼接；
  
  3.boolean 类型：
  // 作用：描述一件事 对或者错？存在？确定？
  // var a = true;
  // var b = false;

  4.Null值; 
  // var a = null;

  5.Undefined类型；
  // var a;
  // js 会给默认值；undefined
```

## 03-js检查数据类型

```js
  var a;
  // 默认值：undefined；

  // 两种用法：
  var aType = typeof(a);
  var aType = typeof a;
```

## 04-js-转数字

```js
  // ========================================= Number方法
  // 传入：参数，传入要转化的值；
  // 返回值：转化后数据；
  //  var a = "100";     只能传入纯数字字符串
  //  a = Number(a);     ----->a=100
  //  var a = "100abc";
  //  a = Number(a);     ----->a=NaN
  //  var a = "abc";
  //  a = Number(a);     ----->a=NaN
  //  var a = true;
  //  a = Number(a);     ----->a=1

  // ========================================== parseInt()方法
  // 返回：整数部分；
  // 传入：参数，转成功的话，只能传入数字部分在前的字符串；
  // var b = "10.1abc";
  //  b = parseInt(b);    ---->b=10
  // 传入是其他（和上面不一样）,返回NaN；
  //  var b = true;
  //  b = parseInt(b);    ---->b=NaN
  // var b = "abc10.1";
  //  b = parseInt(b);    ---->b=NaN

  // ========================================== parseFloat()方法
  // JS小数：浮点数；
  // 返回值：整数加小数部分；
  // 传入：转成功的话，只能传入数字部分在前的字符串；
  // var a = "10.1abc";
  // a = parseFloat(a);  ---->a=10.1
```

## 05-js-转字符串

```js
  // =================================================String()
  // 传入：数据或者变量；
  // 返回：转换后数据，字符串；
  // var b = true;
  // b = String(b);
  
  // ===========================================.toString();
  // 格式：注意有个.
  // 注意：undefined和null不能使用这个方式变成字符串；
  // 用法：数据或者变量.toString()
  // 返回：字符串；
  // var a = 10;
  // a = a.toString();

  // var a = null;
  // a = a.toString();
  // 报错： Uncaught TypeError: Cannot read property 'toString' of null
```

## 06-js-转Boolean

```js
  // ===============================================Boolean()
  // 参数：传入数据或者变量；
  // 返回：true /false;
  // true:  确定，对，成立；
  // false: 不确定，错误，不存在；
```

* 转化为false的几种情况:

```
var res1 = Boolean(0);
var res3 = Boolean(NaN);
var res2 = Boolean('');  // 空字符，里面啥没有，空格也没有；
var res6 = Boolean(false);
var res5 = Boolean(null);  
var res4 = Boolean(undefined); 
```

## 07-js数据转换总结

* 转Number		
  * Number()
    * "100abc"---->NaN;  只识别数字部分；
    * true------->1;
  * parseInt()、parseFloat()：
    - "100abc"---->100;  只识别前面的数字部分；
    - true/null/undefined ----->  NaN；
* 转String：方法内部相当于给你要转的这个数据左右两边加单双引号；
  - String(NaN)  :  ------>"NaN";
  - null.toString()  :  报错， null undefined 不能用；
* 转Boolean：
  - 转false情况
    - 空字符串：“”
    - 数字：0、NaN；
    - null、undefined
    - false

## 08-js-操作符-算术操作符

```js
  // +   -   *   /   %
  // 常规：Number类型 进行 算术运算；
  // 场景：奇偶数判断；
  // var a = 50 % 2;

  // ----------------------------------特别：字符串 遇见 + ;
  // 规则：字符串 遇见 +，使临近字符串的其他数据类型，转化为字符串，形成字符串拼接；
  // 隐式转化：看不见的转化过程；
  // var a = 10 + "abc" + 10;   ---->a="10abc10"
  //  "10"+"abc"+"10";
  // var b = 10 + 10 + 10 + "55" + 10 + 10;    ----->b="30551010"   从左到右运算，遇到"+"再转换

  // -----------------------------------特别：字符串 遇见 -  *  /  %
  // 规则：字符串会隐式转化Number类型；
  // var a = "abc" - 1;    ---->NaN-1----->a=NaN

  // ------------------------------------特别：++  --：
  // 作用：在自己的基础上进行自增1，或自减1；
  // var a = 10;
  // a++;
  // ++a;

  // 规则：++写在a前面，++a先算，计算后的结果，再往位置上提供数据；
  // var a = 10;
  // var b = ++a + 1;    ------>11+1

  // 规则：++写在a的后面，先往位置上提供数据,再进行a++运算（运算后结果不推到位置上）
  // var a = 10;
  // var b = a++ + 1;    ------->10+1
 
  var a = 10;
  var b = a++ + ++a;     -------->10+12
  
  var a = 10;
  var b = ++a + a++;     -------->11+11
```

## 09-js-操作符-比较运算符

```js
  // 比较运算符： >  <  >=  <=
  // 常规：两边都是需要Number类型；
  // = ：优先级最低；
  // 返回：Boolean;
  // >= 满足一个就可以；
  // var a = 4 >= 4;   ---->a=true
 
  // 非常规操作规则：非Number类型要和Number类型比较的话，非Number类型就要隐式转换为Number类型
  // var a = "abc" > 10; ----->NaN > 10 ----->a=false

  // == 规则：
  // 1.如果两边的数据类型不同，非Number类型转Number类型，看值是否相同；
  // 2.如果两边的数据类型相同，看值是否相等；

  // === 规则：(严格，没有隐式转化)
  // 1.直接先看数据类型，如果数据类型不同，直接返回false;
  // 2.如果两边的数据类型相同，看值是否相等；
```

## 10-js-操作符-逻辑运算符

```js
  // && 
  // 且：全部满足，如果有一个条件不满足，直接返回不满足的条件;
  // 执行过程：&& 前后 每个位置上需要一个数据 （Boolean类型）只进行比较，不返回；
  // 返回： 最后成立的结果 或 不成立的结果；
  // var a = true && true;

  // || 或：只要满足一个条件就可以；
  // 返回：满足条件的结果；
  // var a = 1 || 0;   --->1
  // 只是进行比较：true || false;不进行返回；
 
  // !:取反；
  var a = true;
  // 进行取反的运算；
  var b = !a;
   
  //判断闰年的算法： 能被4整除且不能整除100的为闰年；或者能够被 400 整除的就是闰年
   var year = prompt("请输入年份");
    if ((year % 4 == 0 && year % 100 != 0) || year % 400 == 0) {
        alert("是闰年")
    } else {
        alert("不是闰年")
    }
```

## 11-js-操作符-优先级

```js
  // 1. 第一优先级：()
  // 2. 第二优先级：++ -- !
  // 3. 第三优先级： * /  %
  // 4. 第四优先级： + -
  // 5. 第五优先级： > >= < <=
  // 6. 第六优先级： == != === !==
  // 7. 第七优先级： &&
  // 8. 第八优先级： ||
  // 9. 第九优先级： = += -= *= /= %=  

  var a = 200 === (10 + 10) * 10 > 1;
  // 200 === 20 * 10 > 1
  // 200 === 200 > 1
  // 200 === true;
  // false
```

# js基础day02

## 01-分支结构-if-else

```js
  // 语法：
  // if (条件表达式1) {
  //   当条件表达式1的结果是 true 时执行的代码
  // }
  // else if (条件表达式2) {
  //   当条件表达式2的结果是 true 时执行的代码
  // }
  // else if (条件表达式3) {
  //   //当条件表达式3的结果是 true 时执行的代码
  // }
  // // 特点1：上面的分支都是false, 执行else的分支：
  // // 特点2：else 分支不是必须的；else只能出现一次；
  // else {
  //    多个条件表达式的结果都是 false 的时候执行的代码
  // }
```

## 02-分支结构-switch-case

```js
  // 语法：
  // 特点：与固定值进行比较；
  // key:传入的数据；
  // value：其中一个固定值，数据要和固定值进行比较：数据===固定值；
  // 注意：
  //    :不能省略，
  //    break当前情况的结束；
  //    default：所有情况都不满足时，执行default；
  // switch (key) {
  //   case value:
  //     // JS代码；
  //     break;
  //   default:
  //     break;
  // }
```

## 03-分支结构-三元表达式

```js
  // 三元表达式：if else 简写  有返回值
  // 表达式1 ? 表达式2 : 表达式3;
  // 过程：
  // 如果表达式1 执行结果为true。执行表达式2，把表达式2的结果作为整个三元表达式的结果进行返回；
  max = a > b ? a : b;
  
三元表达式只要前面的条件成立，就会指向？后面的语句，可以是一条也可以是多条； 多条的话使用逗号分隔就可以了
```

## 04-循环结构-while

```
  // 作用：有重复的思想在里面，有规律的变化，循环：重复；
  // 语法：
  // condition：条件表达式，返回Boolean值；不是Boolean值，隐式转化为Boolean；
  // while (表达式) {
  //   循环体；
  //   alert("这是个病毒");
  // }
  //条件表达式为true，执行循环体
   
  var num = 1;
  while (num <= 10) {
    sum = sum + num;
    num++;
  }
  
  var num = 1;
  while (num <= 100) {
    if (num % 2 == 0) {
      console.log("偶数是" + num);
    }
    num++;
  }
```

## 05-循环结构-for

```js
  // 先执行 初始化表达式 var num = 1; 在整个循环里面，只执行一次；
  // 进入 条件表达式: num<=100;
  //   返回true ,执行循环体；
  //   返回fasle ,终止循环；
  // 执行完循环体以后，才执行自增表达式: num++;
for (var num = 1; num <= 3; num++) {
    // 循环体
    console.log(num);
  }
  // 特点：有执行第4次，判断条件为false,循环结束；

  //打印金字塔
   for (var a = 1; a <= 10; a++) {
      for (var b = 1; b <= a; b++) {
         document.write("o");
       }
    // 换行
    document.write("</br>");
  }
```

## 06-循环结构-do-while循环及小结

```js
  // 条件表达式：位置上需要一个Boolean值，若不是Boolean，会隐式转化；
  // while (true) {
  //   alert(1);
  // }

// 补充:do-while
  do {
    // 循环体
    alert(1)
  } while (false);
  // 至少会执行一次；
```

- while、do-while 循环不易看出循环的次数，一般用于**未知次数的循环**
- for循环明显看出循环的次数，一般用于已知次数的循环；**使用最多是for；**
- 执行特点：
  - while、for循环可能一次循环都不会执行
  - do-while（了解） 循环至少执行一次；

##07-循环结构-break和continue

* break：终止当前循环
* continue：跳过本次循环

```
  // 例子：电梯一共有6层，现在我们要上电梯，我们的教室在3楼，电梯只要到3楼就可以了。
  // 1. 每一层都要停;
  // 2. 到了3层,终止循环;
  // for (var a = 1; a <= 6; a++) {
  //   console.log(a);
  //   // 到了3层
  //   if (a == 3) {
  //     // 终止 当前 for 循环整体；
  //     break;
  //   }
  // }

  // 例子：电梯一共有6层，除了3楼没人下去，其他楼层都有人下去(3楼不停，其他楼层都要停)
  // 1. 每层都停；
  // 2. 到了这一次for循环，不需要执行；
  for (var a = 1; a <= 6; a++) {
    if (a == 3) {
      // 作用：跳过 当次 循环，意味着写在 continue 本次后面的代码，都不会执行了；
      // continue：本次不用执行了，继续往下一次执行；
      continue;
    }
    console.log(a);
  }
  
break必须在switch语句或者是在for循环中使用
break可以在for循环的循环体中使用,可以在一个循环中多次使用break
switch语句中 经常会出现多个break
break可以在循环中搭配if一起使用，但是不能单独使用
```

## 08-输出0-100之间的所有质数

```js
// 1,2 都为质数
for (var a = 3; a <= 100; a++) {
        for (var n = 2; n <= a; n++) {
            if (a % n == 0) {
                break;
            }
        }
 //a == n为true，意味着n已经全部循环完毕，没有中断过，没有一次被整除      
        if (a == n) {
            console.log(a)
        }
    }

for (var a = 3; a <= 100; a++) {
    var is_zhishu=true;
        for (var n = 2; n <a; n++) {
            if (a % n == 0) {
                is_zhishu = false;
            }
        }
        if (is_zhishu) {
            console.log(a)
        }
    }
```

# js基础day03

## 01-数组

```js
//声明数组
// 索引：位置，数字表示，从0开始；
//1.字面量声明  
  var arr = [];
  arr[0] = 97;
  var arr_1 = [90, 50, "abc", true];
//2.构造函数声明
  var arr = new Array();

// var arr = [10, 10, 10]
// var arr_1 = new Array(10, 10, 10);

// 单个值：传入，构造函数会把这个数据当作数据个数；
// var arr = [10];
// var arr_1 = new Array(10);

// 第一个位置上数据被替换，arr[0]可以当作变量使用；
   arr[0] = 200;
//数组长度
   arr.length  
//最大索引总是比长度少 1 ；因为索引是从0（第一位）开始

//遍历数组
 for (var i = 0; i < arr.length; i++) {
     sum += arr[i];
  }

// 2.清空数组
    arr.length = 0;
```

## 02-转义字符-换行

```
换行：\n；  转译字符：把特殊字符 " ' \  \n
```

## 03-split()把字符串转换成数组

```js
var str = "1,2,3,4";
// 传入：分隔符；把字符串中和分隔符一样的地方，切割开；
// 返回：一个数组
var arr = str.split(",");
//隐式转换，把字符串转换为数字
arr[i] = arr[i] * 1;
```

## 04-new Date()时间对象

```js
  var date = new Date();    时间对象
  // 语法：date.方法名();  必须跟着小括号

  // 返回：年份
  var year = date.getFullYear();

  // 返回：月份：从0,开始  0-11
  var month = date.getMonth() + 1;
  if (month < 10) {
    month = "0" + month;
  }
 
  // 返回：日期：
  var riqi = date.getDate();
  if (riqi < 10) {
    riqi = "0" + riqi;
  }

  // 返回：星期
  // var day = date.getDay();  
 
  // 返回：时
  var hour = date.getHours();
  if (hour < 10) {
    hour = "0" + hour;
  }
 
  // 返回：分
  var minute = date.getMinutes();
  if (minute < 10) {
    minute = "0" + minute;
  }

  // 返回：秒
  var second = date.getSeconds();
  // 单位数：补位双位数
  if (second < 10) {
    second = "0" + second;
  }
```

## 05-ES6 语法：模板字符串:``

```js
  //反引号``
  // 字符串拼接
  // 2019-11-12 14:53:33
  // var str = year + "-" + month + "-" + riqi + " " + hour + ":" + minute + ":" + second;
  // ES6 语法：模板字符串；``  
  // 特点：`` 单双引号直接用法；变量放在${}里面
  var str = `${year}-${month}-${riqi} ${hour}:${minute}:${second}`;
```

## 06-随机数Math.random()

```js
  // 随机小数:  JS内置对象 Math
  // 返回：[0~1)随机小数；有可能会取值为0，有可能的概率很低；不包括1；
  var a = Math.random();
```

## 07-向下、向上取整

```js
  // Math.floor()  向下取整
  // floor:地板；
  // 传入:向下取整的数据；
  // 返回:向下取整后的值； 
  var a = Math.floor(a);   向下取整
  
  // ceil 天花板
  //Math.ceil();   向上取整；
   var b = Math.ceil(b);
```

## 08- 冒泡排序

```js
1.比较相邻的两个元素，如果前一个比后一个大，则交换位置。
2.第一轮的时候最后一个元素应该是最大的一个。
3.按照步骤1的方法进行相邻两个元素的比较，这时由于最后一个元素已经是最大的了，所以最后一个元素不用比较。    
    var arr = [74, 54, 23, 41];
    for (var i = 0; i < arr.length - 1; i++) {             //需要比较arr.length-1次
        for (var j = 0; j < arr.length - 1 - i; j++) {     //大的数值放在后面，每次前几个数值比较
            if (arr[j] > arr[j + 1]) {
                var key = arr[j];
                arr[j] = arr[j + 1];
                arr[j + 1] = key;
            }
        }
    }
```
# js基础day04

## 01-函数

```js
  // 作用：函数将重复出现的代码封装起来；在需要的地方进行调用（复用）
  // function:声明函数的关键字 
  function fn() {
    // 封装的代码；不会自己调用；
    
  }
  // 调用语法：函数名();
  fn();
```

## 02-函数的形参、实参

```js
 // 形参：内部定义的这个变量，只能在内部使用；外面不能使用；和外面没有任何关系;
 // 实参：外部调用函数的时候，传入真实数据，实参；把真实数据赋值了一份给形参；
 function sum(n, m) {
    var num = 0;
    for (var i = n; i <= m; i++) {
      num += i;
    }
    // 返回的是数据
    return num;
  }
  var num =sum(10,20);
  
  // 函数定义时有形参，调用时不传入参数，没有实参传入，JS内置给赋值为undefined
  // 形参的个数可以多于实参的个数
  // function fn(a) {
  //   console.log(a);
  // }
  // fn(); // 输出undefined
```

## 03-函数返回值return

```js
  // 语法：返回值 return；
  // 作用：把内部运算结果，返回给到外面；
  function fn(a) {
    a = a + 10;
    return a;
  }
  // 外面：需要找个变量接受
  var b = fn(10);
  
//  1. 函数返回值，把内部的值进行返回，返回到外面；
//  2. 只要函数内部出现了return，函数内return下面的代码(函数内)不再执行；
//  3. 如果return 后面没有任何数据（变量）,默认返回undefined；
//  4. 如果连return都没有，函数就没有返回值，执行函数，默认返回undefined；
```

## 04-函数参数-arguments

```js
  // arguments：解决参数个数不确定；
  // 函数内部（里面）的变量；只能在函数内部使用；
  // 特点：JS内置的变量，不需要我们声明，也不需要写在小括号内；
  // 语法：arguments把参数传入值，都接收到，生成一个 伪数组；
  //      伪数组：和数组很像，但不是数组。伪数组有下标，有长度，可遍历；
  // function fn() {
  //   console.log(arguments);
  // }

  // fn(1, 10, 20, 66, 89, 88, 99);
  // Arguments(7) [1, 10, 20, 66, 89, 88, 99, callee: ƒ, Symbol(Symbol.iterator): ƒ]
```

## 05-函数表达式

```js
  // 函数表达式 是另外一种声明函数的方式
  // 必须先声明后调用，否则程序报错。
  // var fn_2 = function() {
  //   console.log(1);
  // }
  // fn_2();
```

## 06-匿名函数

```js
  // 匿名函数：函数没有名字；
  // 特点：不能单独使用：
  // function () {
  //   console.log(1);
  // } 报错: Uncaught SyntaxError: Unexpected token 

  // 使用1:函数表达式;
  // var fn_2 = function() {
  //   console.log(1);
  // };
  
  // 使用2:自调用(自执行)函数；
  // (function() {
  //   console.log(1);
  // })();
```

## 07-回调函数

```js
// 参数：传入的是函数，这个被传入的函数（作为参数）就叫回调函数；
function demo() {
    console.log("1");
  }
  fn(demo);
```

## 08-js-作用域

>在ES6之前，作用域可以分为全局作用域和局部作用域,ES6才出现块级作用域。

```js
  // 全局作用域：在script 里面声明的变量 函数 function 作用域范围：全局作用域；
  // 规则：全局声明的变量，在JS代码 任何位置都可以使用；包括局部作用域（函数内部）；
  // 全局变量可以在函数内部使用；
  // var a = 1;
  // function fn() {
  //   console.log(a);
  // }
  // fn();
  
  // 局部作用域：函数内部的范围  function fn() { 局部作用域 } 
  // 局部变量：函数内部声明的变量；规则：只能在函数内部使用；在外面不能访问；
```

## 09-js-预解析

```js
 // 预解析，会把声明的变量和函数提升到你当前的作用域的最顶端，也叫变量提升和函数提升；
 // 预解析规则：遇到一个新的作用域，声明：var 变量；function fn(){}，提升到当前作用域最顶端；
 
 // 全局作用域
  console.log(a);    ---->undefined
  var a = 1;
 //模拟内存的解析过程如下：
  var a;
  console.log(a); // undefined;
  a = 1;
```

## 10-js-作用域链

* 局部变量的寻找规则：先在当前自己的作用域的中找有没有声明的变量，如果没有往上层作用域找，如果上层作用域也没有该变量，就报错；

# js基础day05

## 01-对象创建

* 对象：属性和**方法**的集合体；

```js
  // 1.字面量
  var obj = {};
  console.log(obj);

  // 2.构造函数
  var obj_1 = new Object();
  console.log(obj_1);
```

## 02-对象添加属性

```js
  // ----------------------------点方式
  // 对象.属性名 = 属性值
  // obj.name = "狗蛋";

  // 对象.方法名 = 匿名函数；
  // obj.say = function() {
  //   console.log("1");
  // }

  // ----------------------------初始化的时候，进行属性和方法的添加
  // var obj = {
  //   name: "zhangsan",
  //   age: 16,
  //   say: function() {
  //     console.log(1);
  //   },
  // };
  // console.log(obj);
  // 格式：名字：属性值 或者 匿名函数；客观来说，属性和方法名都是名字；
  // 注意:每组后面必须有逗号，最后一组可以不加

  // ---------------------------键值对 [] 方式
  // 键：属性名或者方法名；
  // 值：属性值或匿名函数；

  var obj = {};
  obj["name"] = "狗蛋";
  obj["say"] = function() {
    console.log(1);
  };
```

- 注意：

```js
  // 键值对和点方式区别：[属性名和方法名 必须是字符串]
  // var a = "name";
  // a暂时变量，变量后面的值 属性名；
  // obj[a] = "狗蛋";

  // 有个属性名叫a
  // obj.a = "狗蛋a"
```

## 03-对象-获取及遍历属性

```js
  // -------------------------------------------点方式获取  设置属性
  var obj = {
    a: 1,
    b: 2,
  };

  // 获取一个对象上没有的属性名后的值，返回的undefined；
  console.log(obj.key);      ----->undefined

  // console.log(obj.a);     ----->1
  // obj.a = "abc";          重新设置属性值
  // console.log(obj.a);     ----->"abc"

  // -------------------------------------------键值对 [] 方式
  // console.log(obj["a"]);
  // obj["a"] = "abc";
  // console.log(obj);
  
  // -------------------------------------------对象遍历 for in
  // 语法：遍历就是循环；
  // key：代表每一次循环的 名字（属性名和方法名）
  // key:"a"
  // key:"b"
  // object: 遍历循环的对象 obj
  for (var key in obj) {
    // obj.key 从obj上找.key,返回是undefined；
    console.log(key, obj[key]);
  }

  // 遍历数组
  var arr = [1, 2];
  for (var key = 0; key < arr.length; key++) {
    console.log(key, arr[key]);
  }
```

## 04-对象补充

```js
  // 设计者:设计一个自己对象;
  // 语法:形式没有绝对;混合起来使用
  // var obj = {
  //   a: 1,
  //   b: 2,
  // };

  // obj.c = "abc";
  // obj["d"] = "-----";
  // console.log(obj);
  
  // 一直使用：
  // Math:内置对象
  // console.log(Math);
  
  // var Console = {
  //   log: function() {
  //     console.log("hello");
  //   }
  // }
  // Console.log();

  // console 内置对象
  // console.log(console);
```

## 05-小娜对象化

```js
// 设计对象；
var Na = {};
// 设置
Na.getHe = function(str) {
    str = str.split("-");
    var he = 0;
    for (var i = 0; i < str.length; i++) {
        str[i] = 1 * str[i];
        he += str[i];
    }
    return he;
};
Na.getHe();


  // 注意问题：
  // 1. info == q  : 报错，把q认为变量；
  // 2. info == 1  ：谁隐式转化：info :"1"------>1;
  // 3. info = "1" :赋值表达值，返回值 "1" ------->true;
  // 4. 求和 var he; 输出NaN ： undefined + 10；---->NaN+10
  
  // 5. 封装函数:是否设置形参？
  // 设置形参：str作为内部变量；值从哪来？实参传入；
  // function getHe(str) {
  //   str = str.split("-");
  //   var he = 0;
  //   for (var i = 0; i < str.length; i++) {
  //     str[i] = 1 * str[i];   // 隐式转换，把string类型转换为number类型
  //     he += str[i];
  //   }
  //   return he;
  // }
  
  // 没有设置形参：str作为全局变量; 在函数内部把全局变量的值变了；
  // function getHe() {
  //   str = str.split("-");
  //   var he = 0;
  //   for (var i = 0; i < str.length; i++) {
  //     str[i] = 1 * str[i];    // 隐式转换，把string类型转换为number类型
  //     he += str[i];
  //   }
  //   return he;
  // }
```

## 06-Math的n-m的随机整数

* 给已经存在的对象上，新增一个方法；
  * 1.实际过程
  * 2.封装函数:参数？返回值？
  * 3.设置对象上  对象.方法名 = function(){}

```js
  // 需求 : Math上拓展方法，用途：范围 n~m 随机整数  n<m
  // 1.实际过程：0-10;  10个数,中间间隔11个数
  
  // 扩大：10-0+1
  // var a = Math.random();
  // a = a * (m - n + 1);
  // 缩小：向下取整；
  // a = Math.floor(a);

  // 0-10 范围 向后挪动 n个；
  // a = a + n;
  
  // 2.函数封装：
  // 0-10
  // n-m
  // function getRandomInt(n, m) {
  //   var a = Math.random();
  //   a = a * (m - n + 1);
  //   缩小：向下取整；
  //   a = Math.floor(a);
  //   a = a + n;
  //   return a;
  // }
  
  //3.设置到对象上
  Math.getRandomInt = function(n, m) {
    var a = Math.random();
    a = a * (m - n + 1);
    // 缩小：向下取整；
    a = Math.floor(a);
    a = a + n;
    return a;
  };

  // 根据业务，丰富对象；
  var a = Math.getRandomInt(60, 62);
```

## 07-数组的拼接concat()

```js
  // 数组.concat();
  // 传入：拼接的数据。
  // 返回：新数组；
  
  // var arr = [1, 2];
  // 传入1个数据
  // var Arr = arr.concat("abc");
  // console.log(arr, Arr);

  // 传入多个数据
  // var Arr = arr.concat("a", "b", "c", "d", "e", "f");
  // console.log(arr, Arr);

  // 传入1个数组
  // var Arr = arr.concat(["aa", "bb"]);
  // console.log(arr, Arr);

  // 传入多个数组
  // var Arr = arr.concat(["aa", "bb"], [77, 88]);
  // console.log(arr, Arr);
```

## 08-js简单类型与复杂类型

- 简单数据类型：

<img src="images/jiandan.png"/>

- 复杂数据类型：

<img src="images/fuza.png"/>

```js
 function fn(b) {
        // 局部变量b 
        b = 2;
    }
  var a = 1;
  fn(a);
  // b = a;
  console.log(a);   ----->1
  --------------------------------------------------------------
   var a = 10;
   var b = a;
   b = b + 10;
   console.log(a, b);  ----->10  20
   --------------------------------------------------------------
   var obj_1 = {
        a: 10
    };
    // 赋值，自己运算把原来的数据影响
    var obj_2 = obj_1;
    obj_2.a = 20;
    console.log(obj_1.a);   ----->20
    --------------------------------------------------------------
    //复制数据类型
    function f2(o) {
        o.name = '翠花';
    }
    var a = {
        name: '狗蛋'
    }
    f2(a);
    // o = a; // a 给了 o 地址；
    // 最终a的name属性是多少？  翠花
    console.log(a.name);    ---->翠花
    ----------------------------------------------------------------
    var a = 10;
    var b = 10;
    // 类型相同,比值：格子里存的值；
    console.log(a == b);    ------>true

    var c = {};
    var d = {};
    //类型相同,比值：格子里存的值；地址不同，复杂数据类型，存放在堆
    console.log(c == d);    ------->false
```

# js基础day06

## 1.Math

### 1.1Math.random()随机数

```js
// var a = Math.random();
// a *= 256;
```

### 1.2Math.floor()向下取整

```js
// var b = Math.random();
// b *= 256;
// b = Math.floor(b);
```

###1.3Math.ceil()向上取整

```js
// var b = Math.random();
// b *= 256;
// b = Math.ceil(b);
```

### 1.4Math.round()四舍五入

 ```js
// var a = 3.999999;
// 四舍五入
// var res = Math.round(a);
 ```

### 1.5Math.abs()取绝对值

```js
// var b = -5.33;  
// 返回绝对值，求正；不是取整数；
// var res_b = Math.abs(b);
```

### 1.6Math.max()取最大值

```js
  // 求一堆数中最大值；
  // var c = Math.max(8, 4, 5, 7, 3, 99, 599, 299, 399);
  // console.log(c);

  // 需求：函数输入一些数字，求最大值；
  // var d = MAX(8, 4, 5, 7, 3, 99, 599, 299, 399);
  Math.MAX = function() {
    // 伪数组：有长度，有下标，可遍历
    // console.log(arguments);
    var max = arguments[0];
    for (var i = 0; i < arguments.length; i++) {
      if (arguments[i] > max) {
        max = arguments[i];
      }
    }
    return max;
  };
  var c = Math.MAX(8, 4, 5, 7, 3, 99, 599, 299, 399);
  console.log(c);
```

### 1.7Math.min()取最小值

```js
  // 求一堆数中最小值；
  // var c = Math.min(8, 4, 5, 7, 3, 99, 599, 299, 399);
  // console.log(c);
```

## 2.Date

###2.1获取时间年月日时分秒

```js
var date = new Date(); // 得到的是当前时间的日期对象
```

- 获取年月日时分秒

```js
console.log(date.getFullYear()); // 年份
console.log(date.getMonth());    // 月份，从0开始

// 英语：日期date   day某天
console.log(date.getDate());  //日期
console.log(date.getDay())    //星期
console.log(date.getHours()); // 小时，0-23
console.log(date.getMinutes()); // 分钟 ， 0-59
console.log(date.getSeconds()); // 秒数 ， 0-59
console.log(date.getMilliseconds()); // 毫秒 0-999 ， 1秒 = 1000毫秒
```

- 创建一个**指定日期**的对象

```js
// 给一个日期格式字符串
var date = new Date('2019-01-01');

// 特定的格式1: 输入一个字符串
// var date = new Date("2018-08-23 12:00:12");
// month从0开始
// var month = date.getMonth() + 1;
// console.log(month);

// 分别传入年月日时分秒。注意传入的月份是从0开始算的
var date = new Date(2019,0,1,12,33,12);

// 特定的格式2:传入是数字；
// var date = new Date(2018, 7, 23, 12, 00, 12);
// var month = date.getMonth() + 1;
// console.log(month);
```

###2.2获取时间戳

- 获取从1970年1月1日到现在的总毫秒数，**常说的时间戳**

```js
  // 比较："2018-08-23 12:00:12"   "2019-11-17 12:00:12"
  // 哪个靠未来些？

  // var date = new Date(); // 当前时间对象；
  // 返回：数字，当前时间点距离 1970年1月1日 毫秒数，时间戳；
  // console.log(date.valueOf());
  // console.log(date.getTime());
  // console.log(1 * date);
  // console.log(Date.now());

  // 生成ID：identification 身份证号：唯一
  // 场景1：JS测试用生成ID：
  // var id = Date.now() * Math.random();

  // 场景2：比较时间字符串的大小；
  var date_1 = new Date("2018-08-23 12:00:12");    //创建一个指定日期的对象
  var time_1 = date_1.valueOf();
  console.log(time_1);

  var date_2 = new Date("2019-11-17 12:00:12");
  var time_2 = date_2.valueOf();
  console.log(time_2);

  if (time_2 > time_1) {
    console.log("2019-11-17 12:00:12");
  } else {
    console.log("2018-08-23 12:00:12");
  }
```

## 3.Array数组方法

### 3.1 push从后面添加到数组

```js
  // var arr = [1, 2, 3, 4, 5, 6];
  // 作用：把一个元素或多个元素，从数组后面添加到数组里面；
  // 参数：添加的数据
  // 返回：添加后的数组的长度；
  var l = arr.push(8, "abc");
  console.log(arr, l);
```

### 3.2 pop从后面删除一个元素

```js
  // 作用：从数组的后面删除一个元素
  // 参数：无；
  // 返回：被删除的元素；
  var res = arr.pop();
  console.log(arr, res);
```

###3.3 unshift从前面添加数据 

```js
  // 作用：从数组前面添加数据（一个或者多个）
  // 参数：一个或者多个；
  // 返回：添加后的数组的长度
  var l = arr.unshift("a", "b");
  console.log(arr, l);
```

###3.4 shift从前面删除第一个元素 

```js
  // 参数：无；
  // 返回：被删除的元素；
  var res = arr.shift();
  console.log(arr, res);
```

###3.5 splice可进行数组任何位置的增删改

```js
  // var arr = ['a', 'b', 'c', 'd', 'e'];
  // 删除：
  // 参数：第一个参数是开始的下标，第二个参数：要移除的个数；
  // 返回：被删除元素的数组；
  // var res = arr.splice(3, 1);
  // console.log(arr);----->['a', 'b', 'c',  'e']     删除元素对原数组进行操作
  // console.log(res);----->['d']
  
  // 添加：
  // 参数：第一个参数：开始的下标；第二个参数：删除的个数；后面参数：要添加的数据，从开始的下标位置添加；
  // 返回：没有删除，返回[]
  // var res = arr.splice(3, 0, "AA", 18);
  // console.log(arr); ---->["a", "b", "c", "AA", 18, "d", "e"]
  // console.log(res); ---->[]
  
  // 修改：
  // 参数：第一个参数：开始的下标；第二个参数：删除的个数；后面参数：要添加替换的数据，从开始的下标位置；
  // 返回：被替换的数据的数组；
  // var res = arr.splice(3, 1, "HH");
  // console.log(arr); ----->["a", "b", "c", "HH", "e"]
  // console.log(res); ----->["d"]
```

### 3.6 数组与字符串互转

```js
  var str = '刘备|关羽|张飞';
  console.log(str);

  // 字符串---->数组：
  // 参数：分隔符
  // 返回：数组；
  var arr = str.split("|");
  console.log(arr);

  // 数组----->字符串
  // 参数:分隔符；
  // 返回：字符串；
  var str_1 = arr.join("*_*");
  console.log(str_1);
```

### 3.7 indexOf数组中查找元素

```js
  // ---------------------------------------------indexOf  【!!!】
  // 参数：被查找的元素
  // 返回：被查找的元素的下标索引（没有找到返回-1）

  // 场景：查找数组中有没有我们需要的数据；
  var arr = [1, 10, 20];
  var index = arr.indexOf("a");
  console.log(index);     ----->-1

  // ----------------------------------------------findIndex
  // 参数：函数（被传入的函数，回调函数）
  //      格式要求：
  //          item  回调函数，代表每一次遍历的数据
  //          return 判断条件(自己写)
  // 返回：满足条件的第一个元素的下标，若没有，返回-1；
  var index = arr.findIndex(function(item) {
     return item === 20;
  });
  // console.log(index);
```

###3.8 遍历数组  

#### 3.8.1 forEach

```js
  var arr = [0, 10, 10, 10, 20];
  // forEach:  
  // 作用：遍历数组
  // 参数：函数（函数）格式要求：
  //      函数参数：item,index,arr
  //      item：每个数据
  //      index：下标；
  //      arr：当前遍历的数组；

  // var max = arr[1];
  // arr.forEach(function(item, index, arr) {
  //    console.log(item, index, arr);
  //   if (item > max) {
  //     max = item;
  //   }
  // });
  // console.log(max);
```

#### 3.8.2 filter

```js
  // filter  
  // 作用：对当前数组一定的过滤；
  // 参数：函数（函数）格式要求：
  //      函数参数：item,index,arr
  //      item：每个数据
  //      index：下标；
  //      arr：当前遍历的数组；
  //      return 过滤条件; 返回是true，把当前满足条件的item 放入新的数组中
  // 返回:返回过滤后的新数组;

  var arr_1 = arr.filter(function(item, index, arr) {
    // 过滤条件; 返回是true，把当前满足条件的item 放入新的数组中
    return item == 10;
  });
  console.log(arr, arr_1);
```

###3.9 concat 数组拼接

```js
  // concat 
  // 作用：数组的拼接
  // 参数：要拼接的数据（单个数据、多个数据、单个数组，多个数组）
  // 返回：拼接后的 新数组；

  // var arr1 = [1, 2, 3];
  // var arr2 = [4, 5, 6];
  // var arr3 = [7, 8, 9];
  // var res = arr1.concat(arr2, arr3);
  // console.log(arr1, res);
```

### 3.10 slice截取数组

```js
  // slice:
  // 作用：截取数组
  // 参数：
  // 返回：被截取的新数组；
  var arr = ['a', 'b', 'c', 'd', 'e'];
  
  // 参数:2个参数。第一个参数从哪个下标开始（包括），截取到哪个下标结束(不包括),
  // var res = arr.slice(1, 4);
  // console.log(arr, res);

  // 参数：1个参数，从哪个下标开始，一直到结尾都要截取
  // var arr_1 = arr.slice(1);
  // console.log(arr_1);

  // 参数：没有参数，全部截取，复制数组；
  // var res = arr.slice();

  // 数组：复杂数据类型；
  // console.log(res, arr);
  // console.log(res == arr);   ---->false
```

### 3.11 数组复制

```js
  // 需求：复制过来的新数据和原来的数据没有任何关系；
  var arr = ["a", "b", "c", "d"];

  // var arr_1 = arr;
  // arr_1[0] = "abc";
  // console.log(arr);   ---->arr = ["abc", "b", "c", "d"];

  // -----------------------------------------------------------for
  // var arr_1 = [];
  // for (var i = 0; i < arr.length; i++) {
  //   arr_1[i] = arr[i]
  // }
  // arr_1[0] = 10
  // console.log(arr_1, arr);
  
  // -----------------------------------------------------------forEach
  // arr：可选参数
  // var new_arr = [];
  // arr.forEach(function(item, index) {
  //   new_arr.push(item);
  // });
  // new_arr[0] = "abc";
  // console.log(new_arr, arr);

  // ------------------------------------------------------------filter
  // 作用：满足过滤条件的元素，组成1个新数组返回；
  // var new_arr = arr.filter(function(item, index, arr) {
  //   过滤条件？
  //   return arr.indexOf(item) != -1;
  // });
  // // arr.indexOf(item) != -1条件：过滤条件结果为true , 把当前的item组成到新的数组里；
  // new_arr[0] = "abc";
  // console.log(new_arr, arr);
  
  // ------------------------------------------------------------拼接和截取
  // 参数：不传入
  // 返回：新数组（和arr一样）
  // var new_arr = arr.concat();
  // new_arr[0] = "---------------------";
  // console.log(new_arr, arr);

  // 参数：不传入
  // 返回：全部截取，新数组（和arr一样）
  // var new_arr = arr.slice();
  // new_arr[0] = "-----------++----------";
  // console.log(new_arr, arr);

  // ------------------------------------------------------------与字符串的互转
  // var str = arr.join("-");
  // console.log(str);
  // var new_arr = str.split("-"); // 新数组
  // new_arr[0] = "-----------++----------";
  // console.log(new_arr, arr);
```

###3.12 数组排序 sort()

```js
sort() 方法用于对数组的元素进行排序。

 var arr = [11,52,74,85,96,15];
 arr.sort(sortby)
 sortby	可选。规定排序顺序。必须是函数。
 返回值:对数组的引用。
 
 注意:数组在原数组上进行排序，不生成副本。

如果调用该方法时没有使用参数，将按字母顺序对数组中的元素进行排序，说得更精确点，是按照字符编码的顺序进行排序。要实现这一点，首先应把数组的元素都转换成字符串（如有必要），以便进行比较。

如果想按照其他标准进行排序，就需要提供比较函数，该函数要比较两个值，然后返回一个用于说明这两个值的相对顺序的数字。比较函数应该具有两个参数 a 和 b，其返回值如下：

若 a 小于 b，在排序后的数组中 a 应该出现在 b 之前，则返回一个小于 0 的值。
若 a 等于 b，则返回 0。
若 a 大于 b，则返回一个大于 0 的值。
```

### 3.13数组倒序reverse()

```js
reverse() 方法用于颠倒数组中元素的顺序。

var arr = [11,52,74,85,96,15];
arr.reverse();

注意：该方法会改变原来的数组，而不会创建新的数组。
```

## 4.对象复制

 ```js
// 需求：对象如何复制？
  var obj = {
    a: 1,
    b: "abc"
  };

  // var new_obj = obj;
  // new_obj.a = 2;
  // console.log(obj.a);   ------>2

  // 遍历对象
  var new_obj = {};
  for (var key in obj) {
    new_obj[key] = obj[key]
  }

  // 浅拷贝,深拷贝：JS高级，第三天；
  // var arr_1 = [];
  // for (var key = 0; key < arr.length; key++) {
  //   arr_1[key] = arr[key]
  // }
 ```

## 5.String字符串

### 5.1字符串不可变

- 字符串不可变：
  - 旧的字符串赋值在一个变量上，给变量重新赋值新的字符串（完全新的字符串，或者拼接后字符串），旧的字符串不是被覆盖；**在内存的游离状态；**
  - **所以尽量避免大量使用字符串的拼接；这个算性能优化的一点；**

### 5.2  indexOf()查找字符

```js
  // indexOf
  // 作用：查询字符所在字符串的位置；
  // 参数：查询字符
  // 返回：下标，若没有查询到，返回-1；
  // var str = '我爱中华人民共和国';
  // var key = str.indexOf("通州");
  // console.log(key);

  // 场景：查询是否有敏感字；
```

- lastIndexOf  用法和indexOf一样，只不过是从后面开始找，【了解】；
- charAt：【了解】

```js
// 这个方法用于获取字符串中位于指定位置的字符
var str = '我爱中华人民共和国';
console.log(str.charAt(2));    ----->中
```

- charCodeAt ：【了解】

```js
// 这个方法用于获取字符串中位于指定位置的字符的ASCII码
var str = 'abcdef'
console.log(str.charCodeAt(0));
```

###5.3 split()-字符串转为数组

```js
  // 案例：解析地址`b.com?id=1&name=2`中的参数； JS高级   ajax
  // 地址：https://www.baidu.com/s?wd=a&rsv_spt=1  GET请求
  // 解析：id=1&name=2  变成对象  {id:1,name:2}

  var str = "b.com?id=1&name=2";
  var arr = str.split("?");
  // console.log(arr);   ---->["b.com", "id=1&name=2"]

  str = arr[1];
  // console.log(str);   ----->["id=1&name=2"]
  var arr_1 = str.split("&");
  // console.log(arr_1);  ["id=1", "name=2"]

  // 遍历：
  var obj = {};
  var one, key, val;
  for (var i = 0; i < arr_1.length; i++) {
    // 其中的一样被分隔为数组  ["id", "1"]
    one = arr_1[i].split("="); // 

    // 数组中第一项：对象中属性名  键
    key = one[0]; // id

    // 数组中第二项：对象中属性值  值
    val = one[1]; // "1"

    // 对象上设置 对象[属性名]
    obj[key] = val; // obj["id"] = "1";
  }

  console.log(obj);
```

###5.4 字符串拼接与截取

- 下面的方法都没有对原字符串进行操作，返回新的字符串；

```js
  // var str = "abcdefghjk";
  // ----------------------------------------------------------拼接concat 
  // 作用：可以与多个字符串进行拼接  
  // 参数：拼接的数据
  // 返回：拼接后的字符串；
  // var res = str.concat("--------", '88888');
  // console.log(str, res);

  // ----------------------------------------------------------截取substring
  // substring
  // 作用：截取字符串
  // 参数：第一个参数：截取开始的下标(包括);第二个参数：截取结束的下标(不包括)
  // 返回：截取出来的字符串
  // var res = str.substring(0, 3);
  // console.log(str, res);

  // -----------------------------------------------------------截取slice
  // 作用：截取字符串;
  // 参数：第一个参数：截取开始的下标(包括);第二个参数：截取结束的下标(不包括)
  // 返回：截取出来的字符串
  // var res = str.slice(0, 3);
  // console.log(str, res);

  // 特别：参数可以设置负数，遇见负数，内部（负数+字符串的长度--->值 下标）
  var str = "abcdefghjk";
  // var res = str.slice(-6, 7);   // -6 + 10
  // var res_1 = str.slice(4, 7);
  // console.log(res, res_1);

  // --------------------------------------------------------------截取substr
  // 作用：截取字符串
  // 参数：第一个参数，开始下标。第二个参数，截取的个数；
  // 返回：被截取新字符串，没有对原字符串修改；
  var res = str.substr(2, 3);
  console.log(res);
```
