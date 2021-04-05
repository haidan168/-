# JavaScript 基础

一个完整的JavaScript实现包含了三个部分：ECMAScript、DOM和

BOM。

## 基本语法

### 1. 数据类型

- JavaScript有六中数据六类型：String（字符串）、Number（数值）、Boolean（布尔值）、Null（空值）、Undefined（未定义）、Object（对象）。
- String、Number、Boolean、Null、Undefined属于基本数据类型，Object属于引用数据类型

**String 字符串**

- 在JS中字符串需要使用引号引起来
- 使用双引号或单引号都可以，但是不要混着用
- 引号不能嵌套，双引号不能放双引号，单引号不能放单引号
- 在字符串中我们可以使用\作为转义字符，当表示一些特殊符号时可以使用\进行转义

```
\" 表示 "
\' 表示 '
\n 表示换行
\t 制表符
\\ 表示\
```

1.2 Number 数值

可以使用一个运算符 typeof 来检查一个变量的类型

```
typeof 变量
```

- 在JS中所有的数值都是Number类型，包括整数和浮点数（小数）
- JS中可以表示的数字的最大值和最小值

```
Number.MAX_VALUE
1.7976931348623157e+308

Number.MIN_VALUE 大于0的最小值
5e-324
```

- 如果使用Number表示的数字超过了最大值，则会返回一个Infinity（表示正无穷），-Infinity （表示负无穷）
- 使用typeof检查Infinity也会返回number
- **NaN** 是一个特殊的数字，表示Not A Number，使用typeof检查一个NaN也会返回number



**Null 和 Undefined**

**1. Null：**

- Null（空值）类型的值只有一个，就是null
- null这个值专门用来表示一个为空的对象
- 使用typeof检查一个null值时，会返回object

**2. Undefined：**

- Undefined（未定义）类型的值只有一个，就undefined
- 当声明一个变量，但是并不给变量赋值时，它的值就是undefined
- 使用typeof检查一个undefined时也会返回undefined

#### 1. 强制类型转化

强制类型转换，指讲一个数据类型强制转换为其他数据类型；类型转换主要指，将其他数据类型转换为String、Number、Boolean。

##### 1.1 将其他数据类型转换为 String

- 方法一：调用被转换数据类型的 toString() 方法

  - 但是注意：null和undefined这两个值没有toString()方法，
    如果调用他们的方法，会报错

  - 方法不会影响到原变量，它会将转换的结果返回

```
var a = 123;
a.toString();
console.log(typeof a); // number
console.log(a); // 123

a = a.toString();
console.log(typeof a); // String
console.log(a); // 123
```

- 方法二：调用String()函数，并将被转换的数据作为参数传递给函数
  - 使用String()函数做强制类型转换时，对于Number和Boolean实际上就是调用的toString()方法
  - 对于null和undefined，就不会调用toString()方法，它会将 null 直接转换为 "null"，将 undefined 直接转换为 "undefined"

```
var a = 123；
a = String(a);
console.log(typeof a); // String
console.log(a); // 123
```

##### 1.2 将其他数据类型转换为 Number

- 方法一：使用 Number() 函数

  - 字符串 --> 数字
    - 如果是纯数字的字符串，则直接将其转换为数字
    - 如果字符串中有非数字的内容，则转换为NaN
    - 如果字符串是一个空串或者是一个全是空格的字符串，则转换为0
  - 布尔 --> 数字
    - true 转成 1
    - false 转成 0
  - null --> 数字     为 0
  - undefined --> 数字     为NaN

- 方法二：parseInt() 和 parseFloat() 

  - 这两种方式是用来处理字符串类型
  - parseInt()
    - 把一个字符串转换为一个整数
    - 可以将一个字符串中的有效的整数内容去出来，然后转换为Number
  - parseFloat()
    - 把一个字符串转换为一个浮点数
    - 以获得有效的小数
  - 如果对非String使用parseInt()或parseFloat()，它会先将其转换为String然后在操作

  ```
  var a;
  a = "123px";
  
  a = parseInt(a);
  console.log(typeof a);// Number
  console.log(a);// 123
  ```

  ```
  a = "123.4.5px";
  
  a = parseInt(a);
  console.log(typeof a);// Number
  console.log(a);// 123
  
  a = parseFloat(a);
  console.log(typeof a);// Number
  console.log(a);// 123.4
  ```

  ```
  a = true;
  
  a = parseInt(a);
  console.log(typeof a);// Number
  console.log(a);// NAN
  ```

  ```
  a = 123.4;
  
  console.log(typeof a);// Number
  console.log(a);// 123
  ```

##### 1.3将其他的数据类型转换为Boolean

- 使用 Boolean() 函数
  - 数字 ---> 布尔
    - 除了0和NaN，其余的都是true
  - 字符串 ---> 布尔
    - 除了空串（""），其余的都是true
  - null和undefined都会转换为false
  - 对象也会转换为true

### 2. 其他进制

- 表示16进制的数，以 0x 开头
- 表示8进制的数，以 0 开头
- 表示2进制的数，以 0b 开头，但是不是所有浏览器支持2进制

注：像 "070" 这种字符串，有些浏览器会当成8进制解析，有些会当成10进制解析

- 可以在parseInt()中传递一个第二个参数，来指定数字的进制

```
var a = "070";
a = parseInt(a,10);
```

- 对于Number调用toString()时可以在方法中传递一个整数作为参数
- 此时它将会把数字转换为指定的进制,如果不指定则默认转换为10进制

```
var a = 255;
a = a.toString(2);
```

### 3. 运算符

通过运算符可以对一个或多个值进行运算,并获取运算结果。

- typeof
  - typeof就是运算符，可以来获得一个值的类型，它会将该值的类型以字符串的形式返回

#### **3.1. 算数运算符**

当对非Number类型的值进行运算时，会将这些值转换为Number然后在运算。

**何值和NaN做运算都得NaN**

**任何的值和字符串做加法运算，都会先转换为字符串，然后再和字符串做拼串的操作**

- +：
  - 可以对两个值进行加法运算，并将结果返回
  - 如果对两个字符串进行加法运算，则会做拼串，将两个字符串拼接为一个字符串返回
  - 任何的值和**字符串做加法运算**，都会**先转换为字符串**，然后再和字符串做拼串的操作
    - 可以利用这一特点，来将一个任意的数据类型转换为String
    - 只需要为任意的数据类型 + 一个 "" 即可将其转换为String，这是一种隐式的类型转换，由浏览器自动完成，实际上它也是调用String()函数

```
result = 1 + 2 + "3"; //33
result = "1" + 2 + 3; //123
```

- -：可以对两个值进行减法运算，并将结果返回
- *：可以对两个值进行乘法运算
- /：可以对两个值进行除法运算
- %：取模运算（取余数）
- 任何值做- * /运算时都会自动转换为Number
  - 可以利用这一特点做隐式的类型转换
  - 可以通过为一个值 -0、 *1、 /1来将其转换为Number，原理和Number()函数一样

#### 3.2. 一元运算符

一元运算符，只需要一个操作数

- +：正号
  - 正号不会对数字产生任何影响
- -：负号
  - 负号可以对数字进行负号的取反
- 对于非Number类型的值，会将先转换为Number，然后在运算，可以对一个其他的数据类型使用+,来将其转换为number

```
var result = 1 + +"2" + 3;// 6
```

#### 3.3. 自增和自减

- 自增 ++
  - 通过自增可以使变量在自身的基础上增加1
  - 对于一个变量自增以后，原变量的值会立即自增1
  - 无论是a++ 还是 ++a，都会立即使原变量的值自增1
    - 不同的是a++ 和 ++a的值不同
    - a++的值等于原变量的值（自增前的值）
    - ++a的值等于新值 （自增后的值）

```
var d = 20;

d = d++;
console.log(a);// 20

var e = d++;
d = e;
```

- 自减 --
  - 通过自减可以使变量在自身的基础上减1
  - 无论是a-- 还是 --a 都会立即使原变量的值自减1
    - 不同的是a-- 和 --a的值不同
    - a-- 是变量的原值 （自减前的值）
    - --a 是变量的新值 （自减后的值）

#### 3.4 逻辑运算符

JS提供了三种运算符：！（非）、&&（与）、||（或）

- **！非**：
  - !可以用来对一个值进行非运算（对一个布尔值进行取反操作，true变false，false变true）
  - 如果对一个值进行两次取反，它不会变化
    - 可以利用该特点，来将一个其他的数据类型转换为布尔值
    - 为一个任意数据类型取两次反，来将其转换为布尔值，原理和Boolean()函数一样
  - 如果对非布尔值进行元素，则会将其转换为布尔值，然后再取反
- **&& 与**：
  - &&可以对符号两侧的值进行与运算并返回结果
  - 运算规则：
    - 两个值中只要有一个值为false就返回false，只有两个值都为true时，才会返回true
    - JS中的“与”属于短路的与，如果第一个值为false，则不会看第二个值
- **|| 或**：
  - ||可以对符号两侧的值进行或运算并返回结果
  - 运算规则：
    - 两个值中只要有一个true，就返回true，如果两个值都为false，才返回false
    - JS中的“或”属于短路的或，如果第一个值为true，则不会检查第二个值 

**&& || 非布尔值的情况**：

- 对于非布尔值进行与或运算时，会先将其转换为布尔值，然后再运算，**并且返回原值**
- 与运算：
  - 如果第一个值为true，则必然返回第二个值的原值
  - 如果第一个值为false，则直接返回第一个值的原值
- 或运算：
  - 如果第一个值为true，则直接返回第一个值的原值
  - 如果第一个值为false，则直接返回第二个值的原值

#### 3.5 赋值运算符

- =
  - 可以将符号右侧的值赋值给符号左侧的变量
- +=
  - a += 5 等价于 a = a + 5
- -=
  - a -= 5 等价于 a = a - 5
- *=
  - a *= 5 等价于 a = a * 5
- /=
  - a /= 5 等价于 a = a / 5
- %=
  - a %= 5 等价于 a = a % 5

#### 3.6 关系运算符

通过关系运算符可以比较两个值之间的大小关系，如果关系成立它会返回true，如果关系不成立则返回false

