# 问题

## 1. v-show 和 v-if 的区别

### v-show

符合条件的显示，不符合条件的display: none,用于频繁切换的节点。

### v-if

符合条件的显示，不符合条件的将不会挂载的dom树上，用于一次性的或更新不频繁的节点。

## 2. 为何 v-for 中要用 key

- 和Vue的虚拟DOM的Diff算法有关系
  - **key的作用主要是为了高效的更新虚拟DOM**
- 没有绑定key
  - 有五个li在第二个li后插入新的li，前两个li不变，第三个li变成要插入的内容，原来li的内容都需要插入到后面的li中，最后创建一个li用于插入原来li的最后一个元素
- 绑定了key
  - 每个节点就有了唯一标识，Diff算法就可以正确识别节点，最后就可以找到正确的位置插入新的节点

## 3. 描述 Vue 组件生命周期（有父子组件的情况）

1. new Vue()

2. 第一阶段：初始化
   - 初始化事件和生命周期
   - **beforeCreate()**
     - 创建实例之前执行的钩子
   - 初始化注入
     - 实现数据代理
   - **created()**
     - 创建实例完成后执行的钩子
     - 可以访问data数据
   - 在内存中编译模板
     - 把data对象里的数据和vue语法声明的模板编译成浏览器可读的HTML
   
   ----
   
   - vue实例初始化完成
   - 并没有开始渲染
   
   ---
   
   - **beforeMount()**
     
     - 将编译完成的HTML挂载到对应虚拟dom时触发的钩子
     - 此时页面没有内容
     
   - 将编译好的HTML替换el属性所指向的dom
   
   - **mounted()**
     
     - 渲染
     
     - 编译好的HTML挂载到页面完成之后执行的事件钩子
     - 这是一般会做一下ajax请求和异步任务，进行数据初始化
     - 注：mounted在整个实例中只执行一次
   
   ---
   
   组件已经在网页上绘制完成了
   
   ---
   
3. 第二阶段：更新
   - **beforeUpdate()**
     - 更新之前的钩子
   - 实时监控数据变化，并随之跟新dom
     - 界面更新
   - **updated()**
     - 更新之后的钩子

4. 第三阶段：死亡
   - **beforeDestroy()**
     - 实例销毁之前执行的钩子
     - 在这可以用于销毁自定义事件，防止内存泄露
   - 拆除数据监听，子组件和事件监听
   - **destroyed()**
     - 实例销毁完成后执行的钩子

### 父子组件生命周期调用顺序

#### 挂载阶段

1. 父组件create

2. 子组件create

3. 子组件mounted

4. 父组件mounted

#### 更新阶段

1. 父组件beforeUpdate
2. 子组件beforeUpdate
3. 子组件updated
4. 父组件updated

#### 销毁阶段

1. 父组件beforeDestroy
2. 子组件beforeDestroy
3. 子组件destroyed
4. 父组件destroyed

## 4. Vue 组件如何通讯

### 父组件向子组件传递数据

- 通过props（属性）向子组件传递数据

![](.\img\vue\03.07-01.png)

### 子组件向父组件传递数据

- 通过事件向父组件发送消息
- 自定义事件

------

- 当组件触发点击等已经定义好的事件时，组件的数据可能会发生变化，数据需要传递给父组件
  - 组件触发事件时，需要执行相应的方法
  - 执行方法完后，使用$emit('自定义事件名'，需要传递给父组件的参数)将事件发射出去
- 父组件通过v-on监听子组件自定义的事件，当子组件自定义事件触发时，执行相应的方法接受子组件传来的数据
  - 父组件通过@自定义事件名=“方法1”,监听子组件自定义事件，触发时，执行父组件methods中的方法1
  - methods中的方法1（参数），参数就是子组件传来的数据

## 5. 描述组件渲染和更新的过程

## 6. 双向数据绑定 v-model 的实现原理

v-model包含两个操作

1. v-bind
   - 将页面上的数据与data中的数据进行绑定
   - data中的数据发生变化时，页面上的数据也跟着变化
2. v-on
   - 用于绑定事件
   - 页面上的数据发生变化，触发事件
   - 执行绑定事件时，对data中的数据进行更新，使页面上的数据和data中的数据一致

## 7.响应式数组方法

响应式：数据改变，页面的也跟着变

- push(): 在最后增加
- pop()：删除最后一个元素
- shift()：删除第一个元素
- unshift()：在最前面添加元素
- splice()：删除元素、插入元素、替换元素
  - 第一个元素表示从哪个位置开始操作
  - 删除元素：第二个参数传入要删除的个数（如果没有传就删除后面所有的元素）
  - 插入元素：第二个参数，传入0，并且后面要跟上要插入的元素
    - splice(1,0,'a','b')
  - 替换元素：第二个参数，表示要替换几个元素，后面是用于替换前面的元素
    - splice(1,3,'x','y','z')
  - sort()：排序
  - reverse()：反转

非响应式数组方法

- 通过索引值修改数组中的元素

```
this.arr[index]='changeValue'
```

- splice

```
this.arr.splice(start,index,'changeValue')
```

- Vue. set(要修改的对象，索引值，修改后的值)

