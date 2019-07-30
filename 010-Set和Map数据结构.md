# ----------------------Set和Map数据结构-----------------------
## 目录
<p id="title"></p>
<a href="#p1">:snowflake:Set</a><br>
<a href="#p2">:snowflake:WeakSet</a><br>
<a href="#p3">:snowflake:Map</a><br>
<a href="#p4">:snowflake:WeakMap</a><br>
<p id="p1"></p>

## :sunny:Set
<a href="#title">:whale2:回到目录</a><br>
#### :mag_right:基本用法
ES6提供了新的数据结构--Set.类似于数组,但是**成员的值是唯一的,没有重复**,本身是一个构造函数,用来生成Set数据结构
```JavaScript
const s = new Set();
[2,3,4,5,2,2].forEach(x => s.add(x));

for(let i of s){
    console.log(i);
}
//2 3 4 5
```
Set函数可以接受一个数组(或者具有iterable接口的其他数据结构)作为参数
```JavaScript
//例一
const set = new Set([1,2,3,4,4]);
[...set]
//[1,2,3,4]

//例二
const items = new Set([1,2,3,4,5,5,5,5]);
items.size //5

//例三
function divs (){
    return [...document.querySelectorAll('div')];
}
const set =new Set(divs());
set.size //55
```
上面的代码展示了一种去除数组重复成员的方法<br>
向set加入值不会发生类型转换,所以5和"5"是两个不同的值.Set内部判断两个值是否相同使用的算法类似于"===",但NaN不一样
```JavaScript
let set = new Set();
let a=NaN;
let b=NaN;
set.add(a);
set.add(b);
set //{NaN}
```
上面的代码向set实例添加了两个NaN,但实际上只添加了一个<br>
两个对象是总不相等的
```JavaScript
let set = new Set();
set.add({});
set.size //1

set.add({});
set.size  //2
```
#### :mag_right:Set实例的属性和方法
**属性**: 

属性名|作用
---|:--:
Set.prototype.constructor|构造函数,默认就是Set函数
Set.Prototype.size|放回Set实例成员的总数

**方法**: 

方法名|作用
---|:--:
add(value)|添加某个值,返回Set本身
delete()|删除某个值,返回一个布尔值,表示删除成功
has()|返回一个布尔值,表示参数是否为Set的成员
clear()|清除所有成员,没有返回值

Array.from方法可以将Set结构转换数组
```JavaScript
const items=new Set([1,2,3,4,5]);
const array = Array.from(items);
```
#### :mag_right:遍历操作
Set结构有4个遍历方法:<br>
+ keys(): 返回键名的遍历器
+ values(): 返回键值的遍历器
+ entires(): 返回键值对的遍历器
+ forEach(): 使用回调函数遍历每个成员<br>
**forEach()**<br>
```JavaScript
let set=new Set([1,2,3]);
set.forEach((value,key)=>console.log(value*2));  // 2 4 6
```
另外,forEach方法可以有第二个参数,表示绑定this参数
<br>
拓展运算符(...)内部使用for..of循环,所以也可以用于Set结构
```JavaScript
let set =new Set(["red","green","blue"]);
let arr=[...set];  //["red","green","blue"]
```
拓展运算符与Set结构相结合就可以去除数组的重复成员
```JavaScript
let arr = [3,5,2,2,5,5];
let unique=[...new Set(arr)]; //[3,5,2]
```
数组的map和filter方法也可以用于Set
```JavaScript
let set =new Set([1,2,3]);
set =new Set([...set].map(x=>x*2));
// {2,4,6}
```
用Set结构实现并集,交集和差集
```JavaScript
let a=new Set([1,2,3]);
let b=new Set([4,3,2]);

//并集
let union=new Set(...a,...b);

//交集
let intersect = new Set([...a].filter(x=>x.has(x)))

//差集
let difference = new Set([...a].filter(x=>!b.has(x)));
```
<p id="p2"></p>

## :sunny:WeakSet
<a href="#title">:whale2:回到目录</a><br>
#### :mag_right:含义
#### :mag_right:语法
<p id="p3"></p>

## :sunny:Map
<a href="#title">:whale2:回到目录</a><br>
#### :mag_right:含义和基本用法
#### :mag_right:实例的属性和方法
#### :mag_right:遍历方法
#### :mag_right:与其他数据结构的相互转换
<p id="p4"></p>

## :sunny:WeakMap
<a href="#title">:whale2:回到目录</a><br>
#### :mag_right:含义
#### :mag_right:WeakMap的语法
#### :mag_right:WeakMap的示例
#### :mag_right:WeakMap的用途
