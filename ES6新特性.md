# 												ES6新特性															



### 一、关于ES6和JavaScript的关系

##### 		1、ES6是对于ES2015+的俗称，也可以说是通常叫法，那么，ES6是什么呢？

​			ES 全称是ECAMScript，它是JavaScript基础构建的一种语言，JavaScript正是建立在ECAMScript语言的基础规范中建立使用的，那么，ECAMScript的使用，对于JavaScript至关重要！

​			在我的理解中，ECAMScript是一种语言层面的东西，它只是定义了JavaScript以及在它基础之上建立的其他语言的语法规范，而JavaScript的语言，更关于一种平台性质在其中。

​	正如图1-1所示，JavaScript包括 ECAMScript、DOM、BOM三个组成部分，DOM和BOM是web API提供的接口或者是JavaScript和浏览器之间进行交互的部分，实质就是操纵文档元素，进行展示布局，而ECAMScript在JavaScript中其中语法的作用，它不会去跟文档有直接的关系，但是他的数据处理完成后会通过web API展示在文档中。

![image-20210809114226980](C:\Users\dingfan\AppData\Roaming\Typora\typora-user-images\image-20210809114226980.png)

​																																	1-1

​		下面就关于ES2015、ES2016、ES2015三个版本的更新内容，即我们通常讲的ES6来展开讲讲它都有哪些新内容

### 二、ES6新特性的分类

​		我们将讲解的内容主要归为四大类：

​			  1、解决原有语法上的一些不足 

​					let 和 const 的块级作用域

​		  	2、对原有语法进行增强

​					解构、展开、参数默认值、模板字符串

​			  3、全新的对象、全新的方法、全新的功能

​					promise、proxy、object的assign、is

​			  4、全新的数据类型和数据结构

​						symbol、set、map 



### 	三、ES6的使用

##### 				1、let 和 const 的块级作用域

​				在之前的ECMAScript中，对于作用域的划分只有**全局作用域**和**函数作用域**，在ES6中又新增了块级作用域，通常的来说就是**一对{}**包裹着的代码，在{}中的作用域就是块级作用域，因此新定义了两个let和const关键词，对于var这个老的关键词，是用于对老代码的维护所保留。

​			1>  let 关键字禁止变量提升，要先定义后使用，而且只作用于它所定义的块级作用域中，常用于for 或 if 之类的结构中。

```
for ( var i = 0;i < 3;i++) {
        for ( var i = 0; i < 3; i++) {
            console.log(i);
        }
    } // 0 1 2
    
    -----------------------------------
    for ( let i = 0;i < 3;i++) {
        for (let i = 0; i < 3; i++) {
            console.log(i);
        }
    } // 0 1 2 0 1 2 0 1 2
```

​			2> 在for循环中，let效果实际上是利用了闭包的机制，并且，对于循环块中的let 和 执行块中的let是两个块中分别定义的变量，互不影响。

```
    for (let i = 0; i < 2; i++) {
        let i = 'foo'
        console.log(i);
    } // foo  foo
```

​		3>  const 是在let 的基础上添加了一个**只读**属性，即变量一旦声明过后就不允许在修改，这里是不允许修改定义的地址，而不是不可以修改他内部的属性值。

```
const obj = {name: 'aaa'}
obj.name = 'bbb'
```

​		4>在使用上，不要使用var，主要使用 const 并配合着 let 使用

##### 	2、数组的解构

​		数组的解构是根据位置进行获取的

```
// 
const arr = [100, 200, 300]
  // 都获取
  const [a, b, c] = arr // a = 100 b = 200 c = 300
  // 只获取特定的值
  const [, , c] = arr  // c = 300
  // 对于的数组长度超过，会返回undefined
  const [a,b,c,d,e] = arr // a = 100, b = 200 c = 300  d = undefined e = undefined
  // 还可以设置默认值
  const [a,b,c,d = 400,e = 500] = arr // a = 100, b = 200 c = 300  d = 400 e = 500
```
##### 	3、对象的解构

