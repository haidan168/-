# ES 6

## 1. 作用域

### let

- 使用声明变量和var类似
- let的特点：
  - 变量不能重复声明
  - 使用let声明的变量具有块级作用域
  - 不存在变量提升
  - 不影响作用域链

```
{
	let name = "dx";
	function fun(){
		console.log(name);// dx
	}
	fun()
}
```

### const

- 使用声明变量和var类似
- const的特点：
  - 一定要赋初始值
  - 一般常量使用大写(潜规则)
  - 块儿级作用域
  - 对于数组和对象的元素修改, 不算做对常量的修改, 不会报错
    - 修改对象不会改变常量中的地址值

## 2. 数组

### 2.1 数组遍历

- for()

```
const arr = [1, 2, 3, 4, 5]
for (let i = 0; i < arr.length; i++) {
  if (arr[i] === 2) {
    continue
  }
  // console.log(arr[i])
}
```

- forEach()
  - 不能使用break和continue
  - 循环会一口气执行完

```
arr.forEach(function (item) {
  // console.log(item)
})
```

- every()

  - 方法默认返回false

  - 返回false表示循环执行结束
  - 返回true循环将会继续执行

```
arr.every(function (item) {
  if (item === 2) {

  } else {
    // console.log(item)
  }
  return true
})

```

- for in
  - 这个方法是为对象准备的
  - 数组也可以使用，但是会出现问题
  - 该方法可以使用break和continue控制循环
  - index是字符串

```
const arr = [1,2,3,4,5]
arr.a = 8
for(let index in arr){
	if(index*1 === 2){
		continue
	}
	console.log(index, arr[index])
}
打印结果：
0 1
1 2 
2 3
3 4
4 5
a 8
```

```
const obj = {
    name: "dx",
    number: 330
}
for(let key in obj){
    console.log(key,obj[key])
}
打印结果：
name dx
number 330
```

**ES 6新增方法：**

- for of
  - 遍历自定义的数据结构

### 2.2 伪数组转换成数组

- 伪数组：按照索引方式存储数据，具备一个length属性 
- 转换:

```
let imgs = Array.from(document.querySelectorAll('img'))
```

- 使用from进行数组初始化和赋初始值：

```
// Array.from(arrayLike,mapFn,thisArg)
let array = Array.from({ length: 5 }, function () { return 1 })
```

### 2.3 创建数组

- Array.of()
  - 创建数组时，就可以对数组赋值

```
let obj = {
    name: "dx",
    num: 16
}
let array = Array.of(1,obj,"hebe")
console.log(array)// [1, {…}, "hebe"]
```

- Array.fill()

```
let array = Array(3).fill(2)
console.log(array)// [2,2,2]
```

- 该方法也可以修改数组的值
  - 参数：
    1. 替换的值
    2. 开始的index（包括）
    3. 结束的index（不包括）

```
let obj = {
    name: "dx",
    num: 16
}
let array = Array(3).fill(2)
console.log(array)// [2,2,2]
console.log(array.fill(obj,1,2))// [2, {…}, 2]
```

### 2.4 查找元素

- filter()
  - 返回符合条件的数组
  - 没找到则返回空数组

```
let array = [1,2,3,4,5]
let find = array.filter(function(item){
    return item%2 === 0
})
let find2 = array.filter(function(item){
    return item === 6
})
console.log(find)// [2,4]
console.log(find2)// []
```

- find()
  - 找满足条件的第一个值，返回并且不继续找了
  - 没找到返回undefined

```
let array = [1,2,3,4,5]
let find = array.find(function(item){
    return item%2 === 0
})
let find2 = array.find(function(item){
    return item === 6
})
console.log(find,typeof find)// 2 "number"
console.log(find2)// undefined
```

- findIndex()
  -  查找第一满足条件的值得index
  - 没找到返回-1

```
let array = [1,2,3,4,5]
let find = array.findIndex(function(item){
    return item%2 === 0
})
let find2 = array.findIndex(function(item){
    return item === 6
})
console.log(find)// 1
console.log(find2)// -1
```

## 3. 函数

### 3.1 类的声明

- es 5
  - 通过原型链声明类

```
function Person(name){
	this.name = name
}
Person.prototype.showName = function(){
	console.log("最佳二传")
}
let dx = new Person("dx")
dx.showName()// 最佳二传
console.log(Person.prototype.constructor)// f Person(name){}
console.log(dx.constructor)// f Person(name){}
```

- es 6
  - 语法糖
  - constructor 中存放属性
  - 方法需要放在构造函数外
  - 和es 5本质是一样的

```
class Person{
	constructor(name){
		this.name = name
	}
	showName(){
		console.log("最佳二传")
	}
}
let dx = new Person("dx")
dx.showName()// 最佳二传
console.log(Person.prototype.constructor)// class Person
console.log(dx.constructor)// class Person
console.log(typeof Person)// function
```

### 3.2 读写属性

- get 
  - 写在构造函数外，添加之后就会变成类的属性
  - 只可以读数据，无法对数据进行修改
- set
  - 写在构造函数外，可以对私有属性进行修改

```
let number = 8
class Animal{
	constructor(type){
		this.type = type
	}
	get num(){
		return number
	}
	set num(val){
		if(val>2){
			number = val
		}
	}
}
let dog = new Animal("dog")
console.log(dog.num)// 8
console.log(dog.number)// undefined
dog.num = 16
console.log(number)// 16
console.log(dog.num)// 16
```

### 3.3 静态方法

- 类的静态方法拿不到当前的实例对象

- es 5

```
function Person(name){
	this.name = name;
}
Person.prototype.show = function(){
	Person.showMsg()
	console.log(this.name)
}
Person.showMsg = function(){
	console.log("最佳二传")
}
let dx = new Person("dx")
dx.show()
dx.showMsg()
结果：
最佳二传
dx
dx.showMsg is not a function
```

