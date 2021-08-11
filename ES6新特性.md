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

```
const fn = n => n+1
const fn1 = (n = 3, m = 2) => {
	return n + m
}
```

​	箭头函数的特点：

​			1、简化的函数的书写格式，使函数看起来更加容读和书写

​			2、它没有this的机制，不会改变this的指向，任何情况下都不会改变

```
name = 1
const fn = (n,m) => {
n = this.name 
return n + m
}

// 非箭头函数的写法，this会指向函数调用者
say : function (n, m) {
const _this = this
setTimeout( ()=> {
	console.log(this.name) // undefined
}, 1000)
}
```



##### 	7、对象字面量的增强

​		对于对象用法的增强，主要表现在：

​		1、如果想给对象的属性赋值一个变量值，并且该变量名和属性名一样，则可以省略写法。

​		2、在对象中的方法也可以省略写，当方法名和属性名相同时，省略冒号,这里的this是指向调用对象方法的对象

​		3、对于属性名的命名，必须使用明确的值，在es2015中，可以使用[]的方式对对象属性名进行命名

```
 const name = 'df'
// 1、
const obj = {
 foo: 'foo',
 name   //这里的name名字相同，可以省略写
 
 // 2、
 // fn : function fn () {console.log('eeeee...')}
 // es2015中可以用
 fn () {console.log('eeeee...')}
 }
 
//  3、
// obj.Math.random():123  //写法是错误的
// obj[Math.random()]:123
// 在es2015中，新增了写法
obj[Math.random()] = 123
```

在说之前，现补充一个遗漏的点，

​		1、对于字符串，新增加了三个方法，include 和 startWith endWith，入参是字符串，返回一个是否包含该字符串的boolean值.

​		2、assign方法：将源对象合并到目标对象中

```
const obj = {
name: 'df'
age: 12
}
const objDog = {
	type: 'dog'
}
const action = { say : 'www'}
const animal = Object.assign(objDog, obj, action) // 后面也可以跟多个参数，都会赋值到第一个目标对象中
console.log(animal) // {name: 'df',age: 12,type: 'dog',say: 'www'}
```

​		具体的应用场景是：

​			1、如果一个对象（o1）的属性引用了另一个对象（o2）的值，在修改o1的时候，也会修改o2的值，这里用到assign方法，将o2的值赋值给o1的话，两个就相互不影响了。

```
 const obj1 = function func () {
 	const name = Object.assign({},obj)
 }
 obj1.name = 'jxl'
 console,log(obj.name) // df
 console.log(obj1.name) // jxl
```



##### 	8、proxy

​	proxy对象是对之前的defineProperty的一次强大升级，这个对象相当于对象的一个门卫，对于对象的读取操作以及delete都会做到监听和过滤。

```
const obj = {
    name: 'df',
    age: 18
}
						//参数： t1 -- 目标对象  t2 -- {}，方法的对象
const proxyObject = new Proxy(obj, {
    get (targe, property) { // 对于读取对象属性进行监视
        console.log(targe, property);
        return property in obj ? obj[property] : 'error'
    },
    set (targe, property,val) { // 对于函数属性的写入进行监视 
        console.log(targe, property,val);
        if (property === 'age') {
            if(!Number.isInteger(val)) throw new TypeError(`${val} is not number`)
        }
    }
})  
console.log(proxyObject.name);  // { name: 'df', age: 18 } name   df
proxyObject.age = 123 // { name: 'df', age: 18 } age 123
console.log(proxyObject.age);//  18
```

​			对于Object的proxy 和 defineProperty 的对比

​				1、proxy中有对delete操作的监听，而defineProperty没有

​				2、proxy更好的支持对数组对象的监听，对原数组方法进行重写的方式实现。（vue.js所使用的方式）

​				3、proxy是以非侵入的方式监管了对象的读写，即对已经定义好的操作，不需要对对象本身进行过多的操作就可以监听到读写

```
const list = []

const listProxy = new Proxy(list, {
    set (targe, property, val) {
        console.log(targe, property, val);
        targe[property] = val // 这里会自动监听到数组的索引进行赋值
        return true // 不写返回值会报错
    }
})

listProxy.push(100)   // [] 0 100    [ 100 ] length 1
```



##### 	9、Reflect