​			对象的解构和数组类似，只不过不是根据位置下标获取，而是根据属性名进行获取

```
const obj = {name: 'bob', age: 23}

 // 首先是根据属性获取值
 const {name, age} = obj
 console.log(name)
 console.log(age)
 // 如果外面有一个相同的属性名，可以使用重命名的方式获取，并且可以设置默认值
 const {name:setName = 'sale', age} = obj
 let name = 'reset'
 console.log(name)
 console.log(age)

```

##### 	4、模板自变量

​		在ES6的语法中，新增了模板自变量的新语法格式，使用破折号按键那个点做双引号的格式  ·· ，这个模板自变量的特性如下：

​				1、支持换行

​				2、采用${}的方式进行插值表达式，{}中的内容就是js代码

​				3、在模板自变量之前，我们可以加一个标签函数用来对模板自变量的值进行处理

```
	const name = 'df'
	const age == 18
	const mrg = `I am df, ${name}的年龄是 ${age}` // 定义一个模板自变量
	
	const fn = (strs) => { // strs 就是接收到的模板自变量的数组
		console.log(strs) // 这里会打印一个数组出来，是通过${}进行分割后的字符串数组，不包含分割符中的值
	}
	function tag ( strs,name,name1) { // 在str后面，会依次接收表达式的值
		console.log(strs,name1,name1) // [ 'I am df, ', '的年龄是 ', '' ] 18 18
		console.log(strs,name,name1) // [ 'I am df, ', '的年龄是 ', '' ] df 18
		return strs[0] + name + strs[1] + name1 + strs[2] // 
	}
    const mrg1 = tag`I am df, ${name}的年龄是 ${age}` // 对于模板标签函数，我们可以看成是模板自变量的一个过滤器，对模板进行数据处理
     console.log(mrg1); // 这里标签函数tag的返回值就是模板自变量的值（即mggr1的值）
```

​		

##### 	5、默认参数和剩余参数

在说之前，现补充一个遗漏的点，就是对于字符串，新增加了三个方法，include 和 startWith endWith，入参是字符串，返回一个是否包含该字符串的boolean值.

默认参数

​	默认参数的设定在之前是通过在函数内部进行条件判断进行判断

```
function add (a ,b) {
a = a === undefined ? 0 : a
b = b === undefined ? 1 : b
retrun a + b
}
add (0) // 1
```

​	在ES6中新增的给参数设置默认值的特性，将大大简化我们的代码

```：
function add (a = 0 ,b = 1) { // 这里要说明的是，一定要将有默认值的参数放到没有默认值参数的后面位置（即出现在参数列表的最后），因为我们的参数是按照次序传递的，如果没有放到最后，我们的默认值将无法正常工作
console.log(' foo is shu', a + b)
retrun a + b
}
add (0) // 1
```

剩余参数

​		之前我们是使用arguments对象，通过伪数组方式来接收参数，包括我们在未知参数个数的情况下。现在，在ES6的语法中，新增了...的操作符，它有两个作用：

​		1、剩余操作符，用来接收从当前位置剩余参数的操作                    

```
function redece (...arg) {
	console.log(arg) // 这里的arg是一个伪数组，是传递进来的实参数组，并且这个操作只能放到最后一个参数的位置上进行（只能使用一次），否则影响前面参数
}
```

​		2、spread用法：（展开），将数组或者对象中内容或者属性进行依次展开	

```
const arr = ['foo', 'fn', 'functions']

console.log(arr[0], arr[1], arr[2]) // 方案一 
console.log.apply(console, arr) // 方案二   apply方法是（参数一： 用来从新定向this指向，参数二，向函数中放入参数的数组）
console.log(...arr) // ES6（spread）写法
```



##### 	6、箭头函数

​			箭头函数 （参数列表）=>  {函数体}  ，在函数体中只有返回值的情况下， 大括号可以省略。

##### 	7、对象字面量的增强

##### 	8、proxy

##### 	9、reflect

##### 	10、promise

##### 	11、class类

##### 	12、set、map

##### 	13、symbol

##### 	14、迭代器和生成器