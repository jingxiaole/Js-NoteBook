# 										Js基础笔记

## 1、七大基本数据类型

在ECMAScript之中有六种原始类型(undefined, null, bealoon, number, String, symbol)，以及一个复杂类型（Object）。

可以使用typeof关键字进行判断这七种数据类型（记住，typeof是关键字，不是函数），它可以有参数，也可以没有参数。

​		1 undefined  表示声明了但是未定义的变量

​		2 number	表示一个整数或者是浮点型的值

​		3 String 表示一个字符串的值

​		4 function 表示函数

​		5 bealoon  表示一个布尔值

​		6 Object  表示对象，是区别于function的，另外null也是一个函数

​		7 symbol



#### 	1、undefined

​		什么是undefined，就是未定义，这里是指变量声明了但是未初始化的时候，变量就是未定义（undefined），而对于未声明的变量，直接使用的话，会直接抛错（new Error）出来。

​		undefined怎么用，这里说明一下，一般建议是，每个变量是先声明，再使用，且要对进行的变量进行初始化。ECMAScript定义一个undefined的类型，目的是为了找出没有赋值的变量，我们一般不会显示的去声明的undefined的，它只是用于变量声明的判断。

​			在typeof的判断中，会遇到

代码块01

```
let name 
console.log(name) // undefined
```

​		

#### 	2、null

​		对于声明而未赋值的变量，默认数据类型是null，null表示的是空指针对象，即它是一个Object的对象，只不过是指向空指针的。

​		它衍生出了undefined这个类型，undefined就是用于与之前的null进行区别。

#### 	3、String

#### 	4、Number

Number类型的三个方法Number，parseInt（）、parseflote（）

以及infinanty和NaN

#### 	5、Boolean

#### 	6、Object

#### 	7、Symbol