```
Vue.set(this.arr,index,'changeValue')
```

## 8. 组件中data为什么必须是一个函数

- 组件时会复用的，组件和组件之间应该是不会相互影响的，不然复用就没有意义了，组件应该只能控制自己的数据
- data是一个函数，并且每次都返回一个新的对象，这样每个组件都有自己专属的数据存放空间，组件之间的数据是独立，不会受到其他组件的影响

# 基本使用

## 插值操作

#### Mustache

- 可以通过Mustache语法(也就是双大括号)，将data中的文本数据，插入到HTML中

![](.\img\vue\03.04-01.png)

#### v-once

- 该指令后面不需要跟任何表达式
- 该指令表示元素和组件(组件后面才会学习)只渲染一次，不会随着数据的改变而改变

#### v-html

- 会将string的html解析出来并且进行渲染
  - 如果我们直接通过{{}}来输出，会将HTML代码也一起输出

![](.\img\vue\03.04-02.png)

#### v-text

- v-text作用和Mustache比较相似：都是用于将数据显示在界面中
- v-text通常情况下，接受一个string类型

![](.\img\vue\03.04-03.png)

#### v-pre

- v-pre用于跳过这个元素和它子元素的编译过程，用于显示原本的Mustache语法

![](.\img\vue\03.04-04.png)

#### v-cloak

- 在某些情况下，我们浏览器可能会直接显然出未编译的Mustache标签

![](.\img\vue\03.04-05.png)

- 在vue解析之前，div中有v-cloak属性
- 在vue解析之后，div中没有v-cloak属性

## 绑定属性

- v-bind用于绑定一个或多个属性值，或者向另一个组件传递props值
- 语法糖：
  - 使用  :   代替 v-bind:

#### v-bind绑定class

- 固定的class和动态绑定的class会进行合并，不会覆盖

##### 1. 对象语法

![](.\img\vue\03.04-06.png)

- 当布尔值是true时，表示有这个类型，反之没有这个类名

![](.\img\vue\03.04-07.png)

##### 2. 数组语法

![](.\img\vue\03.04-08.png)

#### v-bind绑定style

![](.\img\vue\03.04-09.png)

## 计算属性

![](.\img\vue\03.04-10.png)

**计算属性和methods的区别**

- 计算属性会进行缓存，如果多次使用时，计算属性只会调用一次

## 事件

1. event是原生的
2.  事件被挂载到当前元素

# 组件使用

## 父组件访问子组件的数据

### $children

- 父组件可以通过this.$children获得子组件对象的数组，这个数组包含所有的子组件对象
- 可以通过遍历获得所有子组件对象
- 一旦插入新的子组件，数组中子组件的索引将会发生改变

### $refs

- $refs和ref指令通常是一起使用的
  - 通过ref给某一个子组件绑定一个特定的ID
  - 通过this.$refs .ID就可以访问到该组件了

![](.\img\vue\03.08-01.png)

# 高级特性

## 自定义v-model

```
// 父组件中的数据（appMsg）和子组件的数据（cpnMsg）进行双向绑定
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>Document</title>
</head>
<body>
	<div id="app">
		{{appMsg}}
		<!-- 自定义v-model -->
		<cpn v-model="appMsg"></cpn>
	</div>
	<!-- 子组件模板 -->
	<template id="cpn">
		<div>
			<!-- value需要和子组件中的数据cpnMsg进行绑定 -->
			<input type="text"
			   :value="cpnMsg"
			   @input="$emit('change',$event.target.value)">
		</div>
	</template>
	<script src="../vue.js"></script>
	<script>
		const app = new Vue({
			el: "#app",
			// 父组件的数据
			data: {
				appMsg: "hebe"
			},
			components: {
				// 子组件
				cpn: {
					template: "#cpn",
					model: {
						prop: "cpnMsg",// 必须和props中的cpnMsg对应
						event: "change"
					},
					props: {
						cpnMsg: String
					}
				}
			}
		})
	</script>
</body>
</html>
```

## $nextTick

- vue是异步渲染
- data改变以后，dom不会立刻渲染
- $nextTick会在dom渲染之后触发，以获取最新的dom节点
- 页面渲染时会将data的修改整合，多次data修改只会渲染一次

```
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>Document</title>
</head>
<body>
	<div id="app">
		<ul ref="ul">
			<li v-for="item in list">{{item}}</li>
		</ul>
		<button @click="additem">添加</button>
	</div>
	<script src="../vue.js"></script>
	<script>
		const app = new Vue({
			el: "#app",
			data: {
				list: ['a','b','c']
			},
			methods: {
				additem(){
					this.list.push(`${Date.now()}`)
					this.list.push(`${Date.now()}`)
					this.list.push(`${Date.now()}`)
					// 返回值： 3
					/*const ul = this.$refs.ul
					console.log(ul.childNodes.length)*/
					//返回值： 6
					this.$nextTick(() => {
						const ul = this.$refs.ul
					console.log(ul.childNodes.length)
					})
				}
			}
		})
	</script>
</body>
</html>
```

## slot

## 动态、异步组件

## keep-alive

## mixin

# Vuex

# Vue-router