- （>）大于
  - 判断符号左侧的值是否大于右侧的值
  - 如果关系成立，返回true，如果关系不成立则返回false
- （>=）大于等于
  - 判断符号左侧的值是否大于或等于右侧的值
- （<）小于和 （<=）同理

**非数值情况**：

- 对于非数值进行比较时，会将其转换为数字然后在比较
  - 任何值和NaN做任何比较都是false
- 如果符号**两侧的值都是字符串**时，不会将其转换为数字进行比较，而会**分别比较字符串中字符的Unicode编码**
  - 比较两个字符串时，比较的是字符串的字符编码
  - 比较字符编码时是**一位一位进行比较**
  - 如果两位一样，则比较下一位，所以借用它来对英文进行排序
  - 如果比较的两个字符串型的数字，可能会得到不可预期的结果
  - **/注意：在比较两个字符串型的数字时，一定一定一定要转型**

```
console.log("1" < "5"); //true
console.log("11" < "5"); //true

//比较两个字符串时，比较的是字符串的字符编码
console.log("a" < "b");//true

//如果两位一样，则比较下一位，所以借用它来对英文进行排序
console.log("abc" < "bcd");//true

console.log("11123123123123123123" < "5"); //true
console.log("11123123123123123123" < +"5"); //false
```

**编码**：

- 在字符串中使用转义字符输入Unicode编码，\u四位编码

```
console.log("\u2620");
```

- 在网页中使用Unicode编码，#编码; 这里的编码需要的是10进制

```
<h1 style="font-size: 200px;">&#9760;</h1>
```

#### 3.7 条件运算符（三元运算符）

- 语法：
  - 条件表达式?语句1:语句2;
- 执行的流程： 
  - 首先对条件表达式进行求值
    - 如果该值为true，则执行语句1，并返回执行结果
    - 如果该值为false，则执行语句2，并返回执行结果
  - 如果条件的表达式的求值结果是一个非布尔值，会将其转换为布尔值然后在运算

### 4. 语句

**代码块**

- 程序是由一条一条语句构成的，语句是按照自上向下的顺序一条一条执行的，在JS中可以使用{}来为语句进行分组,同一个{}中的语句我们称为是一组语句，它们要么都执行，要么都不执行，一个{}中的语句我们也称为叫一个**代码块**，在代码块的后边就不用再编写;了。
- JS中的代码块，只具有分组的的作用，没有其他的用途，代码块内容的内容，在外部是完全可见的

```
{
	var a = 10;	
	alert("hello");
	console.log("你好");
	document.write("语句");
}
console.log("a = "+a); // 10
```

**流程控制语句**

S中的程序是从上到下一行一行执行的，通过流程控制语句可以控制程序执行流程，使程序可以根据一定的条件来选择执行

- 语句的分类：
  1. 条件判断语句
  2. 条件分支语句
  3. 循环语句

#### 4.1 if 语句（条件判断语句）

用条件判断语句可以在执行某个语句之前进行判断，如果条件成立才会执行语句，条件不成立则语句不执行。

**语法一：**

```
if(条件表达式){
	语句...
}
```

- if语句在执行时，会先对条件表达式进行求值判断，如果条件表达式的值为true，则执行if后的语句，如果条件表达式的值为false，则不会执行if后的语句
- if语句只能控制紧随其后的那个语句,如果希望if语句可以控制多条语句，可以将这些语句统一放到代码块中

**语法二：**

```
if(条件表达式){
	语句...
	}else{
	语句...
}
```

- 当该语句执行时，会先对if后的条件表达式进行求值判断
  - 如果该值为true，则执行if后的语句
  - 如果该值为false，则执行else后的语句

**语法三：**

```
if(条件表达式){
	语句...
}else if(条件表达式){
	语句...
}else if(条件表达式){
	语句...
}else{
	语句...
}
```

- 语句执行时，会从上到下依次对条件表达式进行求值判断
  - 如果值为true，则执行当前语句
  - 如果值为false，则继续向下判断
  - 如果所有的条件都不满足，则执行最后一个else后的语句
  - 该语句中，只会有一个代码块被执行，一旦代码块执行了，则直接结束语句

#### 4.2 switch语句（条件分支语句）

语法：

```
switch(条件表达式){
	case 表达式:
		语句...
		break;
	case 表达式:
		语句...
		break;
	default:
		语句...
		break;
}
```

- 在执行时会依次将case后的表达式的值和switch后的条件表达式的值进行**全等比较**
- 如果比较结果为true，则从当前case处开始执行代码，之后case下的语句也会执行
- 在case的后边跟着一个break关键字，这样可以确保只会执行当前case后的语句，而不会执行其他的case
- 如果比较结果为false，则继续向下比较
- 如果所有的比较结果都为false，则只执行default后的语句

#### 4.3 循环语句

通过循环语句可以反复的执行一段代码多次

##### 4.3.1 while循环

语法：

```
while(条件表达式){
	语句...
}
```

- while语句在执行时，先对条件表达式进行求值判断，如果值为true，则执行循环体
- 循环体执行完毕以后，继续对表达式进行判断，如果为true，则继续执行循环体，以此类推
- 如果值为false，则终止循环

##### 4.3.2 do...while 循环

语法：

```
do{
	语句...
}while(条件表达式)
```

- do...while语句在执行时，会先执行循环体，循环体执行完毕以后，在对while后的条件表达式进行判断
- 如果结果为true，则继续执行循环体，执行完毕继续判断以此类推
- 果结果为false，则终止循环

while 和 do...while的区别：

- while是先判断后执行
- do...while会先执行后判断
- do...while可以保证循环体至少执行一次，而while不能

##### 4.3.3 for 循环

语法：

```
for(①初始化表达式;②条件表达式;④更新表达式){
	③语句...
}
```

- for循环的执行流程：
  - ①执行初始化表达式，初始化变量（初始化表达式只会执行一次）
  - ②执行条件表达式，判断是否执行循环。
    - 如果为true，则执行循环③
    - 如果为false，终止循环
  - ④执行更新表达式，更新表达式执行完毕继续重复②
- or循环中的三个部分都可以省略，也可以写在外部，如果在for循环中不写任何的表达式，只写两个; ，此时循环是一个死循环会一直执行下去

```
for(;;){
	alert("hello");
}
```

##### 4.3.4 break 和 continue

break：

- break关键字可以用来退出switch或循环语句
- 不能在if语句中使用break和continue

```
if(i == 2){
	break;
}// 外层没有循环语句，浏览器会报错
```

- break关键字，会立即终止离他最近的那个循环语句
- 可以为循环语句创建一个label，来标识当前的循环
  - label:循环语句
  - 使用break语句时，可以在break后跟着一个label，这样break将会结束指定的循环，而不是最近的

```
outer:
for(var i=0 ; i<5 ; i++){
	console.log("@外层循环"+i)
	for(var j=0 ; j<5; j++){
		break outer;
		console.log("内层循环:"+j);
	}
}
```

continue：

- continue关键字可以用来跳过当次循环
- 同样continue也是默认只会对离他最近的循环循环起作用
- 同样可以为循环语句创建一个label，来标识当前的循环

开启计时器：

```
console.time("计时器的名字");//可以用来开启一个计时器
```

- 它需要一个字符串作为参数，这个字符串将会作为计时器的标识

终止计时器：

```
console.timeEnd("计时器的名字");//用来停止一个计时器，需要一个计时器的名字作为参数
```

开放：

```
Math.sqrt(97);
```

##  对象

对象属于一种复合的数据类型，在对象中可以保存多个不同数据类型的属性。

对象分类：

1. 内建对象
   - 由ES标准中定义的对象，在任何的ES的实现中都可以使用
     - 比如：Math String Number Boolean Function Object....
2. 宿主对象
   - 由JS的运行环境提供的对象，目前来讲主要指由浏览器提供的对象
     - 比如 BOM DOM
3. 自定义对象
   - 由开发人员自己创建的对象

### 1. 自定义对象

**创建对象：**

```
var obj = new Object();
```

- 使用new关键字调用的函数，是构造函数constructor
- 造函数是专门用来创建对象的函数

**向对象添加属性：**

```
obj.age = 18;
```

- 语法：对象.属性名 = 属性值;

**读取对象中的属性：**

```
obj.age
```

- 语法：对象.属性名
- 如果读取对象中没有的属性，不会报错而是会返回undefined

**修改对象的属性值：**

```
obj.age = 19;
```

- 语法：对象.属性名 = 新值

**删除对象的属性：**

```
delet obj.age;
```

- 语法：delete 对象.属性名

#### 1.1 属性名和属性值

**属性名：**

- 对象的属性名不强制要求遵守标识符的规范，什么乱七八糟的名字都可以使用，但是我们使用是还是尽量按照标识符的规范去做。

- 如果要使用特殊的属性名，不能采用.的方式来操作
  - 语法：对象["属性名"] = 属性值
  - 读取时也需要采用这种方式
  - 使用[]这种形式去操作属性，更加的灵活，在[]中可以直接传递一个变量，这样变量值是多少就会读取那个属性

```
obj["123"] = 789;
obj["nihao"] = "你好";
var n = "nihao";
var m = "123"
console.log(obj[n]);//你好
console.log(obj[m]);//789
```

**属性值：**

- JS对象的属性值，可以是任意的数据类型，甚至也可以是一个对象

**in 运算符：**

- 通过该运算符可以检查一个对象中是否含有指定的属性
  - 如果有则返回true，没有则返回false
- 语法："属性名" in 对象

```
var obj = new Object();
obj.age = 18;

console.log("age" in obj);//true
console.log("name" in obj);//false
```

#### 1.2 基本数据类型和引用数据类型

**基本数据类型：**

- String Number Boolean Null Undefined
- JS中的变量都是保存到栈内存中的，基本数据类型的值直接在栈内存中存储
- 值与值之间是独立存在，修改一个变量不会影响其他的变量

**引用数据类型：**

- Object
- 对象是保存到堆内存中的，每创建一个新的对象，就会在堆内存中开辟出一个新的空间
- 而变量保存的是对象的内存地址（对象的引用），如果两个变量保存的是同一个对象引用
- 当一个通过一个变量修改属性时，另一个也会受到影响

