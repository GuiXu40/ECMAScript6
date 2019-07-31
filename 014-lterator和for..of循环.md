# ----------------------Iterator和for...of循环-----------------------
## 目录
<p id="title"></p>
<a href="#p1">:snowflake:Iterator(遍历器)的概念</a><br>
<a href="#p2">:snowflake:默认Iterator接口</a><br>
<a href="#p3">:snowflake:调用Iterator接口的场合</a><br>
<a href="#p4">:snowflake:字符串的Iterator接口</a><br>
<a href="#p5">:snowflake:Iterator和Generator函数</a><br>
<a href="#p6">:snowflake:遍历器对象的return(),throw()</a><br>
<a href="#p7">:snowflake:for...of循环</a><br>
<p id="p1"></p>

## :sunny:Iterator(遍历器)的概念
<a href="#title">:whale2:回到目录</a><br>
遍历器(Iterator)是一种接口机制,为各种不同的数据结构提供统一的访问机制,任何数据结构,只要部署了Iterator接口,就可以完成遍历操作
<br>
**Iterator的作用**: 一是为各种数据结构提供一个统一的,简便的的访问接口;二是使得数据结构的成员能按照某种次序排列;三是ES6创造了一种新的遍历命令--for...of<br>
Iterator的遍历过程如下:<br>
1. 创建一个指针对象,指向当前数据结构的起始位置(遍历器对象本质就是一个指针对象)<br>
2. 第一次调用指针对象的next方法,可以将指针指向数据结构的第一个成员<br>
3. 第二次调用指针对象的next方法,指针就指向数据结构的第二个成员
4. 不断调用指针对象的next方法,直到他指向数据结构的结束位置
<br>
下面是一个模拟next方法返回值的例子
```JavaScript
var it = makeIterator(['a','b']);

it.next(); //{value :"a",done :false}
it.next(); //{value :"b",done: false}
it.next(); //{value:undefined,done: true}

function makeIterator(array){
    var nextIndex =  0;
    return {
        next:function(){
            return nextIndex<array.length?
            {value: array[nextIndex++],done: false} :
            {value: undefined,done:true}
        }
    }
}
```
done表示遍历是否结束<br>
对于遍历器对象,done:false和value:undefined属性都是可以省略的,因此上面的方法可以简写:
```JavaScript
function makeIterator(array){
    var nextIndex =  0;
    return {
        next:function(){
            return nextIndex<array.length?
            {value: array[nextIndex++]} :
            {done:true}
        }
    }
}
```
<p id="p2"></p>

## :sunny:默认Iterator接口
<a href="#title">:whale2:回到目录</a><br>
#### :mag_right:
<p id="p3"></p>

## :sunny:调用Iterator接口的场合
<a href="#title">:whale2:回到目录</a><br>
#### :mag_right:
<p id="p4"></p>

## :sunny:字符串的Iterator接口
<a href="#title">:whale2:回到目录</a><br>
#### :mag_right:
<p id="p5"></p>

## :sunny:Iterator和Generator函数
<a href="#title">:whale2:回到目录</a><br>
#### :mag_right:
<p id="p6"></p>

## :sunny:遍历器对象的return(),throw()
<a href="#title">:whale2:回到目录</a><br>
#### :mag_right:
<p id="p7"></p>

## :sunny:for..of循环
<a href="#title">:whale2:回到目录</a><br>
#### :mag_right:数组
#### :mag_right:Set和Map结构
#### :mag_right:计算生成的数据结构
#### :mag_right:类似数组的对象
#### :mag_right:对象
#### :mag_right:与其他遍历语法的比较
