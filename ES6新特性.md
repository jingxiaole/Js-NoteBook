# 												ES6新特性															



### 一、关于ES6和JavaScript的关系

##### 		1、ES6是对于ES2015的俗称，也可以叫通常，那么，ES6是什么呢？

​			ES 全称是ECAMScript，它是基于JavaScript之上的一种语言，JavaScript正是建立在ECAMScript语言的基础规范中建立使用的，那么，ECAMScript的使用，对于JavaScript至关重要！

​			在我的理解中，ECAMScript是一种语言层面的东西，它只是定义了JavaScript以及在它基础之上建立的其他语言的语法规范，而JavaScript的语言，更关于一种平台性质在其中。

​	正如图1-1所示，JavaScript包括 ECAMScript、DOM、BOM三个组成部分，DOM和BOM是web API提供的接口或者是JavaScript和浏览器之间进行交互的部分，实质就是操纵文档元素，进行展示布局，而ECAMScript在JavaScript中其中语法的作用，它不会去跟文档有直接的关系，但是他的数据处理完成后会通过web API展示在文档中。

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

​			2> 在for循环中，let效果实际上是利用了闭包的机制，并且，对于循环块中的let 和 执行块中的lei是两个块中分别定义的变量，互不影响。

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

``` `
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

​	3、对象的解构

​		对象的解构和数组类似，只不过不是根据位置下标获取，而是根据属性名进行获取

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