区别：

- 当比较两个基本数据类型的值时，就是比较值
- 比较两个引用数据类型时，它是比较的对象的内存地址
  - 如果两个对象是一摸一样的，但是地址不同，它也会返回false

#### 1.3 对象字面量

- 使用对象字面量来创建一个对象

```
var obj = {};
```

- 使用对象字面量，可以在创建对象时，直接指定对象中的属性

```
var obj2 = {
	
	name:"丁霞",
	age:13,
	gender:"女",
	test:{name:"Hebe"}
	
};
```

- 语法：{属性名:属性值,属性名:属性值....}
- 对象字面量的属性名可以加引号也可以不加，建议不加,如果要使用一些特殊的名字，则必须加引号
- 属性名和属性值是一组一组的名值对结构
- 名和值之间使用:连接，多个名值对之间使用,隔开
- 如果一个属性之后没有其他的属性了，就不要写

### 2. 函数

- 函数也是一个对象

- 函数中可以封装一些功能（代码），在需要时可以执行这些功能（代码）
- 函数中可以保存一些代码在需要的时候调用
- 使用typeof检查一个函数对象时，会返回function

#### 2.1 函数的声明

**使用构造函数创建函数：**

```
var fun = new Function("console.log('Hello 这是我的第一个函数');");
```

- 可以将要封装的代码以字符串的形式传递给构造函数

**使用函数声明创建函数：**

```
function fun2(){
	console.log("这是我的第二个函数~~~");
}

语法：
// 使用[]，表示可选
function 函数名([形参1,形参2...形参N]){
	语句...
}
```

**使用函数表达式创建函数：**

```
var fun3 = function(){
	console.log("我是匿名函数中封装的代码");
};

语法：
var 函数名  = function([形参1,形参2...形参N]){
	 语句....
}
```

**调用函数：**

```
fun();

语法：
函数对象();
```

- 当调用函数时，函数中封装的代码会按照顺序执行

#### 2.2 函数的参数

- 可以在函数的()中来指定一个或多个形参（形式参数）
- 多个形参之间使用,隔开，声明形参就相当于在函数内部声明了对应的变量
- 但是并不赋值

```
function sum(a,b){
	console.log(a+b);
}
```

- 在调用函数时，可以在()中指定实参（实际参数）
- 实参将会赋值给函数中对应的形参

```
sum(1,2);
```

- 调用函数时解析器不会检查实参的类型
  - 要注意，是否有可能会接收到非法的参数，如果有可能则需要对参数进行类型的检查
- 函数的实参可以是任意的数据类型

```
sum(123,"hello");
sum(true , false);
```

- 调用函数时，解析器也不会检查实参的数量
- 多余实参不会被赋值
- 如果实参的数量少于形参的数量，则没有对应实参的形参将是undefined

#### 2.3 函数的返回值

- 可以使用 return 来设置函数的返回值

```
function sum(a,b){
	return a+b;
}

语法：
	return 值;
```

- return后的值将会会作为函数的执行结果返回，可以定义一个变量，来接收该结果
- 在函数中return后的语句都不会执行
- 如果return语句后不跟任何值就相当于返回一个undefined，函数中不写return，则也会返回undefined

```
var result = sum(1,2);
```

- 变量result的值就是函数的执行结果
- 函数返回什么result的值就是什么
  - 返回值可以是任意的数据类型,也可以是一个对象，也可以是一个函数

```
function fun(){
	function fun1(){
		consloe.log("fun1");
	}
	return fun1;
}

a = fun();//fun1
fun()();//fun1();
```

#### 2.4 立即执行函数

```
(function(a,b){
	consloe.log(a + b);
})(1,2);
```

- 函数定义完，立即被调用，这种函数叫做立即执行函数
- 立即执行函数往往只会执行一次

### 3. 枚举对象中的属性

使用 for ... in 语句

```
语法：
for(var 变量 in 对象){
	
}
```

- for...in语句，对象中有几个属性，循环体就会执行几次
- 每次执行时，会将对象中的一个属性的名字赋值给变量

```
var obj = {
	name:"dx",
	number1:"8",
	number2:"16"
}
```

```
for(var n in obj){
	console.log("属性名="+n+
				",属性值="+obj[n]);
}

// 属性名=name，属性值=dx
// 属性名=number1，属性值=8
// 属性名=number2，属性值=16
```

### 4. 作用域(Scope)

作用域指一个变量的作用的范围。

在JS中一共有两种作用域：

##### 4.1 全局作用域

- 直接编写在script标签中的JS代码，都在全局作用域
- 全局作用域在页面打开时创建，在页面关闭时销毁
  - 在全局作用域中有一个**全局对象window**，它代表的是一个浏览器的窗口，它由浏览器创建可以直接使用
  - 在全局作用域中：
    - 创建的**变量**都会作为window对象的**属性**保存
    - 创建的**函数**都会作为window对象的**方法**保存
  - 全局作用域中的变量都是全局变量，在页面的任意的部分都可以访问的到

- 对象的属性值可以是任何的数据类型，也可以是个函数
- 如果一个函数作为一个对象的属性保存，称这个函数时这个**对象的方法**，调用这个函数就说调用对象的方法（method）

```
var obj = {
	name="dx",
	sayName:function(){
		consloe.log(obj.name);
	}
}
```

##### 4.2 变量声明提前

**变量声明提前：**

- **使用var关键字**声明的变量，会在所有的代码执行之前被声明（但是不会赋值）

```
console.log(a);// undefined
var a = "dx";
```

- 如果声明变量时**不使用var关键字**，则变量不会被声明提前

```
console.log(a);//Uncaught ReferenceError: a is not defined
a = "dx";
```

**函数声明提前：**

- 使用函数声明形式创建的函数（ function 函数(){}）
  - 它会在所有的代码执行之前就被创建，所以我们可以在函数声明前来调用函数

```
fun();// dx

function fun(){
	console.log("dx");
}
```

- 使用函数表达式创建的函数(var 函数名 = function(){})
  - 不会被声明提前，所以不能在声明前调用

```
fun();//Uncaught TypeError: fun is not a function
var fun = function(){
	console.log("dx");
}
```

##### 4.3 函数作用域

- 调用函数时创建函数作用域，函数执行完毕以后，函数作用域销毁
- 每调用一次函数就会创建一个新的函数作用域，他们之间是互相独立的
- 在函数作用域中可以访问到全局作用域的变量，在全局作用域中无法访问到函数作用域的变量

```
var a = "dx";
function fun(){
	console.log(a);//dx
}
fun();
```

- 在函数作用域操作一个变量时，它会先在自身作用域中寻找，如果有就直接使用
- 如果没有则向上一级作用域中寻找，直到找到全局作用域
- 如果全局作用域中依然没有找到，则会报错ReferenceError
- 在函数中要访问全局变量可以使用window对象

**在函数作用域也有声明提前的特性：**

- 使用var关键字声明的变量，会在函数中所有的代码执行之前被声明

```
var a = "hebe";
function fun(){
	console.log(a);//undefined
	var a = "dx";
}
fun();
```

```
function fun(a){
	console.log(a);//undefined
}
fun();
```

- 函数声明也会在函数中所有的代码执行之前执行
- 在函数中，不使用var声明的变量都会成为全局变量

```
var a = "hebe";
function fun(){
	 a = "dx";
	 //相当于 window.a
}
fun();
console.log(a);//dx
```

```
var a = "hebe";
function fun(){
	console.log(a);//hebe
	a = "dx";// 这个a是全局的
}
fun();
```

```
var a = "dx";
function fun(a){
	console.log(a);//undefined
	a = "hebe";// 对局部的a进行赋值操作
}
fun();
console.log(a);//dx
```

### 5. this

解析器在调用函数每次都会向函数内部传递进一个隐含的参数,这个隐含的参数就是this，this指向的是一个对象，这个对象我们称为函数执行的上下文对象。

- 根据函数的调用方式的不同，this会指向不同的对象

  - 以函数的形式调用时，this永远都是window

  - 以方法的形式调用时，this就是调用方法的那个对象

```
// 创建的变量都会作为window对象的属性保存
var name = "hebe";
// 创建的函数都会作为window对象的方法保存
function fun(){
	console.log(this.name);//hebe
}
fun();//相当于 window.fun();
```

```
var obj = {
	name:"dx",
	sayName:fun
}
obj.sayName();//dx
```

### 6. 构造函数

- 构造函数就是一个普通的函数，创建方式和普通函数没有区别,不同的是构造函数习惯上首字母大写。

- 构造函数和普通函数的区别就是调用方式的不同
  - 通函数是直接调用，而构造函数需要使用new关键字来调用

```
function Person(name){
	this.name = name;
	this.sayName = function(){
		console.log(this.name);//dx
	};
}
var person = new Person("dx");
```

- **构造函数的执行流程：**
  1. 立刻创建一个新的对象(person)
  2. 将新建的对象设置为函数中this,在构造函数中可以使用this来引用新建的对象(person)
  3. 逐行执行函数中的代码
  4. 将新建的对象作为返回值返回
- 使用同一个构造函数创建的对象，我们称为一类对象，也将一个构造函数称为一个类
- this的情况：
  1. 当以函数的形式调用时，this是window
  2. 方法的形式调用时，this就是调用方法的那个对象
  3. 当以构造函数的形式调用时，this就是新创建的那个对象(person)

**instanceof：**

- 使用instanceof可以检查一个对象是否是一个类的实例

```
语法：
对象 instanceof 构造函数
person instanceof Person;//true
```

- 如果是，则返回true，否则返回false
- 所有的对象都是Object的后代
  - 任何对象和Object做instanceof检查时都会返回true

### 7. 原型 prototype