- es 6
  - 添加了static关键字的方法就是静态方法

```
class Person{
	constructor(name){
		this.name = name
	}
	show(){
 		Person.showMsg()
		console.log(this.name)
	}
	static showMsg(){
		console.log("最佳二传")
		console.log(this)// class Person
	}
}
let dx = new Person("dx")
dx.show()
dx.showMsg()
结果：
最佳二传
class Person
dx
dx.showMsg is not a function
```

### 3.4 继承

- es 5 

```
function Person(name){
	this.name = name;
}
Person.prototype.show = function(){
	Person.showMsg()
	console.log(this.name)
}
Person.showMsg = function(){
	console.log("最佳二传")
}
function Dx(){
	// 使Person中的this指向当前对象，继承父类的属性
	Person.call(this, "dx")
}
// 继承父类的方法
Dx.prototype = Person.prototype
let dx = new Dx()
dx.show()
console.log(dx.name)
```

- es 6

```
class Person{
	constructor(name){
		this.name = name
	}
	show(){
 		Person.showMsg()
		console.log(this.name)
	}
	static showMsg(){
		console.log("最佳二传")
	}
}
```

- 只进行继承不添加属性
  - 可以不用写构造函数（隐式）

```
class Dx extends Person{

}
let dx = new Dx()
dx.show()
结果：
最佳二传
undefined
```

- 添加自己的属性
  - 必须写构造函数（显示），

```
class Dx extends Person{
	// 可以传多个值
	constructor(name){
		// 必须写到最上面
		super(name)
		this.number = 16
	}
}
let dx = new Dx("dx")
dx.show()
console.log(dx.number)
结果：
最佳二传
dx
16
```

### 3.5 函数的参数

- es 6
- 没有默认值的参数必须写在有默认值的参数前
- 需要使用默认值时，传undefined

```
function fun(x,y=2,z=3){
	return x+y+z
}
console.log(fun(1))// 6
console.log(fun(1,1,1))// 3
console.log(fun(1,undefined,1))//4
```

- 默认值也可以是一个表达式

```
function fun(x,y=2,z=x+y){
	return x+z
}
console.log(fun(1))// 4
console.log(fun(1,1,1))// 2
console.log(fun(1,undefined,1))//2
console.log(fun(1,3))//5
```

### 3.6 **rest变量赋值**

- 参数不确定，将参数放入数组

```
let arr = [1,2,3,4,5,6,7];
let [one,two,...last] = arr;
console.log(one);// 1
console.log(two);// 2
console.log(last);// [3, 4, 5, 6, 7]
```

```
function sum(base1,base,...nums) {
    let num = 0;
    // nums是数组
    nums.forEach(function (item) {
        num += item*1;
    })
    return base1*2 + base*2 + num;
}
console.log(sum(1,2,2));// 
```

- 逆运算
  - 参数确定，参数是数组，需要将数组打散

```
function sum (x = 1, y = 2, z = 3) {
  return x + y + z
}
let data = [4, 5, 9]
// console.log(sum(data[0], data[1], data[2]))
// es5:
// console.log(sum.apply(this, data))
// spread
console.log(sum(...data))// 18
```

### 3.7 箭头函数

- ()=>{}
  - ()：函数对应的参数集合
  - {}：函数体
  - 箭头函数this的定义发生了改变
    - 写的时候this的指向，而不是执行的时候this的指向

## 4. 数据结构

### 4.1 Object

- 属性简写
- key值是可变得
- 函数，加 * 表示异步函数（es 6新增）

```
let a = 1,b = 2,name = "dx"
let obj = {
	a,
	b,
	show(){
		console.log(a,b)
	},
	[name]: 16,
	// 异步函数
	* sum(){
		console.log(a+b)
	}
}
obj.show()
console.log(obj)//{a: 1, b: 2, dx: 16, show: ƒ}
```

### 4.2 Set

- Set存储的数据必须是唯一的
- 如果存入了重复的数据会自动过滤
- Set接受的参数是一个可遍历的对象

#### **声明**

```
let s = new Set()
// 声明并赋值
let set = new Set([1,2,3,4])
console.log(set)// Set(4) {1, 2, 3, 4}
```

#### **add()**

- 存数据

```
let s = new Set()
s.add("dx").add("hebe").add("8").add("dx")
console.log(s)// Set(3) {"dx", "hebe", "8"}
```

#### **delete()**

- 删除指定数据

```
let s = new Set()
s.add("dx").add("hebe").add("8").add("dx")
s.delete("hebe")
console.log(s)// Set(2) {"dx", "8"}
```

#### **clear()**

- 全部删除

```
let s = new Set()
s.add("dx").add("hebe").add("8").add("dx")
s.clear()
console.log(s)// Set(0) {}
```

#### **has()**

- 查找数据，存在返回true，不存在返回false

```
let s = new Set()
s.add("dx").add("hebe").add("8").add("dx")
console.log(s.has("dx"))// true
console.log(s.has("2"))// false
```

#### **size属性**

- 查看存储的数据条数

```
let s = new Set()
s.add("dx").add("hebe").add("8").add("dx")
console.log(s.size)// 3
```

#### **读取数据**

- keys()
- values()

```
let s = new Set()
s.add("dx").add("hebe").add("8").add("dx")
console.log(s.keys())// SetIterator {"dx", "hebe", "8"}
console.log(s.values())// SetIterator {"dx", "hebe", "8"}
```

- entries()
  - 返回键值对

```
let s = new Set()
s.add("dx").add("hebe").add("8").add("dx")
console.log(s.entries())// SetIterator {"dx" => "dx", "hebe" => "hebe", "8" => "8"}
```

- forEach()

