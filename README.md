# Array
Array 引用类型可以通过 new 关键字调用或者字面量表达式来生成实例，当使用 new 并传入一个数字参数时，会创建参数长度的稀疏数组（由空单元组成的数组），当传入两个以上参数时，会创建由参数组成的数组

* 数组：数组通过数字进行索引，但是数组也是对象，所以也可以包含字符串键值和属性（但这些并不计算在数组长度内），除非字符串键值能够被强制类型转换为十进制数字的话，它就会被当作数字索引来处理。
* 类数组：包括 DOM查询操作返回的DOM元素列表、arguments

| 操作 | 语法 |
| --- | --- |
| 类数组转换成数组 | 1、var arr = Array.prototype.slice.call( arguments ); //slice(..)不带参数会返回当前数组的一个浅复本  2、Array.from(arguments)|
| 字符串转换成数组 | 1、"foo".split('').reverse().join('')对于包含复杂字符(Unicode，如星号、多字节字符)的字符串并不适用，这时则需要功能更加完备、能够处理Unicode的工具库，可参考Esrever |
| length=0 | 清空数组 |
```
//空数组和undefined数组还是有区别的：
var a = new Array( 3 ); 
var b = [ undefined, undefined, undefined ]; 
var c = []; 
c.length = 3;

a.join( "-" ); // "--" 
b.join( "-" ); // "--" 

a.map(function(v,i){ return i; }); // [ Empty x 3 ]  因为数组中并不存在任何单元，所以map(..)无法遍历。而join通过length属性值来遍历其中的元素
b.map(function(v,i){ return i; }); // [ 0, 1, 2 ]

//创建包含undefined单元（而非“空单元”）的数组
Array.apply( null, { length: 3 } ); //执行的实际上是Array(undefined, undefined, undefined)

```
## 1、Array实例常用方法：
**会改变原数组，可变更方法：**
* 栈方法：push()、pop()  
* 队列方法：shift()、unshift() //shift是删除  
* 增删改方法：splice()
* 重排序方法：reverse()、sort()、copyWithin(target, start, end)
* 填充方法：fill()

**下面的都不会改变原来数组，非变更方法：**
* 查找是否存在方法：indexOf()、lastIndexOf()、includes()
* 维度降级方法：flat()、flatMap()
* 操作方法：slice()、concat()、join()


### 1.1 迭代方法
每个方法都接受俩个参数，要在每一项上运行的函数和运行该函数的作用域对象-影响this的值。除了reduce其他的函数都会接受三个参数，分别是数组项的值、该项在数组中的位置和数组对象本身（item, index, arr）。数组大小（可通过设置length来改变）是可以动态调整的，即可以随着数据的添加自动增长以容纳新增数据。
*   some()：返回boolean值，对数组中的每一项运行给定函数，如果该函数对任一项返回true，则返回true
*   every()：返回boolean值，
*   map()：返回数组，
*   filter()：返回数组
*   forEach()：不返回任何值，纯遍历
*   find()：返回数组成员，用于找出第一个符合条件的数组成员。
*   findIndex()：返回index，返回第一个符合条件的数组成员的位置，如果所有成员都不符合条件，则返回-1
*   flatMap()：返回一个新数组，对原数组的每个成员执行一次函数，然后对返回值组成的数组执行flat()方法。不改变原数组。
*   reduce(): 有return，主要用于累加或者去重或者降维。[参考链接](https://www.cnblogs.com/caideyipi/p/7679681.html)

### 1.2 归并方法
这俩个方法都接收俩个参数，一个在每一项上调用的函数和作为归并基础的初始值。传入这些方法中的函数会接受4个参数，分别是前一个值、当前值、该项在数组中的位置和数组对象本身（lastItem, item, index, arr）,这个函数返回的任何值都会第一个参数自动传给下一项。
*   reduce()：从数组第一项开始，逐渐遍历到最后。
*   reduceRight()：从数组最后一项开始，向前遍历到第一项。

### 1.3 遍历数组方法
用for...of进行遍历

*   entries()：返回[index, elem]
*   keys()：返回index
*   values()：返回elem

### 1.4 转换方法
与其他引用类型一样，Array类型也重写了toLocaleString()、toString()和valueOf()方法。
*   toString()：返回由数组中每个值的字符串形式（它会依次调用数组中每个元素的 toString 方法 (null 和 undefined 是例外，它们会直接转为空字符串) ）拼接而成的一个以逗号分隔的字符串。
*   toLocaleString()：经常返回与toString()方法相同的值，但也不总是如此。当调用数组的toLocaleString()方法时，它也会创建一个数组值的以逗号分隔的字符串。而唯一的不同之处在于，这一次为了取得每一项的值，调用的是每一项的toLocaleString()方法，而不是toString()方法。
*   valueOf()：返回的还是数组。

`注意：如果数组中的某一项的值是null或者undefined，那么该值在join()、toLocaleString()、toString()和valueOf()方法返回的结果中以空字符串表示。`
```
let arr = [{a:1},123,()=>{},undefined]
console.log(arr.toString()) // "[object Object],123,()=>{}," 最后以逗号结尾，因为 undefined 变成空字符串了

let obj = {}
obj[arr] = ""
console.log(obj) // { '[object Object],123,()=>{},': "" } 当对象的属性是一个对象，JS 会将其转为字符串再作为其属性，这里就发生了隐式转换

//toLocaleString与toString区别：
var person1 = {     
  toLocaleString : function () {         
    return "Nikolaos";     
  },     
  toString : function() {                     
    return "Nicholas";     
  } 
}; 
var person2 = {     
  toLocaleString : function () {         
    return "Grigorios";     
  },     
  toString : function() {         
    return "Greg";     
  } 
}; 
var people = [person1, person2]; 
console.log(people);                          //Nicholas,Greg 
console.log(people.toString());               //Nicholas,Greg 
console.log(people.toLocaleString());         //Nikolaos,Grigorios
```
## 2、Array构造函数常用方法：
* Array.isArray()：判断是不是数组