- 我们所创建的每一个函数，解析器都会向函数中添加一个属性prototype
- 这个属性对应着一个对象，这个对象就是我们所谓的原型对象
- 当函数以构造函数的形式调用时，它所创建的对象中都会有一个隐含的属性，指向该构造函数的原型对象,可以通过(\__proto__)来访问该属性
- 原型对象就相当于一个公共的区域，所有同一个类的实例都可以访问到这个原型对象
- 可以将对象中共有的内容，统一设置到原型对象中
- 原型对象也是对象，所以它也有原型
  - 当使用一个对象的属性或方法时，会现在自身中寻找，自身中如果有，则直接使用
  - 如果没有则去原型对象中寻找，如果原型对象中有，则使用
  - 如果没有则去原型的原型中寻找,直到找到Object对象的原型
  - Object对象的原型没有原型，如果在Object原型中依然没有找到，则返回undefined

> 使用in检查对象中是否含有某个属性时，如果对象中没有但是原型中有，也会返回true
>
> ```
> fun Person(){
> 	
> }
> var per = new Person();
> per.prototype.name = "dx";
> console.log("name" in per);//true
> ```
>
> 可以使用对象的hasOwnProperty()来检查对象自身中是否含有该属性
>
> - 使用该方法只有当对象自身中含有属性时，才会返回true
>
> ```
> console.log(per.hasOwnProperty("name"));//false
> ```

**创建对象的方法：**

> 1. 字面量
>
> ```
> var obj1 = {name:"obj1"};
> var obj2 = new Object({name:"obj2"});
> //= Object {name: "obj1"}
> ```
>
> 2. 构造函数
>
> ```
> function Fun(name){
> 	this.name = name;
> }
> var obj3 = new Fun("obj3");
> //= Fun {name: "obj3"}
> ```
>
> 3. 使用Object的create方法
>
> ```
> var p = {name:"p"};
> var obj4 = Object.create(p);
> //= Object {}
> ```

### 8. 垃圾回收

- 当一个对象没有任何的变量或属性对它进行引用，此时我们将永远无法操作该对象
- 此时这种对象就是一个垃圾，这种对象过多会占用大量的内存空间，导致程序运行变慢
- 在JS中拥有自动的垃圾回收机制，会自动将这些垃圾对象从内存中销毁
- 我们不需要也不能进行垃圾回收的操作
- 只是要将不再使用的对象设置null即可进行垃圾回收

### 9. 数组

- 数组也是一个对象，和普通对象功能类似，也是用来存储一些值的
- 不同的是普通对象是使用字符串作为属性名的，而数组时使用数字来作为索引操作元素
  - 索引：从0开始的整数就是索引
- 

**创建数组对象：**

- 使用构造函数创建对象
  - 用构造函数创建数组时，也可以同时添加元素，将要添加的元素作文构造函数的参数传递,元素之间使用,隔开

```
var arr = new Array();
```

```
var arr = new Array(1,2,3);
console.log(arr);//1,2,3
```

- 使用字面量创建数组
  - 使用字面量创建数组时，可以在创建时就指定数组中的元素

```
var arr = [];
```

```
var arr = [1,2,3];
console.log(arr);//1,2,3
```

- 区别：

```
// 创建一个数组数组中只有一个元素2
var arr = [2]
console.log(arr);//2

// 创建一个长度为2的数组
var arr2 = new Array(2);
console.log(arr2);// ,,
```

**向数组中添加元素：**

```
arr[0] = 10;
//语法：数组[索引] = 值
```

- 读取数组中的元素
  - 如果读取不存在的索引，他不会报错而是返回undefined

```
console.log(arr[10]);//10
//语法：数组[索引]
```

- 获取数组的长度
  - 可以使用length属性来获取数组的长度(元素的个数)
  - 对于连续的数组，使用length可以获取到数组的长度（元素的个数）
  - 对于非连续的数组，使用length会获取到数组的最大的索引+1

```
console.log(arr.length);//1

var arr2 = new Array();
arr2[0] = 1;
arr2[3] = 2;
console.log(arr2.length);//4
```

- 修改length
  - 如果修改的length大于原长度，则多出部分会空出来
  - 如果修改的length小于原长度，则多出的元素会被删除
- 向数组的最后一个位置添加元素

```
arr[arr.length] = 20;
//语法：数组[数组.length] = 值;
```

**数组中的元素可以是任意的数据类型**

#### 9.1 push()

> - 该方法可以向数组的末尾添加一个或多个元素，并返回数组的新的长度
> - 可以将要添加的元素作为方法的参数传递,这样这些元素将会自动添加到数组的末尾
> - 该方法会将数组新的长度作为返回值返回

```
var arr = ["hebe"];
var result = arr.push("dx","16");
console.log(arr);//["hebe", "dx","16"]
console.log(result)//3
```

#### 9.2 pop()

> - 该方法可以删除数组的最后一个元素,并将被删除的元素作为返回值返回

```
var arr = ["hebe","dx","330","16"];
var result = arr.pop();
console.log(arr);// ["hebe", "dx", "330"]
console.log(result);//16
```

#### 9.3 unshift()

> - 向数组开头添加一个或多个元素，并返回新的数组长度
> - 向前边插入元素以后，其他的元素索引会依次调整

```
var arr = ["hebe"];
var result = arr.unshift("dx","16");
console.log(arr);//["dx","16", "hebe"]
console.log(result)//3
```

#### 9.4 shift()

> - 删除数组的第一个元素，并将被删除的元素作为返回值返回

```
var arr = ["hebe","dx","330","16"];
var result = arr.shift();
console.log(arr);// ["dx","330","16"]
console.log(result);//hebe
```

#### 9.5 forEach()

这个方法只支持IE8以上的浏览器，IE8及以下的浏览器均不支持该方法。

> - forEach()方法需要一个函数作为参数
>   - 像这种函数，由我们创建但是不由我们调用的，我们称为回调函数
> - 数组中有几个元素函数就会执行几次
> - 每次执行时，浏览器会将遍历到的元素，以实参的形式传递进来，我们可以来定义形参，来读取这些内容
>   - 浏览器会在回调函数中传递三个参数：
>     - 第一个参数，就是当前正在遍历的元素
>     - 第二个参数，就是当前正在遍历的元素的索引
>     - 第三个参数，就是正在遍历的数组

```
var arr = ["hebe","dx"];
arr.forEach(function(value,index,obj){
	console.log(value,index,obj);
})
//hebe 0 ["hebe", "dx"]
//dx 1 ["hebe", "dx"]
```

#### 9.6 slice()

> - 可以用来从数组提取指定元素
>
> - 该方法**不会改变原来的数组**，而是将截取到的元素封装到一个**新数组**中返回
>
> - 参数：
>
>   1. 截取开始的位置的索引,包含开始索引
>   2. 截取结束的位置的索引,不包含结束索引
>      - 二个参数可以省略不写,此时会截取从开始索引往后的所有元素
>
> - 索引可以传递一个负值，如果传递一个负值，则从后往前计算
>
>   -1：倒数第一个
>
>   -2：倒数第二个

```
var arr = ["hebe","dx","330","16"];
var result = arr.slice(1,2);
console.log(arr);//["hebe", "dx", "330", "16"]
console.log(result);//["dx"]
```

```
var arr = ["hebe","dx","330","16"];
var result = arr.slice(1);
console.log(arr);//["hebe", "dx", "330", "16"]
console.log(result);//["dx","330","16"]
```

```
var arr = ["hebe","dx","330","16"];
var result = arr.slice(0,-2);
console.log(arr);//["hebe", "dx", "330", "16"]
console.log(result);//["hebe", "dx"]
```

#### 9.7 splice()

> - 可以用于删除数组中的指定元素
> - 使用splice()**会影响到原数组**，会将指定元素从原数组中删除,并将被删除的元素作为返回值返回
> - 参数：
>   1. 表示开始位置的索引
>   2. 表示**删除的数量**
>   3. 第三个及以后。。
>      - 可以传递一些新的元素，这些元素将会自动插入到开始位置索引前边

```
var arr = ["hebe","dx","330","16"];
var result = arr.splice(1,2);
console.log(arr);//["hebe", "16"]
console.log(result);//["dx", "330"]
```

```
var arr = ["hebe","dx","330","16"];
var result = arr.splice(1,2,"8");
console.log(arr);//["hebe","8", "16"]
console.log(result);//["dx", "330"]
```

```
var arr = ["hebe","dx","330","16"];
var result = arr.splice(1,0,"8");
console.log(arr);//["hebe","8","dx","330","16"]
console.log(result);//[]
```

#### 9.8 concat()

> - 可以连接两个或多个数组，并将新的数组返回
> - 该方法不会对原数组产生影响

```
var arr1 = ["hebe","330"];
var arr2 = ["dx","16"];
var arr3 = ["2"];
var result = arr1.concat(arr2,arr3,"8");
console.log(arr1);//["hebe","330"]
console.log(result);//["hebe","330","dx","16","2","8"]
```

#### 9.9 join()

> - 可以将数组转换为一个字符串
> - 不会对原数组产生影响，而是将转换后的字符串作为结果返回
> - 在join()中可以指定一个字符串作为参数，这个字符串将会成为数组中元素的连接符
>   - 如果不指定连接符，则默认使用,作为连接符

```
var arr = ["hebe","330","dx","16"];
var result1 = arr.join();
var result2 = arr.join("-");
console.log(arr);//["hebe","330","dx","16"]
console.log(result1);//hebe,330,dx,16
console.log(result2);//hebe-330-dx-16
```

#### 9.10 sort()

> - 可以用来对数组中的元素进行排序
> - 会影响原数组，默认会按照Unicode编码进行排序
> - 即使对于纯数字的数组，使用sort()排序时，也会按照Unicode编码来排序,所以对数字进排序时，可能会得到错误的结果

```
var arr = ["b","r","d","a","x"];
arr.sort();
console.log(arr);//["a", "b", "d", "r", "x"]
```

```
var arr = [5,3,6,7,11,2];
arr.sort();
console.log(arr);//[11, 2, 3, 5, 6, 7]
```