```
let s = new Set()
s.add("dx").add("hebe").add("8").add("dx")
s.forEach(item => console.log(item))
结果：
dx
hebe
8
```

- for of

```
let s = new Set()
s.add("dx").add("hebe").add("8").add("dx")
for(let item of s){
	console.log(item)
}
结果：
dx
hebe
8
```

- 修改数据
  - 没有提供方法
  - 需要先删除后添加

### 4.3 Map

- 存储顺序是按初始化的顺序

#### **声明**

```
let m = new Map()
// 声明并赋值
let map = new Map([["key","value"],["name","dx"],["number",16]])
console.log(typeof m)// object
console.log(map)// Map(3) {"key" => "value", "name" => "dx", "number" => 16}
```

#### **set()**

- 存数据，既有增加数据的能力，也有修改数据的能力

```
let m = new Map()
m.set("key","value").set("number",16)
console.log(m)// Map(2) {"key" => "value", "number" => 16}
// 修改数据
m.set("number",8)
console.log(m)// Map(2) {"key" => "value", "number" => 8}
```

#### **delete()**

- 删除数据，删除的是指定key

```
let m = new Map([["key","value"],["number",16],["name","dx"]])
console.log(m)// Map(3) {"key" => "value", "number" => 16, "name" => "dx"}
m.delete("key")
console.log(m)// Map(2) {"number" => 16, "name" => "dx"}
```

#### **clear()**

- 清空所有数据

```
let m = new Map([["key","value"],["number",16],["name","dx"]])
console.log(m)// Map(3) {"key" => "value", "number" => 16, "name" => "dx"}
m.clear()
console.log(m)// Map(0) {}
```

#### **size属性**

- 统计数据条数

```
let m = new Map([["key","value"],["number",16],["name","dx"]])
console.log(m.size)// 3
```

#### **has()**

- 查找数据
- 以key为目标查找，key存在返回true，key不存在返回false

```
let m = new Map([["key","value"],["number",16],["name","dx"]])
console.log(m.has("number"))// true
console.log(m.has("age"))// false

```

#### **get()**

- 那某个索引的值
- 参数是key，返回值是value
- 可以不存在，返回undefined

```
let m = new Map([["key","value"],["number",16],["name","dx"]])
console.log(m.get("number"))// 16
console.log(m.get("age"))// undefined
```

#### **keys()**

- 所有索引集合

```
let m = new Map([["key","value"],["number",16],["name","dx"]])
console.log(m.keys())// MapIterator {"key", "number", "name"}
```

#### **values()**

- 所有值的集合

```
let m = new Map([["key","value"],["number",16],["name","dx"]])
console.log(m.values())// MapIterator {"value", 16, "dx"}
```

#### **entries()**

- 键值对集合

```
let m = new Map([["key","value"],["number",16],["name","dx"]])
console.log(m.entries())// MapIterator {"key" => "value", "number" => 16, "name" => "dx"}
```

#### **读取数据**

**forEach()**

- 第一个值是value，第二个值是key

```
let m = new Map([["key","value"],["number",16],["name","dx"]])
m.forEach((value,key)=>console.log(key,value))
结果：
key value
number 16
name dx
```

**for of**

```
let m = new Map([["key","value"],["number",16],["name","dx"]])
for(let [key,value] of m){
	console.log(key,value)
}
结果：
key value
number 16
name dx
```

### 4.4 对象拷贝

**Object. assign()**

- 参数
  1. target
  2. source，需要拷贝的数据

```
let source = {
	person: {
		name: "hebe",
		num: 330
	},
	like: "sing",
	a: 1
}
let target = {}
Object.assign(target,source)
console.log(target)// {person: {…}, like: "sing", a: 1}
console.log(target === source)// false
```

- 浅拷贝
  - 引用类型的值才做数据替换，对于引用类型的值不做遍历，只是将引用类型的地址进行替换

```
let source = {
	person: {
		name: "dx",
		num: 16
	},
	like: "sing",
	a: 1
}
let target = {
	person: {
		name: "hebe",
		num: 330,
		// 浅拷贝后，obj没有了
		obj: {
			name: "dx"
		}
	},
	like: "sing",
	a: 1
}
Object.assign(target,source)
console.log(target)// person: {name: "dx", num: 16}
```

- 如果需要拷贝的数据是null或者undefined，target还是原来的样子

```
let tar1 = {}
let tar2 = {
	name: "dx"
}
console.log(Object.assign(tar1,undefined))// {}
console.log(Object.assign(tar1,null))// {}
console.log(Object.assign(tar2,undefined))// {name: "dx"}
console.log(Object.assign(tar2,null))// {name: "dx"}
```

- 如果target是null或者undefined，会报错

## 5. 解构赋值

- 允许按照一定模式从数组和对象中提取值，对变量进行赋值

**数组解构**

```
const arr = ["dx","16"];
let [name,number] = arr;
console.log(name);// dx
console.log(number)// 16
```

- 跳过不关心的数据进行赋值

```
let arr = ['a', 'b', 'c', 'd']
let [firstName,, thirdName] = arr
console.log(firstName, thirdName)// a c
```

- 右侧支持所有可遍历的对象，String有length可以遍历
- Set和Map也可以遍历

**对象解构**

- 如果是简写，名称必须和对象的属性名一样

```
let obj = {
	name: "dx",
	number: 16,
	showName: function(){
		console.log(name);
	}
}
let{name,number,showName} = obj;
console.log(name);// dx
console.log(number);// 16
showName();// dx
```

- 不使用对象的属性名

```
let obj = {
	name: "dx",
	number: 16,
	showName: function(){
		console.log(name);
	}
}
let {name: name1,number:num} = obj
console.log(name1,num)// dx 16
// 简写
let {n1,n2} = obj
console.log(n1,n2)// undefined undefiend
```

