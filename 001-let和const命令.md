# -------------------------let和const命令-----------------------
## 目录
<p id="title"></p>
<a href="#p1">:snowflake:let命令</a><br>
<a href="#p2">:snowflake:块级作用域</a><br>
<a href="#p3">:snowflake:const命令</a><br>
<a href="#p4">:snowflake:顶级对象的属性</a><br>
<a href="#p4">:snowflake:global对象</a><br>
<p id="p1"></p>

## :sunny:let命令
<a href="#title">:whale2:回到目录</a><br>
#### :mag_right:基本用法
**let**命令,用于声明变量,类似于var,但是**所声明的变量只能在let命令所在的代码块内有效**
```JavaScript
{
    let a=10;
    var b=1;
}
a  //a is not difined
b  //1
```
for循环的计数器很适合使用let命令
```javascript
for(let i=0;i<10;i++){
    //
}
console.log(i);
//i is not defined;
```
这里的i只在for循环体内有效,再循环体外引用就会报错<br>
**对比**:var与let
```JavaScript
var a=[];
for(var i=0;i<10;i++){
    a[i]=function(){
        console.log(i);
    };
}
a[6]();  //10
-----------------------
var a=[];
for(let i=0;i<10;i++){
    a[i]=function(){
        console.log(i);
    };
}
a[6]();   //6
```
i如果是var声明的话,为全局变量,每一次循环,变量i的值都会发生变化,console.log(i)中的i指向全局的i,导致运行时输出的是最后一轮的i值,就是10<br>
i是let声明的话,i只在本轮循环中有效,于是输出6<br>

---
**疑问:** 每一轮循环的变量都是i都是重新声明的,那他是怎么知道上一轮循环的值从而计算本轮循环的值呢?<br>
因为JavaScript引擎内部会记住上一轮循环的值,初始化本轮的i时,就是在上一轮的基础上进行计算

---
for循环的特殊之处:**设置循环变量的那一部分是一个父作用域,而循环体内部是一个单独的子作用域**
```JavaScript
for(let i=0;i<3;i++){
    let i='abc';
    console.log(i);
}
//abc
//abc
//abc
```
#### :mag_right:不存在变量提升
var命令会发生**变量提升**的问题,即变量在声明之间就可以使用,值为undefined.let命令改变了语法行为,他所声明的变量一定要在声明后使用,否则报错
```JavaScript
//var的情况下
console.log(foo);  //输出undefined
var foo=2;

//let的情况
console.log(bar);  //报错
let bar = 2;
```
#### :mag_right:暂时性死区
只要在块级作用域中**存在**let命令,他所声明的变量就"绑定"(binding)这个区域,不受外部的影响
```JavaScript
var tmp=123;
if(true){
    tmp = 'abc';  //报错
    let tmp;  //因为在此使用了let,所以(不存在变量提升)报错
}
```
**明确规定,如果区块存在let和const命令,则这个区块对这些声明的变量一开始就形成封闭区域,只要在声明之前就使用这些变量,就会报错-->叫做"暂时性死区(temporal dead zone,简称TDZ)"**
```JavaScrip
if(true){
    //TDZ 开始
    tmp='abc';  //报错
    console.log(tmp);
    
    let tmp;  //TDZ结束
    console.log(tmp);  //undefined
    
    tmp=3;
    console.log(tmp);  //3
}
```
"暂时性死区"也意味着typeof不再是一个白分之百安全的操作
```JavaScript
typeof x;
let x;  //报错
```
**如果一个变量根本没有被声明,使用typeof反而不会报错**<br>
有些死区比较隐蔽,不太容易发现
```JavaScript
function bar(x=y,y=2){
    return [x,y];
}
bar();  //报错
```
下面的代码也会报错
```JavaScript
// 不报错
var x=x;
//报错

let x=x; 
```
**暂时性死区的本质:** 只要进入当前作用域,所要使用的变量就已经存在,但是不可获取,只有等到声明变量的那一行代码出现,才可以获取和使用该变量
#### :mag_right:不允许重复声明
let不允许在相同作用域重复声明同一个变量
```JavaScript
//报错
function (){
    let a=10;
    var a=1;
}

//报错
function (){
    let a=10;
    let a=1;
}

//不能在函数内部重新声明参数
function func(arg){
    let arg; //报错
}

function func(arg){
  {
      let arg;  //不报错
  }
}
```

<p id="p2"></p>

## :sunny:块级作用域
<a href="#title">:whale2:回到目录</a><br>
#### :mag_right:为什么需要块级作用域
#### :mag_right:ES6的块级作用域
#### :mag_right:块级作用域和函数声明
#### :mag_right:do表达式
<p id="p3"></p>

## :sunny:cconst命令
<a href="#title">:whale2:回到目录</a><br>
#### :mag_right:基本用法
#### :mag_right:本质
#### :mag_right:ES6声明变量的6种方法
<p id="p4"></p>

## :sunny:顶级对象的属性
<a href="#title">:whale2:回到目录</a><br>
<p id="p5"></p>

## :sunny:global对象
<a href="#title">:whale2:回到目录</a><br>