> - 在sort()添加一个回调函数，来指定排序规则
> - 回调函数中需要定义两个形参
> - 浏览器将会分别使用数组中的元素作为实参去调用回调函数
>
> ```
> var arr = [5,4,2,1,3,6,8,7,11];
> arr.sort(function(a,b){
> 	// 升序排列
> 	if(a > b){
> 		// 数组中前面的数，比后面的大，换位
> 		return 1;
> 	}else if(a < b){
> 		// 数组中前面的数，比后面的小，不换位
> 		return -1;
> 	}else{
> 		// 数组中前面的数和后面的数一样大，不换位
> 		return 0;
> 	}
> });
> console.log(arr);//[1, 2, 3, 4, 5, 6, 7, 8, 11]
> ```
>
> - 在数组中a一定在b前边
> - 浏览器会根据回调函数的返回值来决定元素的顺序:
>   - 如果返回一个大于0的值，则元素会交换位置
>   - 如果返回一个小于0的值，则元素位置不变
>   - 如果返回一个0，则认为两个元素相等，也不交换位置
>
> ```
> var arr = [5,4,2,1,3,6,8,7,11];
> arr.sort(function(a,b){
> 	// 升序排列：数组中前面的数a比后面的数b大，要换位
> 	// 数组中前面的数a减后面的数b大于0 ，换位
> 	return a - b;
> });
> console.log(arr);//[1, 2, 3, 4, 5, 6, 7, 8, 11]
> ```
>
> - 升序排列，则返回 a-b
> - 降序排列，则返回b-a

### 10. call() 和 apply()

> - 这两个方法都是函数对象的方法，需要通过函数对象来调用
> - 当对函数调用call()和apply()都会调用函数执行

```
function fun(){
	console.log(this);
}
var obj = {
	name:"obj"
}
fun();// window 对象
fun.call(obj);// obj 对象
fun.apply(obj);// obj 对象
```

> - 在调用call()和apply()可以将一个对象指定为第一个参数
>   - 此时这个对象将会成为函数执行时的this
> - call()方法可以将实参在对象之后依次传递
> - apply()方法需要将实参封装到一个数组中统一传递

```
function fun(a,b){
	console.log(this,a,b);
}
var obj1 = {
	name:"obj1"
}
var obj2 = {
	name:"obj2"
}
fun.call(obj1,"hebe","330");//{name: "obj1"}name: "obj1"__proto__: Object "hebe" "330"
fun.apply(obj2,["dx","16"]);//{name: "obj2"} "dx" "16"
```

- this 的情况：
  1. 函数形式调用时，this永远都是window
  2. 以方法的形式调用时，this是调用方法的对象
  3. 以构造函数的形式调用时，this是新创建的那个对象
  4. 使用call和apply调用时，this是指定的那个对象

### 11. arguments 对象

> - 在调用函数时，浏览器每次都会传递进两个隐含的参数：
>   1. 函数的上下文对象 this
>   2. 封装实参的对象 arguments

- arguments是一个类数组对象,它也可以通过索引来操作数据，也可以获取长度
  - arguments.length可以用来获取实参的长度

```
function fun(a,b){
	console.log(arguments.length);//3
}
fun("dx","2","16");
```

- 在调用函数时，我们所传递的实参都会在arguments中保存
  - arguments[0] 表示第一个实参
  - arguments[1] 表示第二个实参 。。。

```
function fun(a,b){
	console.log(arguments[0]);//dx
}
fun("dx");
```

**callee 属性**

- arguments有一个属性 callee
- 这个属性对应一个函数对象，就是当前正在指向的函数的对象

```
function fun(a,b){
	console.log(arguments.callee === fun);//true
}
fun();
```

### 12. Date 对象

- 在JS中使用Date对象来表示一个时间

> - 创建一个Date对象
>
> ```
> var d = new Date();
> console.log(d);//Thu Jan 21 2021 14:45:09 GMT+0800 (中国标准时间)
> ```
>
> - 如果直接使用构造函数创建一个Date对象，则会封装为当前代码执行的时间

------

> - 创建一个指定的时间对象
> - 需要在构造函数中传递一个表示时间的字符串作为参数
> - 日期的格式  月份/日/年 时:分:秒
>
> ```
> var d = new Date("2/18/2011 11:10:30");
> console.log(d);//Fri Feb 18 2011 11:10:30 GMT+0800 (中国标准时间)
> ```

##### 12.1 Date 对象的方法

> - getDate()
>   - 获取当前日期对象是几日
>
> ```
> var d = new Date();
> var date = d.getDate();
> console.log(d);//Thu Jan 21 2021 14:49:20 GMT+0800 (中国标准时间)
> console.log(date);//21
> ```

------

> - getDay()
>   - 获取当前日期是周几
>   - 会返回一个0-6的值
>     - 0 表示周日
>
> ```
> var d = new Date();
> var day = d.getDay();
> console.log(d);//Thu Jan 21 2021 14:51:29 GMT+0800 (中国标准时间)
> console.log(day);//4
> ```

------

> - getMonth()
>   - 获取当前时间对象的月份
>   - 会返回一个0-11的值
>     - 0 表示1月
>
> ```
> var d = new Date();
> var month = d.getMonth();
> console.log(d);//Thu Jan 21 2021 14:57:55 GMT+0800 (中国标准时间)
> console.log(month);//0
> ```

------

> - getFullYear()
>   - 获取当前日期对象的年份
>
> ```
> var d = new Date();
> var year = d.getFullYear();
> console.log(d);//Thu Jan 21 2021 14:59:32 GMT+0800 (中国标准时间)
> console.log(year);//2021
> ```

------

> - getTime()
>   - 获取当前日期对象的时间戳
> - 时间戳：
>   - 指的是从格林威治标准时间的1970年1月1日，0时0分0秒，到当前日期所花费的毫秒数（1秒 = 1000毫秒）
>   - 计算机底层在保存时间时使用都是时间戳
>
> ```
> var d = new Date();
> var time = d.getTime();
> console.log(d);//Thu Jan 21 2021 15:02:53 GMT+0800 (中国标准时间)
> console.log(time);//1611212573777
> ```
>
> - 获取当前的时间戳
>
> ```
> var time = Date.now();
> console.log(time);//1611212672581
> ```

### 13. Math 对象

- Math和其他的对象不同，它不是一个构造函数
- 它属于一个工具类不用创建对象，它里边封装了数学运算相关的属性和方法

> - abs()可以用来计算一个数的绝对值
>
> ```
> console.log(Math.abs(-1));// 1
> ```

------

> - Math.ceil()
>   - 可以对一个数进行向上取整，小数位只要有值就自动进1
>
> ```
> console.log(Math.ceil(2.1));//3
> ```

> - Math.floor()
>   - 可以对一个数进行向下取整，小数部分会被舍掉
>
> ```
> console.log(Math.floor(3.9));//3
> ```

> - Math.round()
>   - 可以对一个数进行四舍五入取整
>
> ```
> console.log(Math.round(3.4));//3
> console.log(Math.round(3.5));//4
> ```

------

> - Math.random()
>
>   - 可以用来生成一个0-1之间的随机数
>
>   - 生成一个0-x之间的随机数
>     - Math.round(Math.random()*x)
>   - 生成一个x-y之间的随机数
>     - Math.round(Math.random()*(y-x)+x)
>
> ```
> console.log(Math.round(Math.random()*8+2));// 2~10
> ```

------

> - max() 可以获取多个数中的最大值
> - min() 可以获取多个数中的最小值

------

> - Math.pow(x,y)
>   - 返回x的y次幂
>
> ```
> console.log(Math.pow(4,2));//16
> ```

------

> - Math.sqrt()
>   - 用于对一个数进行开方运算
>
> ```
> console.log(Math.sqrt(16));//4
> ```

### 14. 包装类

> - 基本数据类型
>   - String Number Boolean Null Undefined
> - 引用数据类型
>   - Object

- 在JS中为我们提供了三个包装类，通过这三个包装类可以将基本数据类型的数据转换为对象
  - String()
    - 可以将基本数据类型字符串转换为String对象
  - Number()
    - 可以将基本数据类型的数字转换为Number对象
  - Boolean()
    - 可以将基本数据类型的布尔值转换为Boolean对象

> - 如果使用基本数据类型的对象，在做一些比较时可能会带来一些不可预期的结果
>
> ```{
> var b = new Boolean(false);
> if(b){
> 	console.log("dx");//dx
> }
> ```

- 方法和属性能添加给对象，但是不能添加给属性
- 当我们对一些基本数据类型的值去调用属性和方法时
  - 浏览器会临时使用包装类将其转换为对象，然后在调用对象的属性和方法
  - 调用完以后，在将其转换为基本数据类型

```
var num = 123;
console.log(typeof num);// Number
console.log(typeof num.toString());// String
```

#### 14.1 字符串的方法

- 在底层字符串是以字符数组的形式保存的

```
var str = "dx";
console.log(str[1]);//x
```

> - length属性
>   - 可以用来获取字符串的长度
>
> ```
> var str = "dx";
> console.log(str.length);//2
> ```

------

> - charAt()
>   - 可以返回字符串中指定位置的字符
>   - 根据索引获取指定的字符
>
> ```
> var str = "dx 16 8";
> var result = str.charAt(4);
> console.log(str);//dx 16 8
> console.log(result);//6
> ```

------

> - charCodeAt()
>   - 获取指定位置字符的字符编码（Unicode编码）
>
> ```
> var str = "dx 16 8";
> var result = str.charCodeAt(4);
> console.log(str);//dx 16 8
> console.log(result);//54
> ```

------

> - String.fromCharCode()
>   - 可以根据字符编码去获取字符
>
> ```
> var result = String.fromCharCode(54);
> console.log(result);//6
> ```

------

> - concat()
>   - 可以用来连接两个或多个字符串
>   - 作用和+一样

------

> - indexOf()
>   - 可以检索一个字符串中是否含有指定内容
>     - 如果字符串中含有该内容，则会返回其第一次出现的索引
>     - 如果没有找到指定的内容，则返回-1
>   - 第二个参数，可以指定开始查找的位置
>
> ```
> var str = "dx8dx16";
> var result = str.indexOf("x");
> console.log(str);//dx8dx16
> console.log(result);//1
> result = str.indexOf("x",2);
> console.log(result);//4
> ```

> - lastIndexOf()
>   - 该方法的用法和indexOf()一样
>   - 不同的是：
>     - indexOf是从前往后找
>     - lastIndexOf是从后往前找
>
> ```
> var str = "dx8dx16";
> var result = str.lastIndexOf("x");
> console.log(str);//dx8dx16
> console.log(result);//4
> result = str.indexOf("x",1);
> console.log(result);//1
> ```