- 修改对象的值

```
let obj = {
	name: "dx",
	number: 16
};
[obj.name,obj.number] = ["hebe",330];
console.log(obj);//{name: "hebe", number: 330}
```

- 取嵌套的内容
  - 左侧声明变量的结构要和右侧对象的结构一致

```
let options = {
  size: {
    width: {
      size: {
        width: 200
      }
    },
    height: 200
  },
  items: ['Cake', 'Donut'],
  extra: true
}
let { size: { width:{size: {width} }, height }, items: [, item2], extra } = options
console.log(width, height, item2, extra)
// 200 200 "Donut" true
```

**rest变量赋值**

```
let arr = [1,2,3,4,5,6,7];
let [one,two,...last] = arr;
console.log(one);// 1
console.log(two);// 2
console.log(last);// [3, 4, 5, 6, 7]
```

## 6. 模板字符串

- ES 6 引入新的声明字符串的方式 『``』 '' "" 
- 内容中可以直接出现换行符

```
let str = `是字符串类型`;
console.log(str,typeof str);// 是字符串类型 string
```

- 内容中可以直接出现换行符

```
let str = `<ul>
				<li>hebe</li>
		   </ul>`
```

- 变量拼接

```
let name = "dx";
let str = `${name}世界杯最佳二传`;
console.log(str);// dx世界杯最佳二传
```

- 包含变量或表达式

```
function Price(strings,type) {
    let s1 = strings[0];
    let s2 = strings[1];
    const retailPrice = 20;
    const wholeSalePrice = 16;
    let showTxt;
    if(type === 'retail'){
        showTxt = '购买单价是：' + retailPrice;
    }else{
        showTxt = '购买的批发价是：' + wholeSalePrice;
    }
    return `${s1}${showTxt}${s2}`
}
let showTxt = Price`你此次的${'retail'} 元`;
console.log(showTxt);// 你此次的购买单价是：20 元
```

## 7. Promise

- 解决异步回调问题
  - 异步操作不会立马执行，会放到异步队列中
  - 优先同步操作，同步操作完成后才会执行异步操作
  - 如果想同步操作和异步操作一起，按一定顺序执行需要使用回调函数

### 7.1 创建

- Promise有状态和结果
- 通过new创建Promise对象时
  - 状态：pending
  - 结果：undefined
- resolve()和reject()方法可以改变Promise的状态和结果
- resolve()和reject()方法是不可逆的，只能有一个在执行
- resolve()
  - 状态：fulfilled
    - 没有错误，进入此状态，不会执行其他状态
  - 结果：src
- reject()
  - 状态：rejected
    - 出现错误，进入此状态，不会执行其他状态
  - 结果：err

```
function loadScript(src){
 	return new Promise((resolve,reject) => {
 		let script = document.createElement("script")
 		script.src = src
 		script.onload = () => {
 			resolve(src)
 			console.log(16)
 		}
 		script.onerror = (err) => {
 			reject(err)
 			console.log(8)
 		}
 		document.head.append(script)
 	})
}

loadScript("./02-04-01.js")
结果：
02-04-01.js
16
```

### 7.2 then

- then是Promise对象原型上的方法，必须是Promise对象才能调用then方法

- promise. then(onFulfilled,onRejected)
  - then支持两个参数，两个参数都是函数类型，第一个是必选的，第二个是可选的
  - 这两个函数分别对应着，Promise对象的resolve()和reject()方法
  - 如果传的参数是非函数，会返回一个空的Promise对象，保证只要调用then方法就一定能返回Promise对象 ，因此可以连续使用链式调用
    - 调用then()方法时，需要将对象return出去，否则会一直是fulfilled状态

```
function loadScript(src){
 	return new Promise((resolve,reject) => {
 		let script = document.createElement("script")
 		script.src = src
 		script.onload = () => {
 			resolve(src)
 			console.log(16)
 		}
 		script.onerror = (err) => {
 			reject(err)
 			console.log(8)
 		}
 		document.head.append(script)
 	})
}

console.log(loadScript("./02-04-01.js")
 	.then(() => {
 		return loadScript("./02-04-02.js")
 	},(err) => {
 		console.log(err)
 	}))// [[PromiseState]]: "rejected"
console.log(loadScript("./02-04-01.js")
 	.then(() => {
 		loadScript("./02-04-02.js")
 	},(err) => {
 		console.log(err)
 	}))// [[PromiseState]]: "fulfilled"
```

### 7.3 resolve()&reject()

- 这两个是Promise的静态方法，需要使用Promise对象进行调用
- 异步操作需要使用then()调用
- 不是Promise对象，则不能使用then()
  - resolve()和reject()可以解决不是Promise对象的问题
  - reject()需要传入一个Error对象

```
function test(flag){
	if(flag){
		return new Promise((resolve,reject) => {
			resolve(8)
		})
	}else {
	        // 42 不是Promise对象，不能使用then方法
        	// return 42;
			return Promise.resolve(16)
		}
}
test(0)
	.then(value => console.log(value))
```

```
function test(flag){
	if(flag){
		return new Promise((resolve,reject) => {
			resolve(8)
		})
	}else {
			return Promise.reject(new Error("message: string"))
		}
}
test(0)
	.then(value => console.log(value)
		,err => console.log(err))// Error: message: string
```

### 7.4 catch()

- 用来捕获链式操作reject抛出的异常

```
function loadScript(src){
 	return new Promise((resolve,reject) => {
 		let script = document.createElement("script")
 		script.src = src
 		script.onload = () => {
 			resolve(src)
 			console.log(16)
 		}
 		script.onerror = (err) => {
 			reject(err)
 		}
 		document.head.append(script)
 	})
}
loadScript("./02-04-01.js")
 	.then(() => {
 		return loadScript("./02-04-01.js")
 	}).then(() => {
 		return loadScript("./02-04-0.js")
 	}).catch(err => {
 		console.log(err)
 	})
```