​	reflect是Object对象的一个静态类，里面有处理对象的操作的14个方法，这14个方法就是proxy对象的默认实现，即Proxy内部默认调用了REflect对象的方法

Reflect存在的意义在于统一提供了一套操纵对象的API

```
const obj = {
    name: 'df',
    age: 18
}
console.log(Reflect.has(obj, 'age'));  // 类似  'age' in obj 
console.log(Reflect.defineProperty(obj, 'age'));  // 类似  delete obj.age
console.log(Reflect.ownKeys(obj, 'age'));  // 类似  Object.keys(obj)

// 之前的方法会被慢慢取代掉，建议使用Reflect的方法
```

##### 	10、Promise

​	Promise是ES6新增的链式调用所使用的类，多数用于异步请求，属于微任务类型。

##### 	11、class类

​		1、在之前的js中，我们会通过定义函数的方式进行构造函数的创建，在通过new 一个构造函数的类来实现一种独立的数据类型（Class）。

```
function Person (name) {
    this.name = name
    this.say = function (){
        console.log('这是一个构造函数方法', this)
    }
}
// 通过定义在原型链上的方式来进行类之间数据共享

const person = new Person('df')
person.say()
person.property.action = function () {console.log('原型链上的数据共享')}
```

​		现在，ES6中，定义了一个class关键字来定义类，通java、php这些面向对象语言一样中类的功能类似（强调，JavaScript是面向函数式编程）。

```
class Dog {
    constructor (name,age) { // 这是构造器，对象一经创建就立即执行的类，里面的参数就是new对象时候传入的参数
        this.name = name
        this.age = age
    }
    say () { // 之前都是将方法放在原型上或者属性上，不能直接定义，现在可以了
        console.log('这是一个calss创建的类', this)
    }
}
```

​		2、通过静态方法来创建对象，静态方法只能函数自己来调用，它的实例对象不能调用，而实例方法只能通过它的实例对象来调用，它本身不能调用。实例方法都是定义在类原型上的，而通过关键字static修饰后，这个方法就变成了静态方法，只能通过类名去调用了。

```
class Dog {
    constructor (name,age) { // 这是构造器，对象一经创建就立即执行的类，里面的参数就是new对象时候传入的参数
        this.name = name
        this.age = age
    }
    say () { // 之前都是将方法放在原型上或者属性上，不能直接定义，现在可以了
        console.log('这是一个calss创建的类', this)
    }
    static action (name,age) {
        console.log('这是Dog类的静态方法')
        return new Dog(name, age)
    }
}

const ha = Dog.action('哈士奇', 3)
console.log(ha);  // 这是Dog类的静态方法    Dog { name: '哈士奇', age: 3 }
```

3、 静态方法中的this是是指向当前类型，而不是当前对象。

4、使用extends关键字来实现继承一个父类，通过super关键字来调用继承的父类的属性和方法

```
class Dog {
    constructor (name,age) { // 这是构造器，对象一经创建就立即执行的类，里面的参数就是new对象时候传入的参数
        this.name = name
        this.age = age
    }
    say () { // 之前都是将方法放在原型上或者属性上，不能直接定义，现在可以了
        console.log('这是一个calss创建的类', this)
    }
    static action (name,age) {
        console.log('这是Dog类的静态方法')
        return new Dog(name, age)
    }
}

class MinDog extends Dog {
    constructor (name,age,type) {
        super(name,age) // super关键字是用来调用父类 的，这里相当于在调用父类的构造方法
        this._type = type
    }
    hello () {
        super.say()
        console.log('上一句是调用父类super打印出来的');
    }
}

const ha = new MinDog('哈士奇', 3, 'man')
ha.hello() // 这是一个calss创建的类 MinDog { name: '哈士奇', age: 3, _type: 'man' }   // 上一句是调用父类super打印出来的
```



##### 	12、set、map

​		set 数据结构

​			你可以将set结构看作是一个array的结构，但是区别是set的值都是唯一的值，不能重复，因此set经常应用的场景是数组去重。

​	set的方法：

​			1、add 因为该方法的返回值是一个set类型，所以可以链式调用。

​			2、size 相当于array 的length属性

​			3、delete  删除值

​			4、clear  清除set

​			5、has  类似于array的include	