------

> - slice()
>   - 可以从字符串中截取指定的内容
>   - 不会影响原字符串，而是将截取到内容返回
>   - 参数：
>     - 第一个，开始位置的索引（包括开始位置）
>     - 第二个，结束位置的索引（不包括结束位置）
>     - 如果省略第二个参数，则会截取到后边所有的
>     - 也可以传递一个负数作为参数，负数的话将会从后往前计算
>
> ```
> var str = "dx8dx16";
> var result1 = str.slice(1,2);
> var result2 = str.slice(1,-2);
> console.log(str);//dx8dx16
> console.log(result1);//x
> console.log(result2);//dx8dx
> ```

> - substring()
>   - 可以用来截取一个字符串，和slice()类似
>   - 参数：
>     - 第一个：开始截取位置的索引（包括开始位置）
>     - 第二个：结束位置的索引（不包括结束位置）
>   - 不同：
>     - 这个方法不能接受负值作为参数
>     - 如果传递了一个负值，则默认使用0
>     - 如果第二个参数小于第一个，则自动交换

> - substr()
>   - 用来截取字符串
>   - 参数：
>     1. 截取开始位置的索引
>     2. 截取的长度

------

> - split()
>   - 可以将一个字符串拆分为一个数组
>   - 参数：
>     - 需要一个字符串作为参数，将会根据该字符串去拆分数组
>     - 如果传递一个空串作为参数，则会将每个字符都拆分为数组中的一个元素
>
> ```
> var str = "dx-16-8";
> var result = str.split("-");
> console.log(str);//dx-16-8
> console.log(result);//["dx", "16", "8"]
> ```

------

> - toUpperCase()
>   - 将一个字符串转换为大写并返回

> - toLowerCase()
>   - 将一个字符串转换为小写并返回

### 15. 正则表达式

- 正则表达式用于定义一些字符串的规则
- 计算机可以根据正则表达式，来检查一个字符串是否符合规则，将字符串中符合规则的内容提取出来

##### **15.1 使用构造函数创建正则表达式的对象：**

> - 语法：
>   - var 变量 = new RegExp("正则表达式","匹配模式");
> - 使用typeof检查正则对象，会返回object
>
> ```
> var reg = new RegExp("a");
> ```
>
> - 这个正则表达式可以来检查一个字符串中是否含有a
> - 在构造函数中可以传递一个匹配模式作为第二个参数,可以是：
>   - i 忽略大小写
>   - g 全局匹配模式

> - test()
>   - 正则表达式的方法
>   - 可以用来检查一个字符串是否符合正则表达式的规则
>     - 符合返回 true
>     - 不符合返回 false
>
> ```
> var reg = new RegExp("ab");
> console.log(reg.test("ac"));// false
> ```

------

##### **15.2 使用字面量创建正则表达式：**

> - 语法：
>   - var 变量 = /正则表达式/匹配模式
> - 使用字面量的方式创建更加简单
> - 使用构造函数创建更加灵活
>
> ```
> var reg = /a/;
> console.log(reg.test("ac"));// true
> ```
>
> - 判断字符串中是否含有a

##### 15.3 常用规则

> -  | 表示或者的意思
>
> ```
> var reg = /a|b/;
> console.log(reg.test("ac"));// true
> console.log(reg.test("dx"));// false
> console.log(reg.test("bg"));// true
> ```
>
> - 判断字符串中是否含有a或b

------

> - [] 里的内容也是或的关系
>
> ```
> var reg = /[ab]/;
> console.log(reg.test("ac"));// true
> console.log(reg.test("dx"));// false
> console.log(reg.test("bg"));// true
> ```
>
> - [a-z] 包含任意小写字母
> - [A-Z] 包含任意大写字母
> - [A-z] 包含任意字母
> - [0-9] 包含任意数字

> - [^ ] 包含除了[]里面的内容
>
> ```
> var reg = /[^abc]/;
> console.log(reg.test("ab"));// false
> console.log(reg.test("dx"));// true
> console.log(reg.test("bc"));// false
> ```

------

> - 量词
>   - 通过量词可以设置一个内容出现的次数
>   - 量词只对它前边的一个内容起作用

> - {n} 正好出现n次
>
> ```
> var reg = /(ab){2}/;
> console.log(reg.test("ab"));// false
> console.log(reg.test("abab"));// true
> ```

> - {m,n} 出现m-n次
>
> ```
> varreg = /ab{1,2}c/;
> console.log(reg.test("ab"));// true
> console.log(reg.test("abab"));// true
> ```

> - {m,} m次以上
> - \+ 至少一个，相当于{1,}
> - \* 0个或多个，相当于{0,}
> - ? 0个或1个，相当于{0,1}

------

> - 检查开头和结尾
>   - ^ 表示开头
>   - $ 表示结尾
>
> ```
> reg = /^a/; //匹配开头的a
> reg = /a$/; //匹配结尾的a
> ```
>
> - 如果在正则表达式中同时使用^ $则要求字符串必须完全符合正则表达式
>
> ```
> var reg = /^a$/;
> console.log(reg.test("aa"));// false
> console.log(reg.test("a"));// true
> ```

------

> - 检查一个字符串中是否含有 .
>   - 在正则表达式中. 表示任意字符
> - 在正则表达式中使用\作为转义字符
>   - \\. 来表示 .
>   - \\\\ 来表示 \\
> - 注意：使用构造函数时，由于它的参数是一个字符串，而\是字符串中转义字符
>   - 如果要使用\则需要使用\\\来代替

------

> - \w
>   - 任意字母、数字、_  [A-z 0-9_]
> - \W
>   - 除了字母、数字、_  \[^A-z 0-9_]
> - \d
>   - 任意的数字 [0-9]
> - \D
>   - 除了数字\[^0-9]

> - \s
>   - 空格
> - \S
>   - 除了空格

> - \b
>   - 单词边界
> - \B
>   - 除了单词边界
> - 创建一个正则表达式检查一个字符串中是否含有单词child
>
> ```
> var str = "children hi";
> var reg1 = /\bchild\b/;
> var reg2 = /child/;
> console.log(reg1.test(str));// false
> console.log(reg2.test(str));// true
> ```

#### 15.4 支持正则表达式的String方法

> - split()
>   - 可以将一个字符串拆分为一个数组
>   - 方法中可以传递一个正则表达式作为参数，这样方法将会根据正则表达式去拆分字符串
>   - 这个方法即使不指定全局匹配，也会全都拆分
>
> ```
> var str = "ab1cd3efg4hi5j6k";
> var result = str.split(/\d/);
> console.log(result);//["ab", "cd", "efg", "hi", "j", "k"]
> ```

------

> - search()
>   - 可以搜索字符串中是否含有指定内容
>   - 如果搜索到指定内容，则会返回第一次出现的索引
>   - 如果没有搜索到返回-1
>   - 它可以接受一个正则表达式作为参数，然后会根据正则表达式去检索字符串
>   - search()只会查找第一个，即使设置全局匹配也没用
> - 搜索字符串中是否含有aba 或 aaa 或 aca
>
> ```
> var str = "abab23jion";
> var result = str.search(/a[abc]a/);
> console.log(result);// 0
> ```

------

> - match()
>   - 可以根据正则表达式，从一个字符串中将符合条件的内容提取出来
>   - 默认情况下我们的match只会找到第一个符合要求的内容，找到以后就停止检索
>   - 我们可以设置正则表达式为全局匹配模式，这样就会匹配到所有的内容
>   - match()会将匹配到的内容封装到一个数组中返回，即使只查询到一个结果
>
> ```
> var str = "1a2a3a4a5e6f7A8B9C";
> var result = str.match(/[a-z]/ig);
> console.log(result);//["a", "a", "a", "a", "e", "f", "A", "B", "C"]
> ```

------

> - replace()
>   - 可以将字符串中指定内容替换为新的内容
>   - 参数：
>     1. 被替换的内容，可以接受一个正则表达式作为参数
>     2. 新的内容
>   - 默认只会替换第一个
>
> ```
> var str = "dx1hebbe2dss";
> var result =  str.replace(/\d/,"-");
> console.log(result);//dx-hebbe2dss
> console.log(str.replace(/\d/g,"-"));//dx-hebbe-dss
> ```

> - 去除掉字符串中的前后的空格
> - 使用""来替换空格
>
> ```
> var str = "    hi dx  ";
> console.log(str);//    hi dx  
> console.log(str.replace(/^\s*|\s*$/g,""));//hi dx
> ```

## DOM

- DOM，全称Document Object Model文档对象模型
  - 文档：文档表示的就是整个的HTML网页文档
  - 对象：对象表示将网页中的每一个部分都转换为了一个对象
  - 模型：使用模型来表示对象之间的关系，这样方便获取对象
- 节点Node：是构成我们网页的最基本的组成部分，网页中的 每一个部分都可以称为是一个节点
  - html标签、属性、文本、注释、整个文档等都是一个节点
- 常用节点：
  - 文档节点：整个HTML文档
    - 文档节点document，代表的是整个HTML文档，网页中的所有节点都是它的子节点
    - document对象作为window对象的属性存在的，不用获取可以直接使用
    - 通过该对象可以在整个文档访问内查找节点对象，并可以通过该对象创建各种节点对象
  - 元素节点：HTML文档中的HTML标签
    - HTML中的各种标签都是元素节点
    - 浏览器会将页面中所有的标签都转换为一个元素节点
    - 可以通过document的方法来获取元素节点
  - 属性节点：元素的属性
    - 属性节点表示的是标签中的一个一个的属 性
    - 属性节点并非是元素节点的子节点
    - 是元素节点的一部分
    - 可以通过元素节点来获取指定的属性节点
  - 文本节点：HTML标签中的文本内容
    - 文本节点表示的是HTML标签以外的文本内容，任意非HTML的文本都是文本节点
    - 它包括可以字面解释的纯文本内容
    - 文本节点一般是作为元素节点的子节点存在的
    - 获取文本节点时，一般先要获取元素节点，再通过元素节点获取文本 节点