### 7.5 all()

- 处理并行接口问题
- 几个异步操作处理完成后，将其整合到一起

```
let p1 = Promise.resolve("dx")
let p2 = Promise.resolve(16)
let p3 = Promise.resolve("hebe")

Promise.all([p1,p2,p3])
 	.then(value => console.log(value))// ["dx", 16, "hebe"]
```

### 7.6 race()

- 先到先得
  - 几个异步操作进行竞争，返回最先得到的数据

```
let p1 = () => {
	return new Promise((resolve,reject) => {
		setTimeout(() => {
			reject(new Error("先到的error"))
		},2000)
	})
}

let p2 = () => {
	return new Promise((resolve,reject) => {
		setTimeout(() => {
			resolve("resolve")
		},1000)
	})
} 

Promise.race([p1(),p2()])
 	.then(value => console.log(value))
 	.catch(err => console.log(err))
```

## 8. 反射机制（Reflect)

- 在编译阶段不知道哪个类被加载，而是在运行的时候才加载执行
- es 5：先指定方法再调用apply方法

```
console.log(Math.floor.apply(null,[2.7]))// 2
```

- es 6：静态扫描时，并不知道哪个方法在使用apply()方法
- 当执行时，将参数传过来才知道

```
console.log(Reflect.apply(Math.floor,null,[2.7]))
```

- 通过条件，选择方法

```
function getPrice(price){
	console.log(Reflect.apply(price < 100 ? Math.ceil : Math.floor,null,[price]))
}
getPrice(101.7)// 101
getPrice(91.2)// 92
```

### **实例化类**

- 调用不同的类，动态实例化类
- 不加参数，需要传空数组

```
let str = new String()
console.log(str)// String {""}
let s = Reflect.construct(String,[])
console.log(s)// String {""}
console.log(typeof s)// Object
console.log(s instanceof String)// true
let arr = Reflect.construct(Array,[])
console.log(arr instanceof Array)// true
```

### 新增属性

- defineProperty()
  - Reflect和Object对象都有这个方法
  - 两个对象调用这个方法的返回值不同

```
const obj = {}
console.log(Reflect.defineProperty(obj,"name",{value:"hebe"}))// true
console.log(obj)// {name: "hebe"}
const obj2 = {}
console.log(Object.defineProperty(obj2, "name", {value:"dx"}))// {name: "dx"}
console.log(obj2)// {name: "dx"}
```

### 删除属性

- deleteProperty()
  - Object没有此方法

```
const obj = {
	name:"hebe",
	number:16
}
console.log(Reflect.deleteProperty(obj,"name"))// true
console.log(obj)// {number: 16}
```

### 读数据

- get()
- 参数：
  1. 对象
  2. 属性或者索引
- 如果属性或者索引不存在，返回undefined

```
const obj = {
	name:"hebe",
	number:16
}
console.log(Reflect.get(obj,"name"))// hebe
console.log(Reflect.get(obj,"name1"))// undefined
```

```
const arr = [1,2,"dx"]
console.log(Reflect.get(arr,2))// dx
console.log(Reflect.get(arr,5))// undefined
```

### 写数据

- set()
- 参数：
  1. 对象
  2. 属性或者索引
  3. 值
- 如果属性或者索引存在，将会修改原来的数据

```
const obj = {
	name:"hebe",
	number:16
}
console.log(Reflect.set(obj,"name1","dx"))
console.log(obj)
console.log(Reflect.set(obj,"number",8))
console.log(obj)
```

```
const arr = [1,2,"dx"]
console.log(Reflect.set(arr,3,16))// true
console.log(arr)// [1, 2, "dx", 16]
console.log(Reflect.set(arr,1,"hebe"))// true
console.log(arr)// [1, "hebe", "dx", 16]
```

### 获取属性描述符

- getOwnPropertyDescriptor()
  - 获取Object对象下面的属性，它的具体的描述符
  - 属性描述符：值，是不是只读，可不可以修改，可不可以配置。。。。

```
console.log(Reflect.getOwnPropertyDescriptor(obj, "name"))
// {value: "hebe", writable: true, enumerable: true, configurable: true}
console.log(typeof Reflect.getOwnPropertyDescriptor(obj, "name"))// object
```

### 获取对象原型

- getPrototypeOf()

```
const arr = []
// 报错：Reflect.getPrototypeOf called on non-object
    at Reflect.getPrototypeOf (<anonymous>)
//let str = "123"
let str = new String()
const obj = {}
console.log(Reflect.getPrototypeOf(arr))
// [constructor: ƒ, concat: ƒ, copyWithin: ƒ, fill: ƒ, find: ƒ, …]
console.log(Reflect.getPrototypeOf(obj))
// {constructor: ƒ, __defineGetter__: ƒ, __defineSetter__: ƒ, hasOwnProperty: ƒ, __lookupGetter__: ƒ, …}
console.log(typeof Reflect.getPrototypeOf(arr))// object
console.log(Reflect.getPrototypeOf(str))
// String {"", constructor: ƒ, anchor: ƒ, big: ƒ, blink: ƒ, …}
```

### 验证对象是否存在属性

- has()
  - 这是Reflect特有的方法，Object没有
  - 参数：
    1. 对象
    2. 查找的属性
  - 如果对象中有此属性，返回true，否则返回false

```
const obj = {
	name: "dx",
	num: 16
}
console.log(Reflect.has(obj,"name"))// tue
console.log(typeof Reflect.has(obj,"num"))// boolean
console.log(Reflect.has(obj,"n"))// false
```

### 判断对象是否可扩展

