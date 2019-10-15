# Array
数组相关操作

* 栈方法：push()、push()
* 队列方法：shift()、unshift() //shift是删除
* 重排序方法：reverse()、sort()、copyWithin()
* 查找是否存在方法：indexOf()、lastIndexOf()、includes()
* 维度降级方法：flat()、flatMap()
* 填充方法：fill()
* 操作方法：slice()、splice()、concat()、join()


### 迭代方法
每个方法都接受俩个参数，要在每一项上运行的函数和运行该函数的作用域对象-影响this的值。除了reduce其他的函数都会接受三个参数，分别是数组项的值、该项在数组中的位置和数组对象本身（item, index, arr）。

*   some()：返回boolean值，对数组中的每一项运行给定函数，如果该函数对任一项返回true，则返回true
*   every()：返回boolean值，
*   map()：返回数组，
*   filter()：返回数组
*   forEach()：不返回任何值，纯遍历
*   find()：返回数组成员，用于找出第一个符合条件的数组成员。
*   findIndex()：返回index，返回第一个符合条件的数组成员的位置，如果所有成员都不符合条件，则返回-1
*   flatMap()：返回一个新数组，对原数组的每个成员执行一次函数，然后对返回值组成的数组执行flat()方法。不改变原数组。
*   reduce(): 有return，主要用于累加或者去重或者降维。[参考链接](https://www.cnblogs.com/caideyipi/p/7679681.html)

### 遍历数组
用for...of进行遍历

*   entries()：返回[index, elem]
*   keys()：返回index
*   values()：返回elem

  
### 归并方法
这俩个方法都接收俩个参数，一个在每一项上调用的函数和作为归并基础的初始值。传入这些方法中的函数会接受4个参数，分别是前一个值、当前值、该项在数组中的位置和数组对象本身（lastItem, item, index, arr）,这个函数返回的任何值都会第一个参数自动传给下一项。

*   reduce()：从数组第一项开始，逐渐遍历到最后。
*   reduceRight()：从数组最后一项开始，向前遍历到第一项。