- 浏览器已经为我们提供文档节点对象,这个对象是window属性
- 可以在页面中直接使用，文档节点代表的是整个网页

> - 文档的加载
>   - 浏览器在加载一个页面时，是按照自上向下的顺序加载的
>   - 读取到一行就运行一行
>     - 如果将script标签写到页面的上边，在代码执行时，页面还没有加载
>     - 页面没有加载DOM对象也没有加载，会导致无法获取到DOM对象
> - onload事件会在整个页面加载完成之后才触发
> - 为window绑定一个onload事件
>   - 该事件对应的响应函数将会在页面加载完成之后执行
>   - 这样可以确保代码执行时所有的DOM对象已经加载完毕了
>
> ```
> window.onload = function(){
> 	//js代码
> }
> ```

### 1. DOM 查询

#### 1.1 获取元素节点

- 通过document对象调用

> - getElementById()
>   - 通过id属性获取一个元素节点对象
>
> ```
> var prev = document.getElementById("prev");
> ```

------

> - getElementsByTagName()
>   - 通过标签名获取一组元素节点对象
>   - 会返回一个类数组对象，所有查询到的元素都会封装到对象中
>   - 即使查询到的元素只有一个，也会封装到数组中返回

------

> - getElementsByName()
>   - 通过name属性获取一组元素节点对象
>
> ```
> var inputs = document.getElementsByName("gender");
> ```

------

> - innerHTML
>   - 用于获取元素内部的HTML代码的
>   - 对于自结束标签，这个属性没有意义
> - 读取元素节点属性:
>   - 元素.属性名
>     - 元素.id 元素.name 元素.value
>   - 注意：class属性不能采用这种方式
>     - 读取class属性时需要使用 :元素.className
>
> ```
> inputs[0].className
> ```

#### 1.2 获取元素节点的子节点

- 通过具体的元素节点调用

> - getElementsByTagName()
>   - 方法，返回当前节点的指定标签名后代节点

> - childNodes
>   - 属性，表示当前节点的所有子**节点**
>   - childNodes属性会获取包括文本节点在呢的所有节点
>   - 根据DOM标签标签间空白也会当成文本节点
> - children
>   - children属性可以获取当前元素的所有**子元素**
> - firstChild
>   - firstChild可以获取到当前元素的第一个子**节点**（包括空白文本节点）
> - firstElementChild
>   - firstElementChild获取当前元素的第一个**子元素**
> - lastChild
>   - lastChild可以获取到当前元素的最后一个子**节点**（包括空白文本节点）

#### 1.3 获取父节点和兄弟节点

> - parentNode
>   - 表示当前节点的父节点
> - previousSibling
>   - 表示当前节点的前一个兄弟节点
>   - 也可能获取到空白的文本
> - previousElementSibling
>   - 获取前一个兄弟元素
> - nextSibling
>   - 表示当前节点的后一个兄弟节点
>   - 也可能获取到空白的文本
> - nextSibling
>   - 获取后一个兄弟元素

------

> - innerHTML
>
>   - 用于获取元素内部的HTML代码的
>
>   - 对于自结束标签，这个属性没有意义
>
> - innerText
>
>   - 该属性可以获取到元素内部的文本内容
>   - 它和innerHTML类似，不同的是它会自动将html去除

#### 1.4 其他属性和方法

属性：

> - 获取html标签
>   - 在document中有一个属性documentElement，它保存的是html的引用
>
> ```
> document.documentElement
> document.getElementsByTagName("html")[0]
> ```

> - 获取body标签
>   - 在document中有一个属性body，它保存的是body的引用
>
> ```
> document.body
> document.getElementsByTagName("body")[0]
> ```

> - 获取页面中所有元素
>   - 在document中有一个属性all，它保存的是页面中所有元素
>
> ```
> document.all
> document.getElementsByTagName("*")
> ```

------

方法：

> - getElementsByClassName()
>   - 可以根据class属性值获取一组元素节点对象
>   - 该方法不支持IE8及以下的浏览器
>
> ```
> document.getElementsByClassName("box1")
> ```

> - querySelector()
>   - 需要一个选择器的字符串作为参数，可以根据一个CSS选择器来查询一个元素节点对象
>   - 该方法总会返回唯一的一个元素
>   - 如果满足条件的元素有多个，也只会返回第一个
>
> ```
> docum.querySelect(".box1")
> ```

> - querySelectorAll()
>   - 该方法和querySelector()用法类似
>   - 不同的是它会将符合条件的元素封装到一个数组中返回
>   - 即使符合条件的元素只有一个，它也会返回数组
>
> ```
> docum.querySelectAll(".box1")
> ```

### 2. DOM 增删改

> - createElement()
>   - 可以用于创建一个元素节点对象
>   - 需要一个标签名作为参数，将会根据该标签名创建元素节点对象
>   - 并将创建好的对象作为返回值返回
>
> ```
> var li = document.createElement("li")
> ```

> - createTextNode()
>   - 可以用来创建一个文本节点对象
>   - 需要一个文本内容作为参数，将会根据该内容创建文本节点
>   - 并将新的节点返回
>
> ```
> var text = document.createTextNode("dx")
> ```

> - appendChild()
>   - 向一个父节点中添加一个新的子节点
>   - 语法：
>     - 父节点.appendChild(子节点)
>
> ```
> li.appendChild(text);
> ```

```
var father = document.getElementById("father");
var li document.createElement("li");
li.innerHTML = "dx";
father.appendChild(li);
```

> - insertBefore()
>   - 在指定的子节点前插入新的子节点
>   - 语法：
>     - 父节点.insertBefore(新节点,旧节点)

------

> - replaceChild()
>   - 可以使用指定的子节点替换已有的子节点
>   - 语法：
>     - 父节点.replaceChild(新节点,旧节点)

------

> - removeChild()
>   - 可以删除一个子节点
>   - 语法：
>     - 父节点.removeChild(子节点)
>     - 子节点.parentNode.removeChild(子节点)

### 3. 修改CSS样式

> - 读取元素的样式:
>   - 语法：
>     - 元素.style.样式名
>   - 通过style属性设置和读取的都是内联样式
>     - 无法读取样式表中的样式

> - 通过JS修改元素的样式：
>   - 语法：
>     - 元素.style.样式名 = 样式值
>   - 注意：如果CSS的样式名中含有-，在JS中是不合法的比如background-color
>     - 需要将这种样式名修改为驼峰命名法：去掉-，然后将-后的字母大写
>   - 通过style属性设置的样式都是内联样式
>     - 但是如果在样式中写了!important，则此时样式会有最高的优先级
>     - 通过JS也不能覆盖该样式，此时将会导致JS修改样式失效

------

> - 获取元素的当前显示的样式:
>   - 语法：
>     - 素.currentStyle.样式名
>   - 可以用来读取当前元素正在显示的样式
>     - 如果当前元素没有设置该样式，则获取它的默认值
>   - currentStyle只有IE浏览器支持，其他的浏览器都不支持

> - getComputedStyle()
>   - 这个方法来获取元素当前的样式
>   - 这个方法是window的方法，可以直接使用
>   - 需要两个参数：
>     - 第一个：要获取样式的元素
>     - 第二个：可以传递一个伪元素，一般都传null
>   - 该方法会返回一个对象，对象中封装了当前元素对应的样式
>   - 可以通过对象.样式名来读取样式
>   - 如果获取的样式没有设置，则会获取到真实的值，而不是默认值
>     - 没有设置width，它不会获取到auto，而是一个长度
> - 该方法不支持IE8及以下的浏览器

- 通过currentStyle和getComputedStyle()读取到的样式都是只读的，不能修改
- 如果要修改必须通过style属性

> - 兼容浏览器
>
> ```
> // obj 要获取样式的元素
> // name 要获取的样式名
> fun getStyle(obj,name){
> 	if(window.getComputedStyle){
> 		return obj.getComputedStyle(obj,null)[name];
> 	}else{
> 		return obj.currentStyle[name];
> 	}
> }
> ```
>

------

> - clientWidth
> - clientHeight
>   - 这两个属性可以获取元素的可见宽度和高度
>   - 这些属性都是不带px的，返回都是一个数字，可以直接进行计算
>   - 会获取元素宽度和高度，包括内容区和内边距
>   - 这些属性都是只读的，不能修改

> - offsetWidth
> - offsetHeight
>   - 获取元素的整个的宽度和高度，包括内容区、内边距和边框
> - offsetParent
>   - 可以用来获取当前元素的定位父元素
>   - 会获取到离当前元素最近的开启了定位的祖先元素
>   - 如果所有的祖先元素都没有开启定位，则返回body
> - offsetLeft
>   - 当前元素相对于其定位父元素的水平偏移量
> - offsetTop
>   - 当前元素相对于其定位父元素的垂直偏移量

> - scrollWidth
> - scrollHeight
>   - 可以获取元素整个滚动区域的宽度和高度
> - scrollLeft
>   - 可以获取水平滚动条滚动的距离
> - scrollTop
>   - 可以获取垂直滚动条滚动的距离
>
> ```
> //说明垂直滚动条滚动到底了
> scrollHeight - scrollTop == clientHeight
> ```
>
> ```
> //说明水平滚动条滚动到底
> scrollWidth - scrollLeft == clientWidth
> ```
>

## 事件

- 当事件的响应函数被触发时，浏览器每次都会将一个事件对象作为实参传递进响应函数
- 在事件对象中封装了当前事件相关的一切信息，比如：鼠标的坐标
- 在IE8中，响应函数被处罚时，浏览器不会传递事件对象
  - 是将事件对象作为window对象的属性保存的

```
body.onmousemove = function(event){
	// 解决事件对象的兼容性问题
	event = event || window.event;
}
```

> - clientX和clientY
>   - 用于获取鼠标在当前的可见窗口的坐标
> - pageX和pageY
>   - 可以获取鼠标相对于当前页面的坐标
>     - 在IE8中不支持

### 1. 冒泡

- 指的就是事件的**向上传导**，当后代元素上的事件被触发时，其祖先元素的**相同事件**也会被触发
- 如果不希望发生事件冒泡可以通过事件对象来取消冒泡
  - 可以将事件对象的cancelBubble设置为true，即可取消冒泡

