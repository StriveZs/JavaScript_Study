---
title: JavaScript基本概念

categories:
  - JavaScript

tags:
  - JavaScript
  - LearningNote
---
JavaScript学习笔记。  Github同步链接: [click here](https://github.com/zs670980918/JavaScript_Study) 

# 基本概念
## 区分大小写
JavaScript是区分大小写的，test和TEST是两个不同的变量。  

## 标识符
表示：是指变量、函数、属性的名字，或者函数的参数。  
标识符的规则：
- 第一个字符必须是一个字母、下划线(_)或一个美元符号($)
- 其他字母可以使字母、下划线、美元符号或数字

## 注释
- 单行注释使用的：//
- 多行注释使用的是: 

```
/*
*
*
*/
```

## 语句
JavaScript的语句以一个分号结尾；如果省略分号，则有解析器确定语句的结尾。建议不要省略分号。

## 关键字和保留字
Javascript 的保留关键字不可以用作变量、标签或者函数名。有些保留关键字是作为 Javascript 以后扩展使用。

![figure.1](https://gitee.com/zyp521/upload_image/raw/master/ehDkNW.png)

## 变量
定义变量要使用**var操作符**，var是一个操作符，后面跟变量:
```
var message;
```
上述代码中message是一个变量，它可以用来保存任何值，同样也支持直接初始化变量如下所示:
```
var message = "hello";
```
这样message就被赋予一个字符串值，可以和python一样直接修改变量的值，如下:
```
var message = "hello";
message = 1;
```
但是上述做法是不被推荐的，因为在修改变量值的同时也修改了变量的类型。虽然这种做法是有效的，但是不推荐。  
同样var操作符定义的变量将会被定义为该变量所在的作用域中的局部变量，也就是说如果函数中定义一个var，则在函数退出之后var就会被销毁。  

如果省了var操作符直接定义一个变量的话，那么这个变量就变成了全局变量，这样在其他外部函数中同样可以调用这个变量。
```
function test(){
    var a = "1"; // 局部变量
    b = "2"; // 全局变量
}
test();
alter(b); // 仍然可以被调用
```

可以使用一条语句定义多个变量，只要下面这种形式，用逗号将变量分隔开即可(可以初始化，也可以不初始化)
```
var a="12",
    b="123",
    c;
```

## 数据类型
JavaScript中有五种基本数据类型：
- Undefined
- Null
- Boolean
- Number
- String

### typoef操作符
使用typeof操作符可以用来检查变量的类型。使用形式如下:
```
var message = "some things";
alter(typeof(message));
```
### Undefined类型
Undefined类型只有一个值，即特殊的undefined，在使用var声明变量但未对其加以初始化时，这个变量的值就是undefined。如果对于未初始化的变量，将它和undefined进行比较的话，他们是相等的。
```
var mess;
alter(mess == undefined); // true
```
未使用var声明的变量，使用typeof得到的类型也是undefined。

### Null类型
Null类型是第二个只有一个值的数据类型，这个特殊的值是Null，从逻辑角度来看，null值表示一个空对象指针，而这也正是使用typeof操作符检测null值时会返回object的原因，如下面例子：
```
var car = null;
alter(typeof(car)); // return object
```
如果定义的变量准则在将来用于保存对象，则最好将这个变量初始化为null而不是其他的值。这样就可以直接检测null值来确定这个变量是否已经保存了对象:
```
var car = null;
car = object; // 赋给一个对象
if (car != null){
    执行对象操作;
}
```
undefined是从null派生出来的，因此:
```
alter(undefined == null); //return true
```

### Boolean类型
Boolean类型叫做布尔类型，这个类型只有：true和false。true不一定等于1，而false也不一定等于0。true和false是区分大小写的，即True和False都不是Boolean值而只是标识符。  
在JavaScript中也存在强制类型转换:
```
var mess = "Hello";
var message = Boolean(message); // 将字符串强制转换成了Boolean
```

常用的转换规则:

数据类型 | 转换为true的值 | 转换为false的值
---|---|---
Boolean | true | false
String | 任何非空字符串 | 空字符串
Number | 任何非零数字值 | 0和NaN
Object | 任何对象 | null
Undefined | n/a | undefined

### Number类型
Number类型分成了整数和浮点数。下面是集中常用的格式:
```
- var intnum = 55; //整数
- var octvalnum = 070; //以0开头的八进制
- var hexnum = 0xA; //以0x开头的十六进制
```
在算数计算时，所有的八进制和十六进制最终会被转换成十进制数值。

#### 浮点数值
浮点数值：这种数值中必须包含一个小数点，并且小数点后面必须至少有一位数字，下面是几个例子:
```
var flaotnum1 = 1.1;
var floatnum2 = 0.1;
var floatnum3 = .3; // 有效，但是不推荐
```
如果小数点后面没有跟任何数字，那么这个数值就可以作为整数值来保存。同样JavaScript也支持科学计数法，例子:
```
var floatnum = 3.12e8; // 3.12 * 10^8
var floatnum1 = 3.12e-7; //3.12 * 10^(-7) 
```
浮点数值的最高精度是17位小数，这就导致了0.1+0.2的结果不是0.3，而是0.300000000000004.记住用永远不要测试某个特定的浮点数(存在舍入误差)。

#### 数值范围
JavaScript将能够表示的最小数保存在Number.MIN_VALUE中，这个数值为5e-324;将能够表示的最大数保存在Number.MAX_VALUE中，这个数值是1.7976931348623157e+308。  
如果在某次计算中超出了这个数值范围，则会自动被保存为Infinity值，为负的话则会自动被保存为-Infinity。
```
var maxNum = Number.MAX_VALUE; // 最大数值
var minNum = Number.MIN_VALUE; // 最小数值
```
想要确定一个数值是不是有穷的(介于最小和最大的数值之间)，可使用isFinite()函数，如果位于则会返回true。

#### NaN
NaN的意思是非数值，它是一个特殊的数值，这个数值用于表示一个本来要返回数值的操作未返回数值的情况。在JavaScript中任何数值除以0都会返回NaN，不会影响代码的执行，而在其他语言中则会报错。    
**任何设计NaN的操作都会NaN**，NaN与任何值都必须相等，包括她自己本身。
```
alter(NaN == NaN); //false.
```
JavaScript定义了isNaN()函数，这个函数接受一个参数，该参数可以是任何类型，这个函数可以帮我们确定这个参数是否是NaN，如果是的话，则返回true，如果不是则返回false。
```
alter(isNaN(NaN)); // true
alter(isNaN(10)); // false
```

#### 数值转换
有3个函数可以把非数值转换为数值，分别为: Number()、parseInt()和parseFloat()。
- Number()：可以将任何类型转换为数值，转换规则如下：
  - 如果是Boolean类型，则true和false分别被转换为1和0
  - 如果是数值，只是简单的传入和传出
  - 如果是null，则返回0
  - 如果是undefined，返回NaN
  - 如果是字符串，则遵循以下规则：
    - 只包含数字，则将其转换为十进制数
    - 如果包含有效浮点格式，如"1.1"，则将其转换为对应的浮点数值
    - 如果包含有效地八进制/十六进制格式，则将其转换为对应的十进制整数值
    - 如果字符串是空的，则将其转换为0
    - 如果字符串中包含除上述格式之外的字符，则将其转换为NaN
  - 如果是对象，则调用对象的valueOf()方法，然后依照前面的规则转换返回值，如果返回结果是NaN，则调用对象的toString()方法，然后再依照前面的规则转换返回的字符串值。
- parseInt()：只能将字符串转换为整数，parseInt存在第二个参数，转换时使用的基数，如果为16则按照16进制的规则转换，其他进制同理，例子如下
```
var num1 = parseInt("10",2); // 按二进制解析
var num2 = parseInt("10",8); // 按八进制解析
var num2 = parseInt("10",10); // 按十进制解析
var num2 = parseInt("10",16); // 按十六进制解析
```
- parseFloat()：只能将字符串转换为浮点数

### String 类型
String类型用于表示由零或者多个16位Unicode字符组成的字符序列，即字符串。字符串可以由双引号"或单引号表示'，例如:
```
var firstName = "Hello";
var latsName = "World";
```
上述两种表示方式是等价的，和PHP不同。

#### 字符字面量
String数据类型包含一些特殊的字符字面量，也叫做转义序列，用于表示非打印字符，或者其他用于的字符。如下表所示:
字面量 | 含义
---|---
\n | 换行
\t | 制表
\b | 空格
\r | 回车
\f | 进纸
\\ | 斜杠
\' | 单引号，在字符串中使用
\" | 双引号，在字符串中使用

#### 字符串的特点
在JavaScript中字符串是不可变的，可就是字符串一旦创建，它们的值就不能改变，要改变某个变量保存的字符串，首先要销毁原来的字符串，然后在用另一个包含新值的字符串填充该变量。
```
var lang = "Java";
lang = lang + "Script";
```

#### 转换为字符串
要把一个值转换成一个字符串有两种方式，第一种格式使用几乎每个值都有的toString()方法，如下:
```
var age = 11;
var ageString = age.toString(); // 得到字符串"11"
```

Number、Boolean、Object和String都有toString()方法，但是null和undefined没有。  
多数情况下，调用toString()方法不必传递参数，但是也可以传递一个输出数值的基数，默认情况下是返回十进制格式的字符串，如果传递基数则可以返回二进制、八进制、十六进制等。
```
var num = 10;
alter(num.toString()); // 十进制
alter(num.toString(2)); // 二进制
alter(num.toString(8)); // 八进制
alter(num.toString(16)); // 十六进制
alter(num.toString(13)); // 十三进制
```

在不知道要转换的值是不是null或者undefined的情况下(即toString()可能会报错), 可以使用String()进行强制类型转换，它遵循如下规则：
- 如果值有toString()方法，则自动调用
- 如果是null，则返回“null”
- 如果值是undefined，则返回“undefined”

### Object类型
对象是一组数据和功能的集合，对象可以通过执行new操作符后跟要创建的对象类型的名称来创建，如下:
```
var object1 = new Car(); //创建一个Car对象
```
Object类型所具有的的任何书型盒方法也存在于更具体的对象中。  
Object的每个实例都具有下列属性和方法:
- Constructor：保存者用于创建对象的函数
- hasOwnProperty(propertyName)：用于检查给定的属性propertyName在当前对象示例中是否存在，作为参数的属性名propertyName必须以字符串形式指定，比如o.hasOwnProperty("bane")
- isPrototypeOf(object)：用于检测传入的对象是否是另一个对象的原型
- propertyIsEnumerable(propertyName)：用于检查给定的属性是否能够使用for-in语句来枚举，propertyName必须是字符串
- toLocaleString():返回对象的字符串表示, 该字符串与执行环境的地区对应
- toString(): 返回对象的字符串表示
- valueOf()：返回对象的字符串、数值或布尔值表示，通常与toString()方法的返回值相同。

## 操作符
### 一元操作符
只能操作的一个值的操作符叫做一元操作符

#### 递增和递减操作符
递增递减是直接借鉴C语言的，同样是分为了前置型和后置型，如下:
```
var age = 20;
var a = ++age + 1; // 为22 先age加1在加1
++age; //是先自加1，在使用age
a = 20;
var b = age++; //是先使用age在＋1，所以b为20
--age; //也是先减1在使用
age--: //是先使用age，再减一
```

递减和递增操作符遵循下列规则：
- 在应用于一个不包含有效数字字符的字符串时，将变量的值设为NaN，字符串变量变成数值变量
- 在应用于布尔值false时，先将其转换为0在执行加减1的操作
- 在应用于布尔值true时，先将其转换为1再执行加减1的操作
- 在应用于浮点数值时，执行加减1的操作
- 在应用于对象时，先调用对象的valueOf()方法以取得一个可供操作的值，然后再对值应用前述规则，如果结果是NaN，则在调用toString()方法在应用前述规则

#### 一元加和减操作符
一元加操作以一个加号表示，放在数值面前，对数值不会产生任何影响。
```
var num = 25;
num = +num; //仍然是25
```
一元减操作符主要用于表示负数，将1转换为-1:
```
var num = 25;
num = -num; // -25
```

### 位操作符
位操作符对内存中表示数值的位来操作数值，即操作二进制编码。负数的话则是按照二进制补码来进行存储的。

#### 按位非(NOT)
按位非操作符有一个~表示，执行按位非的结果就是返回数值的反码(包括符号位全部取反)。
```
var num1 = 25;
var num2 = ~num1; //-26 （包括符号位在内的所有二进制数值均取反）
```

#### 按位与(AND)
按位与操作符由一个和号&表示，他有两个操作符数，就是和计算机体系结构中教的一样。
第一个数值的位 | 第二个数值的位 | 结果
---|---|---
1 | 1 | 1
1 | 0 | 0
0 | 1 | 0
0 | 0 | 0

#### 按位或(OR)
按位与操作符由一个竖线|表示，他有两个操作符数，就是和计算机体系结构中教的一样。
第一个数值的位 | 第二个数值的位 | 结果
---|---|---
1 | 1 | 1
1 | 0 | 1
0 | 1 | 1
0 | 0 | 0

#### 按位异或(XOR)
相同为0，不同为1，如下所示:
第一个数值的位 | 第二个数值的位 | 结果
---|---|---
1 | 1 | 0
1 | 0 | 1
0 | 1 | 1
0 | 0 | 0

#### 左移
左移操作符由两个小于号<<表示，这个操作符会将数值的所有位左移指定的位数，例如
```
var value = 2 << 5; //将10左移五位变成1000000十进制的64
```
注意左移后，原数值的右侧多出5个空位，会用0填充，**左移不会影响符号位**。

#### 有符号的右移
有符号的右移操作由两个大于号>>表示，符号位同样不会被影响(移动)。

#### 无符号的右移
无符号的右移由3个大于号>>>表示，会影响符号位，符号位同样会被移动。

### 布尔操作符
之前提到的都是针对数值进行的位运算，下面逻辑操作符。

#### 逻辑非
逻辑非操作由一个叹号!表示，无论这个数据是什么类型，这个操作符都会返回一个布尔值。逻辑非操作首先会将它的操作数转换为一个布尔值，然后在对齐求反。逻辑非遵循以下规则：
- 如果操作数是一个对象，则返回false
- 如果操作数是一个空字符串，返回true
- 如果操作数是一个非空字符串，则返回false
- 如果操作数是数值0，返回true
- 如果操作数是任意非0的数值，返回false
- 如果操作数是null，返回true
- 如果操作是NaN，返回true
- 如果操作数是undefined，返回true

逻辑非！比较常用于条件语句中。

#### 逻辑与
逻辑与操作符由两个和号&&表示，有两个操作符:
第一个数值的位 | 第二个数值的位 | 结果
---|---|---
true | true | true
true | false | false
false | true | false
false | false | false

逻辑与遵循以下规则:
- 如果第一个操作数是对象，则返回第二个操作数
- 如果第二个操作数是对象，则只有在第一个操作数的求值结果为true的情况下才会返回该对象
- 如果两个操作数都是对象，则返回第二个操作数
- 如果有一个操作数是null，则返回null
- 如果有一个操作数是NaN，则返回NaN
- 如果有一个操作数是undefined，则返回undefined

#### 逻辑或
逻辑或由两个竖线符号||表示，有两个操作数：
第一个数值的位 | 第二个数值的位 | 结果
---|---|---
true | true | true
true | false | true
false | true | true
false | false | false

逻辑或遵循以下规则：
- 如果第一个操作数是对象，则返回第一个操作数
- 如果第一个操作数的求值结果为false的情况，则返回第二个操作数
- 如果两个操作数都是对象，则返回第一个操作数
- 如果有一个操作数是null，则返回null
- 如果有一个操作数是NaN，则返回NaN
- 如果有一个操作数是undefined，则返回undefined

**逻辑或操作是短路操作符**，如果第一个操作数的求值结果为true，则不会再进行了，而逻辑与在第一个操作符为true情况下，还需要接着看第二个操作符的数值。

### 乘性操作符
3个乘性操作符：乘法、除法和求模。如果参与乘法计算的某个操作数不是数值，后台会先使用Number()转型函数将其转化为数值。空字符串会被当做0，true会被当做1，false会被当做0.

#### 乘法
乘法操作用*表示，用于计算两个数值的乘积。
不过多陈述了。

#### 减法
减法操作符-同样很常用，不过多介绍了。

#### 求模
求模操作用%表示

### 关系操作符
小于<, 大于>, 小于等于<=, 大于等于>=，这个几个操作符返回的都是Boolean。不过多介绍了。

注意：数字字符串进行比较的话，则比较是ASCII码

### 相等操作符
#### 相等和不相等
判断相等使用的是==，判断不相等使用的是!=。不过多介绍了。

#### 全等和不全等
全等由三个等号===表示，不全等用!==表示，除了在比较之前不转换操作数之外，全等不全等和相等不相等之间没有任何区别。如:
```
var result = ("55" == 55); // true 自动转换
var result1 = ("55" === 55); // false 不会自动转换所以不相等
```

### 条件操作符
三元式，和之前学的条件操作符相似，语法如下:
```
variable = boolean_expression ? true_value : false_value;

var_max = (num1 > num2) ? num1 : num2;
```

### 赋值操作符
简单的赋值操作符有等号=表示，其作用就是把右侧的值赋给左侧的变量，如下面例子:
```
var num = 20;
```

复合赋值操作符如下:
- *= 乘赋值
- /= 除赋值
- %= 模赋值
- += 加赋值
- -= 减赋值
- <<= 左移赋值
- >>= 有符号右移赋值
- >>>= 无符号右移赋值

### 逗号操作符
使用逗号操作符在一条语句中执行多个操作，如下:
```
var num1=1,num2=2,num3=3;
```
常用于声明多个变量，除此之外，逗号操作符还可以用于赋值。在用于赋值时，逗号操作符总会返回表达式的最后一项，如下面式子:
```
var num1 = (5,2,3,4,5,0); //num值为0
```

## 语句
### if语句
形式如下:
```
if (condition){
    statement1;
}
else{
    statemetn2;
}

if (condition1){
    statement1;
}
else if(condition2){
    statemetn2;
}
else if(condition3){
    statement3;
}
else{
    statement4;
}
```

### do-while语句
形式如下:
```
do{
    statement1;
}while(condition);
```

### while语句
形式如下:
```
while(condition){
    statement1;
}
```

### for语句
形式如下:
```
for (var i=0; i < count; i++){
    statment;
}

var i;
for (i=0; i < count; i++){
    statment;
}

for循环的while形式:
for (;;){ // 无限循环
    statement;
}
```

### for-in语句
for-in语句可以用枚举对象的属性:
```
for (property in expression) statement

for (var propNum in window){
    document.wirte(propName); // 显示在window中的所有属性
}
```

建议在使用for-in循环之前，先检测确认对象的值不是null和undefined。

### label语句
使用label语句可以在代码中添加标签，以便将来使用。label语句的语法:
```
label: statement

start: for (var i=0; i<count; i++){
    alter(i)
}
```
这个例子中定义的start标签可以在将来有break或continue语句引用，加标签的语句一般都要与for等循环语句配合使用。

### break和continue语句
break和continue语句用于在循环中精确地控制代码的执行。其中break会立刻退出循环，强制继续执行循环后面的语句。contine虽然也会立即退出循环，但是退出循环后会从循环的顶部继续执行。

break和continue语句都可以和label语句联合使用，从而返回代码中特定的位置。这种联合使用的情况多发生在循环嵌套中，如下面的例子:
```
var num=0;
outermost: for (var i=0; i<10; i++){
    for (var j=0; j<10; j++){
        if (i==5 && j==5){
            break outermost; // 结束j的for和结束i的for
        }
        num++;
    }
}
```
上述操作不仅会退出第一层for也会退出第二层for。

```
var num=0;
outermost: for (var i=0; i<10; i++){
    for (var j=0; j<10; j++){
        if (i==5 && j==5){
            continue outermost; // 结束j的for和结束i的for
        }
        num++;
    }
}
```
contine只会结束本次循环，而继续进行后续的循环。

### with语句
with语句的作用是将代码的作用域设置到一个特定对象中，语法如下:
```
with (expression) statement;
```
with语句的目的主要是为了简化多次编写同一对象的工作，例如：
```
var qs = location.search.substring(1);
var hostName = location.hostname;
var url = location.href;
```
这几行代码都包含了location对象，可以使用with语句改写成:
```
with(location){
    var qs = search.substring(1);
    var hostname = hostname;
    var url = href;
}
```
使用with语句关联了location独享，这就意味着with语句的代码块内部，每个变量首先被认为是一个局部变量，而如果在局部环境中找不到该变量的定义，就会查询location对象是否有同名的属性，如果发现同名的属性，则以location对象的属性的值作为变量的值。  
严格模式下不允许使用with的，否则会视为语法错误。

### switch语句
和其他语言的类似:
```
swith (expression){
    case value1: statement1; break; // 没有break则进行执行
    case value2: statement2; break;
    case value3: statement3; break;
    case value4: statement4; break;
    default:statement; // 上面case条件都不满足，则执行default
}
```
使用break可以避免同时执行多个case代码的情况。

## 函数
函数使用function来声明。形式如下:
```
function functionName(arg0,arg1,arg2,...,argN){
    statements;
    return res; //return 可有可无
}
```

### 理解参数
JavaScript函数不介意传递进来有多少个参数，也不在乎传进来的参数是什么数据类型。即你定义的函数只接受两个参数，再调用函数时也未必会一定传两个参数。  
实际上，在函数体内可以通过arguments对象来访问这个参数数组，从而获得传递给函数的每一个参数。  
arguments对象只是与数组类似，因为可以使用方括号语法访问它的元素。使用length属性(arguments.length)来确定传递进来多少个参数。
```
function say(){
    alter("Hello" + arguments[0]+","+arguments[1]);
    alter(arguments.length);
}
```

### 没有重载
JavaScript函数不能像传统意义上的那样实现重载，在JavaScript中定义了两个名字相同的函数，则改名字只属于后定义的函数。