- isExtensible()
  - Object. freeze()
    - 使对象不可扩展
  - 返回值是boolean类型，可扩展返回true，否则返回false

```
const obj = {
	name: "dx",
	num: 16
}
console.log(Reflect.isExtensible(obj))// true
Object.freeze(obj)
console.log(Reflect.isExtensible(obj))// false
```

### 禁止对象扩展

- preventExtensions()

```
const obj = {
	name: "dx",
	num: 16	
}
console.log(Reflect.isExtensible(obj))// true
Reflect.preventExtensions(obj)
console.log(Reflect.isExtensible(obj))// false
```

### 获取对象自身的属性

- ownKeys()
  - 只会返回自身的属性，不会去原型链上的属性
  - 返回值是一个数组

```
const obj = {
	name: "dx",
	num: 16	
}
const arr = [1,"name","dx",8]
console.log(Reflect.ownKeys(obj))// ["name", "num"]
console.log(Reflect.ownKeys(arr))// ["0", "1", "2", "3", "length"]
console.log(Reflect.ownKeys([]))// ["length"]
console.log(Reflect.ownKeys({}))// []
console.log(Reflect.ownKeys(obj) instanceof Array)// true
```

### 修改原型链

- setPrototypeOf()
  - 修改对象的原型
- getPrototypeOf()
  - 获取对象的原型

```
const arr = [1,2,3,4,5]
console.log(Reflect.getPrototypeOf(arr))
// [constructor: ƒ, concat: ƒ, copyWithin: ƒ, fill: ƒ, find: ƒ, …]
Reflect.setPrototypeOf(arr,String.prototype)
console.log(Reflect.getPrototypeOf(arr))
// String {"", constructor: ƒ, anchor: ƒ, big: ƒ, blink: ƒ, …}
```

## 9. 代理（Proxy)

#### 创建

- 对象有两个参数：
  1. 要代理的对象
  2. 代理之后需要做的事
- target：代理对象
- key：对象的属性

```
let obj ={
	name: "dx",
	number: 16
}
let proxy_obj = new Proxy(obj,{
	get(target,key){
		if(target[key] === "dx"){
			return "最佳二传"
		}else {
			return target[key]
		}
	}
})
console.log(proxy_obj.number)// 16
console.log(proxy_obj.name)// 最佳二传
```

### 只读

- 通过set()方法，拦截赋值操作，使代理对象不能对原对象进行修改

```
let obj = {
	name: "dx",
	number: 16
}
let proxy_obj = new Proxy(obj,{
	get(target,key){
		return target[key]
	},
	set(target,key,value) {
		return false
	}
})
console.log(proxy_obj.name,proxy_obj.number)// dx 16
proxy_obj.number = 8
console.log(proxy_obj.number)// 16
```

### 校验

- 不能破坏数据结构
- 拦截无效数据
- 校验函数可以单独抽离出来，可以重复使用

```
const obj = {
	name: "dx",
	number: 8
}
let validator = (target,key,value) => {
	if(Reflect.has(target,key)){
			if(key === "number"){
				if(value > 1 && value < 17) {
					target[key] = value
				}else {
					return false
				}
			}else {
				target[key] = value
			}
		}else {
			return false
		}
}
const proxy_obj = new Proxy(obj,{
	get(target,key){
		return target[key]
	},
	set: validator
})
console.log(proxy_obj.name,proxy_obj.number)// dx 8
console.log(proxy_obj)// Proxy {name: "dx", number: 8}
proxy_obj.name = "hebe"
proxy_obj.number = 16
console.log(proxy_obj)// Proxy {name: "hebe", number: 16}
proxy_obj.number = 20
console.log(proxy_obj)// Proxy {name: "hebe", number: 16}
```

- 使用throw抛出错误，上报异常

```
window.addEventListener("error", (e) => {
 	console.log(e)
},true)
const obj = {
	name: "dx",
	number: 8
}
let validator = (target,key,value) => {
	if(Reflect.has(target,key)){
			if(key === "number"){
				if(value > 1 && value < 17) {
					target[key] = value
				}else {
					throw new TypeError("number error")
				}
			}else {
				target[key] = value
			}
		}else {
			return false
		}
}
const proxy_obj = new Proxy(obj,{
	get(target,key){
		return target[key] || ""
	},
	set: validator
})
console.log(proxy_obj.name,proxy_obj.number)// dx 8
console.log(proxy_obj)// Proxy {name: "dx", number: 8}
proxy_obj.name = "hebe"
proxy_obj.number = 16
console.log(proxy_obj)// Proxy {name: "hebe", number: 16}
proxy_obj.number = 20
```

### 随机且唯一的只读id

```
class GetNumber{
	// 实例对象的id会变
	/*constructor(){
		this.id = Math.random().toString(36).slice(-8)
	}*/
	constructor(){
		this.proxy_id = new Proxy({
			id: Math.random().toString(36).slice(-8)
		},{})
	}
	get id (){
		return this.proxy_id.id
	}
}
let num1 = new GetNumber()
let num2 = new GetNumber()
for(let i=0;i<10;i++){
	console.log(num1.id,num2.id)// 1d7d5iy8 guowsgwc
}
num1.id = 123
console.log(num1.id,num2.id)// 1d7d5iy8 guowsgwc
```

### 取消代理

- 取消代理代理不能通过new创建代理对象
- Proxy. revocable()
  - 返回值是一个对象，对象包括：
    - Proxy对象
    - revoke()方法
  - 读取代理对象：
    - 代理对象.proxy.属性名
- revoke()
  - 取消代理的方法
  - 使用：代理对象.revoke()
  - 使用该方法后，无法再通过代理对象读取属性