```
div.onclick = function(event){
	event = event || window.event;
	event.cancleBubble = true;
}
```

### 2. 委派

- 指将事件统一绑定给元素的共同的祖先元素
- 当后代元素上的事件触发时，会一直冒泡到祖先元素
  - 通过祖先元素的响应函数来处理事件
  - 事件委派是利用了冒泡，通过委派可以减少事件绑定的次数，提高程序的性能
- 因为绑定的是祖先元素，所有点击子元素都会冒泡到父元素，需要对触发事件进行判断

> - target
>   - event中的target表示的触发事件的对象

```
<button id="btn">添加超链接</button>
<ul id="ul">
	<li><p><span>123</span></p></li>
	<li><p><a href="#" class="link">超链接</a></p></li>
	<li><p><a href="#" class="link">超链接</a></p></li>
	<li><p><a href="#" class="link">超链接</a></p></li>
</ul>
```

```
var btn = document.getElementById("btn");
var ul = document.getElementById("ul");
btn.onclick = function(){
	var li = document.createElement("li");
	li.innerHTML = "<p><a href='#'' class='link'>新超链接</a></p>"
	ul.appendChild(li);
}
ul.onclick = function(event){
	event = event || window.event;
	if(event.target.className == "link"){
		alert("===");
	}
}
```

### 3. 绑定

> - 使用 对象.事件 = 函数 的形式绑定响应函数
>   - 只能同时为一个元素的一个事件绑定一个响应函数
>   - 不能绑定多个，如果绑定了多个，则后边会覆盖掉前边的

- addEventListener()

  - 可以为元素绑定响应函数

  - 参数：

    1. 事件的字符串，不要on

    2. 回调函数，当事件触发时该函数会被调用
    3. 是否在捕获阶段触发事件，需要一个布尔值，一般都传false

  - 使用addEventListener()可以同时为一个元素的相同事件同时绑定多个响应函数

  - 当事件被触发时，响应函数将会按照函数的绑定顺序执行

  - 不支持IE8及以下的浏览器

```
var btn = document.getElementById("btn");
btn.addEventListener("click", function(){
		alert(this);// 绑定事件的对象
}, false)
```

- attachEvent()
  - 在IE8中可以使用attachEvent()来绑定事件
  - 参数：
    1. 事件的字符串，要on
    2. 回调函数
  - 这个方法也可以同时为一个事件绑定多个处理函数
  - 不同的是它是后绑定先执行，执行顺序和addEventListener()相反

```
var btn = document.getElementById("btn");
btn.attachEvent("onclick", function(){
		alert(this);// window 对象
})
```

> - 兼容
>
> ```
> /*
>  * 参数：
>  * 	obj 要绑定事件的对象
>  * 	eventStr 事件的字符串(不要on)
>  *  callback 回调函数
>  */
> function bind(obj,EventStr,callback){
> 	if(obj.addEventListener) {
> 		obj.addEventListener(EventStr, callback, false)
> 	}else {
> 		obj.attachEvent("on"+EventStr,function(){
> 			callback.call(obj);
> 		})
> 	}
> }
> var btn = document.getElementById("btn");
> bind(btn,"click",function(){
> 	alert(this);
> });
> ```

### 4. 传播

- W3C将事件传播分成了三个阶段：
  1. 捕获阶段
     - 在捕获阶段时从最外层的祖先元素，向目标元素进行事件的捕获，但是默认此时不会触发事件
  2. 目标阶段
     - 事件捕获到目标元素，捕获结束开始在目标元素上触发事件
  3. 冒泡阶段
     - 事件从目标元素向他的祖先元素传递，依次触发祖先元素上的事件
- 如果希望在捕获阶段就触发事件，可以将addEventListener()的第三个参数设置为true

### 5. 键盘事件

- onkeydown
  - 按键被按下
  - 对于onkeydown来说如果一直按着某个按键不松手，则事件会一直触发
  - 当onkeydown连续触发时，第一次和第二次之间会间隔稍微长一点，其他的会非常的快
    - 这种设计是为了防止误操作的发生
- onkeyup
  - 按键被松开
- 键盘事件一般都会绑定给一些可以获取到焦点的对象或者是document

> - keyCode
>   - 获取按键的编码
> - altKey
> - ctrlKey
> - shiftKey
>   - 这个三个用来判断alt ctrl 和 shift是否被按下
>   - 如果按下则返回true，否则返回false
>
> - 判断y和ctrl是否同时被按下
>
> ```
> event.keyCode === 89 && event.ctrlKey
> ```

- 在文本框中输入内容，属于onkeydown的默认行为
  - 如果在onkeydown中取消了默认行为，则输入的内容，不会出现在文本框中

## BOM

- 浏览器对象模型
- BOM可以使我们通过JS来操作浏览器
- 在BOM中为我们提供了一组对象，用来完成对浏览器的操作
  - Window
    - 代表的是整个浏览器的窗口，同时window也是网页中的全局对象
  - Navigator
    - 代表的当前浏览器的信息，通过该对象可以来识别不同的浏览器
  - Location
    - 代表当前浏览器的地址栏信息，通过Location可以获取地址栏信息，或者操作浏览器跳转页面
  - History
    - 代表浏览器的历史记录，可以通过该对象来操作浏览器的历史记录
    - 由于隐私原因，该对象不能获取到具体的历史记录，只能操作浏览器向前或向后翻页
  - Screen
    - 代表用户的屏幕的信息，通过该对象可以获取到用户的显示器的相关的信息
- 这些BOM对象在浏览器中都是作为window对象的属性保存的，可以通过window对象来使用，也可以直接使用

### 1. Navigator

- 由于历史原因，Navigator对象中的大部分属性都已经不能帮助我们识别浏览器了

> - 一般我们只会使用userAgent来判断浏览器的信息，不同的浏览器会有不同的userAgent
> - userAgent是一个字符串，这个字符串中包含有用来描述浏览器信息的内容
>
> ```
> navigator.appName
> ```
>
> - 如果通过userAgent不能判断，还可以通过一些浏览器中特有的对象，来判断浏览器的信息
> - 比如：ActiveXObject

### 2. History

- length
  - 属性，可以获取到当前访问的链接数量
- back()
  - 可以用来回退到上一个页面，作用和浏览器的回退按钮一样
- forward()
  - 可以跳转下一个页面，作用和浏览器的前进按钮一样
- go()
  - 可以用来跳转到指定的页面
  - 它需要一个整数作为参数
    - 1:表示向前跳转一个页面 相当于forward()
    - 2:表示向前跳转两个页面
    - -1:表示向后跳转一个页面
    - -2:表示向后跳转两个页面

### 3. Location

- 如果直接打印location，则可以获取到地址栏的信息（当前页面的完整路径）

- 如果直接将location属性修改为一个完整的路径，或相对路径
  - 则我们页面会自动跳转到该路径，并且会生成相应的历史记录

```
location = "http://www.baidu.com";
```

- assign()
  - 用来跳转到其他的页面，作用和直接修改location一样

```
location.assign("http://www.baidu.com");
```

- reload()
  - 用于重新加载当前页面，作用和刷新按钮一样
  - 如果在方法中传递一个true，作为参数，则会强制清空缓存刷新页面
- replace()
  - 可以使用一个新的页面替换当前页面，调用完毕也会跳转页面
  - 不会生成历史记录，不能使用回退按钮回退

### 4. 定时调用

- 如果希望一段程序，可以每间隔一段时间执行一次，可以使用定时调用
- setInterval()
  - 定时调用
  - 可以将一个函数，每隔一段时间执行一次
  - 参数：
    1. 回调函数，该函数会每隔一段时间被调用一次
    2. 每次调用间隔的时间，单位是毫秒
  - 返回值：
    - 返回一个Number类型的数据
    - 这个数字用来作为定时器的唯一标识
- clearInterval()
  - 用来关闭一个定时器
  - 方法中需要一个定时器的标识作为参数，这样将关闭标识对应的定时器

### 5. 延时调用

- 延时调用一个函数不马上执行，而是隔一段时间以后在执行，而且只会执行一次
- 延时调用和定时调用的区别，定时调用会执行多次，而延时调用只会执行一次
- 延时调用和定时调用实际上是可以互相代替的

```
var timer = setTimeout(function(){
	console.log(num++);
},3000);
```

- clearTimeout()来关闭一个延时调用

```
clearTimeout(timer);
```

### 6. JSON

> - JSON就是一个特殊格式的字符串，这个字符串可以被任意的语言所识别
> - 可以转换为任意语言中的对象，JSON在开发中主要用来数据的交互

- JSON
  - JavaScript Object Notation JS对象表示法
  - JSON和JS对象的格式一样，只不过JSON字符串中的属性名必须加双引号，其他的和JS语法一致
  - JSON分类：
    1. 对象 {}
    2. 数组 []
  - JSON中允许的值：
    - 字符串
    - 数值
    - 布尔值
    - null
    - 对象
    - 数组

#### 6.1 json 转 js对象

- JSON.parse()
  - 可以将以JSON字符串转换为js对象
  - 它需要一个JSON字符串作为参数，会将该字符串转换为JS对象并返回

```
var json = '{"name":"hebe","number":330}';
var obj = JSON.parse(json);
console.log(obj.name);//hebe
```

#### 6.2 js对象 转 json

- JSON.stringify()
  - 可以将一个JS对象转换为JSON字符串
  - 需要一个js对象作为参数，会返回一个JSON字符串

```
var obj = {name:"dx",number:16};
var json = JSON.stringify(obj);
```

#### 6.3 eval()

- 这个函数可以用来执行一段字符串形式的JS代码，并将执行结果返回

```
var str2 = "alert('hello');";
eval(str2);
```

- 如果使用eval()执行的字符串中含有{},它会将{}当成是代码块
  - 如果不希望将其当成代码块解析，则需要在字符串前后各加一个()

```
var json = '{"name":"hebe","number":330}';
var obj = eval("("+json+")");
```

- eval()这个函数的功能很强大，可以直接执行一个字符串中的js代码,但是它的执行性能比较差，然后它还具有安全隐患