​			6、forEach  循环

```
const arr = new Set() // 参数可以放入数组array

// add 方法 返回 set，因此可以链式调用,且有重复的话会省略不加入
arr.add(1).add(2).add(2) // [1,2]

// set 不等同于arr 是一个伪数组结构，通过Array的from方法可以将其变成数组结构
console.log(Array.from(arr));
console.log(...arr); // 通过解构也可以

// size -> length
console.log(arr.size); // 2

// has 方法  检查set中是否包含 对应值

console.log(arr.has(i)); // true

// delete  删除
console.log(arr.delete(1)); // [2]

// clear  清空set
console.log(arr.clear); // []
```

map 数据结构

​	map是<key, value>结构的真正意义上的实现，这里的key是可以存储任意类型的数据，而在object对象中，对于key值，即使我们不是存放的String类型的数据，它也会自动给我们使用toString的方法。

```
const obj = {}
obj[true] = '123'
obj[1] = 1
obj[{a: 1}] = 'a = 1'
 // 打结果都是使用过toString方法的键
console.log(Object.keys(obj)); //  [ '1', 'true', '[object Object]' ]
```

​	map 的使用方法：

​		set 方法  存数据

​		get方法  获取方法

​		delete 方法  删除键值对

​		has 方法  判断是否存在

​		clear 方法 清楚map

​		forEeach方法  遍历map    （value， key）

##### 	13、Symbol

​		Symbol数据类型，符号数据类型，它的每一次创建都是独一无二的，其参数是为其添加说明内容，每一个

```
const s =  Symbol()
console.log(s); // Symbol()  -- 这是一个值，Symbol值
console.log(typeof s); // Symbol
console.log(Symbol() === Symbol()); // false    

const obj = {}
obj[Symbol()] = 213
obj[Symbol('foo')] = 123
obj[Symbol(123)] = 321

console.log(obj); // { [Symbol()]: 213, [Symbol('foo')]: 123, [Symbol(123)]: 321 }

```

symbol都是独一无二 ，不相等的，常用的场景是为对象进行属性名的命名，那么现在对象就有String和Symbol两个格式的属性命名。

Symbold特点：

```
const s =  Symbol()
// 特点一：每一个Symbol值都是独一无二的
console.log(Symbol() === Symbol() );  // false

// 特点二： 通过全局注册或者它的内置静态方法for可以拿到同一份Symbol()值
    const s1 = Symbol()
    console.log(s1 === s1); // true
    // for方法是用来维护同一个字符串的参数的Symbol值，传入的参数如果不是String类型，也会在内部转化为String
    const s2 = Symbol.for(123)
    const s3 = Symbol.for('123')
    console.log(s2 === s3); // true

    // 特点三： Symbol中自带了很多自定义常量，用于实现对象的自定义属性标签
    const obj= {}
    console.log(obj.toString()); // [object Object]这个字符串就是属性标签
    // 通过Symbol的自带常量可以为这些属性从新定义 （这块内容不太懂，后续再理解）
    obj[Symbol.toStringTag] = 'XXX'
    console.log(obj.toString()); // [object XXX]


    // 特点四：通过Symbol定义的内置属性是无法通过 forEach、Object.keys、json.stringify 方式拿到值的 -- 这些都是获取到的字符串属性名
    // 只有通过Object.getOwnPropertySymbol可以取到全部symbol值
```



##### 14、for ... of ... 

​		1、for 循环，使用于遍历数组，而且可以使用break中途退出

​		2、for ... in ... 和方法foerEach 循环键值对数组或对象，但是不能brake

​		3、for ... of ... ,ES6新增的循环方式，可以遍历所有的可循环数据，并且有brake中途退出，作为以后主要使用的方式，它可以遍历数组、对象、map、set、伪数组等数据结果

```
// 数组
const arr = [1,2,3,4]
for( i of arr) {
    console.log(i);
}
// set

const set1 = new Set(arr)
for( i of set1) {
    console.log(i);
}

// map
const m = new Map()
m.set('name','df')
m.set('age',18)
for(const [i,key] of m) {
    console.log(i,key);
}
// 对象
const obj = {
    name: 'jxl',
    age: 23
}
for( i of obj) {
    console.log(i);
}
```



##### 	15、迭代器和生成器