```
const obj = {
	name: "dx",
	number: 8
}

const proxy_obj = Proxy.revocable(obj,{
	get(target,key){
		return target[key]
	}
})
console.log(proxy_obj)// {proxy: Proxy, revoke: ƒ}
setTimeout(() => {
	console.log(proxy_obj.proxy.name,proxy_obj.proxy.number)// dx 8
	proxy_obj.recoke()
	setTimeout(() => {
		console.log(proxy_obj.proxy.name,proxy_obj.proxy.number)// proxy_obj.recoke is not a function
	},1000)
},1000)

```

## 10. Generator

- function和函数名之间添加 *
  - * 前后都要有空格
- 在函数内部通过使用yield关键字，暂停函数的执行
- 这个函数执行需要赋值给变量
- 变量通过next()方法恢复函数执行
- 可以控制循环的执行
- 超过循环的范围将不会执行

```
function * loop(){
	for(let i=0;i<3;i++){
		console.log(i)
	}
}
const fun = loop()
console.log(fun)// loop {<suspended>}
fun.next()// 0
fun.next()// 1
fun.next()// 2
fun.next()// 
```

### yield

- yield关键字没有返回值
- next()方法会在遇到yield关键字或函数结束时，暂停函数的执行
  - 第一次next()，在yield 1 时暂停，这是并没有输出语句

```
function * test(){
	let val
	val = yield 1
	console.log(val)
}
const fun = test()
fun.next()
fun.next()// undefined
```

- yield *
  - yield加*表示后面是可遍历的对象或是另一个Generator对象

```
function * test(){
	let val
	val = yield * [1,2,3]
	console.log(val)
}
const fun = test()
console.log(fun.next())
console.log(fun.next())
console.log(fun.next())
console.log(fun.next())
结果：
{value: 1, done: false}
{value: 2, done: false}
{value: 3, done: false}
undefined
{value: undefined, done: true}
```

### next()

- 恢复函数的执行
- 返回一个对象：是当前执行的数据和状态
  - value：当前返回的执行结果
  - done：是否结束

- 函数可以传参数，参数将会作为yield的返回值

```
function * test(){
	let val
	val = yield [1,2,3]
	console.log(val)
}
const fun = test()
console.log(fun.next(2))
console.log(fun.next(8))
结果：
{value: Array(3), done: false}
8
{value: undefined, done: true}
```

- 第一个next()，执行完yield后面的表达式就结束
  - 这步骤不需要yield的返回值
- 第二个next()，恢复函数执行，从之前暂停的地方开始
  - 执行赋值操作，此时需要yield的返回值8
  - 执行打印语句，此时val的值是8

### return()

- 可以使循环提前结束

```
function * test(){
	while (true) {
		yield 1
	}
}
const fun = test()
console.log(fun.next())// {value: 1, done: false}
console.log(fun.return())// {value: undefined, done: true}
console.log(fun.next())// {value: undefined, done: true}
```

- 方法可以传递参数
  - 参数将会作为value的值

```
function * test(){
	while (true) {
		yield 1
	}
}
const fun = test()
console.log(fun.next())// {value: 1, done: false}
console.log(fun.return(8))// {value: 8, done: true}
console.log(fun.next(2))// {value: undefined, done: true}
```

### 跳出此次循环

- 通过抛出异常跳出当次循环

```
function * test(){
	while(true){
		try {
			yield 1
		} catch(e) {
			// statements
			console.log(e);
		}
	}
}
const fun = test()
console.log(fun.next())// {value: 1, done: false}
fun.throw(new Error("error message"))
console.log(fun.next())// {value: 1, done: false}
```

## 11. Iterrator

- 可以自定义对象遍历
- 遍历器接口框架：
  - 输入就是this(这个对象)
  - 输出有规定
    - done的值是boolean，false表示遍历没有结束，true表示遍历结束
    - value的值是当前遍历项的值

```
obj[Symbol.iterator] = function() {
	// this 输入
	// 返回
	return {
		next() {
			return {
				done: ,// boolean
				value: // 当前遍历项的值
			}
		}
	}
}
```

- 可迭代协议：
  - 判断一个对象是否可以迭代，就需要看这个对象是否有Symbol. iterator为key的方法，如果没有就是不可迭代的

- 迭代器协议：

```
return {
		next() {
			return {
				done: ,// boolean
				value: // 当前遍历项的值
			}
		}
	}
```

### 自定义对象遍历

```
let authors = {
  allAuthors: {
    fiction: ['Agla', 'Skks', 'LP'],
    scienceFiction: ['Neal', 'Arthru', 'Ribert'],
    fantasy: ['J.R.Tole', 'J.M.R', 'Terry P.K']
  },
  Addres: []
}

authors[Symbol.iterator] = function (){
	let allAuthors = this.allAuthors
	let keys = Reflect.ownKeys(allAuthors)
	let values = []	
	return {
		next() {
			if(!values.length){
				if(keys.length){
					values = allAuthors[keys[0]]
					keys.shift()
				}
			}
			return {
				done: !values.length,
				value: values.shift()
			}
		}
	}
}
let arr = []
for(let v of authors){
	arr.push(v)
}
console.log(arr)// ["Agla", "Skks", "LP", "Neal", "Arthru", "Ribert", "J.R.Tole", "J.M.R", "Terry P.K"]
```

- 结合Generator

```
authors[Symbol.iterator] = function * (){
	let allAuthors = this.allAuthors
	let keys = Reflect.ownKeys(allAuthors)
	let values = []
	while(1){
		if(!values.length){
			if(keys.length){
				values = allAuthors[keys[0]]
				keys.shift()
				yield values.shift()
			}else {
				return false
			}
		}else {
			yield values.shift()
		}
	}
}
```

## 12. 模块化

- export
  - 导出
- export default
  - 默认导出，只能有一个默认导出

```
export let name = "hebe"
export let arr = [1,2,3,4]
export let obj = {
	name: "dx",
	number: 16
}
```

```
let name = "hebe"
let arr = [1,2,3,4]
let obj = {
	name: "dx",
	number: 16
}

export default name
export {
	arr,
	obj
}
```

- import
  - 导入
  - 默认导出的，放在{}外

```
import name,{arr,obj} from "./02-06-01.js"
```

- 默认导出的，导入时可以不使用导出的名字
  - 因为只能有一个默认导出
- 不使用普通导出的名称
  - 原名 as 重命名

```
import name,{arr as newName,obj} from "./02-06-01.js"
```

**全部导入**

```
import * as Mod from "./02-06-01.js"
```

- 将导出的对象，全部放入Mod中
- 调用时，使用 Mod.属性/方法 的方法，使用导出的内容

# ES 7

## Array

### 判断元素是否存在

- includes()
  - 存在返回true
  - 不存在返回false

```
const arr = [1,2,3,4,5]
console.log(arr.includes(3))// true
console.log(arr.includes(8))// false
```

## Math

### 乘方简写

- \*\*

```
console.log(Math.pow(2,3))// 8
console.log(2 ** 4)// 16
```

# ES 8

## async await

- async
  - 添加async关键字的函数，返回值是一个Promise对象
  - 如果返回值是一个Promise对象则不会进行处理
  - 如果返回值不是一个Promise对象则会将其转化为Promise对象
    - Promise. resolve()

```
async function testAsync(){
	return 16
}
console.log(testAsync())//Promise {<fulfilled>: 16}
console.log(testAsync() instanceof Promise)// true
testAsync().then(val => {
	console.log(val)// 16
	return testAsync()
}).then(val => {
	console.log(val)// 16
})
```

- await
  - 可以是async函数中的异步操作和同步操作一起顺序执行
  - 必须是有async关键字的函数，才可以使用await关键字
- 执行完同步操作后，才会执行异步操作

```
async function testAsync(){
	let promise = new Promise((resolve,reject) => {
		setTimeout(()=>{
			resolve("dx")
		},1000)
	})
	promise.then(val => {
		console.log(val)
	})
	console.log(8)
	return 16
}
//testAsync()// 8 dx
testAsync().then(val => {
	console.log(val)
})
// 8 16 dx
```

```
async function testAsync(){
	let promise = new Promise((resolve,reject) => {
		setTimeout(()=>{
			resolve("dx")
		},1000)
	})
	console.log(await promise)
	console.log(8)
	return 16
}
testAsync()//dx 8 
testAsync().then(val => {
	console.log(val)
})
//dx 8 16 
```

## Object

### Object. keys()

- 返回一个数组，数组中是对象key的集合
- 因为返回值是一个数组，所有可用使用数组的方法

```
const obj = {
	"dx": 16,
	"hebe": 330
}
let arr = []
for(let k in obj){
	arr.push(k)
}
console.log(arr)// ["dx", "hebe"]
console.log(Object.keys(obj))// ["dx", "hebe"]
console.log(Object.keys(obj).filter(item => item === "dx"))// ["dx"]
```

### Object. values()

- 返回一个数组，数组中是对象value的集合

```
const obj = {
	"dx": 16,
	"hebe": 330
}
let arr = []
for(let k in obj){
	arr.push(obj[k])
}
console.log(arr)// [16, 330]
console.log(Object.values(obj))// [16, 330]
console.log(Object.values(obj).filter(item => item > 20))// [330]
```

### Object. entries()

- 可以将对象变成可遍历的对象

```
const obj = {
	"dx": 16,
	"hebe": 330
}
let keys = []
let values = []
for(let [k,v] of Object.entries(obj)){
	keys.push(k)
	values.push(v)
}
console.log(keys)// ["dx", "hebe"]
console.log(values)// [16, 330]
```

### Object. defineProperty()

- 定义对象属性的数据描述符
- 参数：
  1. 对象
  2. 对象的属性名
  3. 数据描述符

```
const obj = {
	hebe: 330,
	dx: 16,
	number: 8
}
console.log(Object.keys(obj))// ["hebe", "dx", "number"]
Object.defineProperty(obj,"number",{
	enumerable: false// 是否可以枚举
})
console.log(Object.keys(obj))// ["hebe", "dx"]
```

### Object. getOwnPropertyDescriptors()

- 获取对象中所有属性的数据描述符

```
const obj = {
	hebe: 330,
	dx: 16,
	number: 8
}
Object.defineProperty(obj,"number",{
	enumerable: false// 是否可以枚举
})
console.log(Object.getOwnPropertyDescriptors(obj))
// {hebe: {…}, dx: {…}, number: {…}}
// number: {value: 8, writable: true, enumerable: false, configurable: true}
```

### Object. getOwnPropertyDescriptor()

- 获取对象某一项属性的数据描述符
- 有两个参数：
  1. 对象
  2. 属性名

```
const obj = {
	hebe: 330,
	dx: 16,
	number: 8
}
Object.defineProperty(obj,"number",{
	enumerable: false
})
console.log(Object.getOwnPropertyDescriptor(obj, "number"))// {value: 8, writable: true, enumerable: false, configurable: true}
```

## String

### padStart()

- 方法有两个参数：
  1. 表示字符串有几位
  2. 不够使使用什么去补
- 在前面补

```
let arr = [1,22,333,4444]
let newArr = []
arr.forEach(item => {
	newArr.push(item.toString().padStart(4,"0"))
})
console.log(newArr)// ["0001", "0022", "0333", "4444"]
```

### padEnd()

- 在后面补

```
let arr = [1,22,333,4444]
let newArr = []
arr.forEach(item => {
	newArr.push(item.toString().padEnd(4,"^*"))
})
console.log(newArr)// ["1^*^", "22^*", "333^", "4444"]
```

# ES 9

