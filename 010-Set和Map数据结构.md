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
与Set结构类似,但是有两个区别:<br>
WeakSet的成员只能是对象,而不能是其他成员;WeakSet中的对象都是弱对象,即垃圾回收机制不考虑WeakSet对该对象的引用(如果其他对象不再引用该对象,那么垃圾回收机制会自动回收该对象所占用的内存)

#### :mag_right:语法
语法:
```JavaScript
const a=new WeakSet();
```
可以接收一个数组或类似数组的队形为参数(任何具备iterable接口的对象都可以作为WeakSet对象的参数)
```JavaScript
const a=[[1,2].[3,4]];
const ws=new WeakSet(a);
// {[1,2],[3,4]}
```
成为WeakSet的成员的是a数组的成员,而不是它本身
```JavaScript
const b=[3,4];
const a=new WeakSet(b);  //报错
```
**WeakSet有3个方法**<br>
+ WeakSet.prototype.add(value): 添加一个新成员
+ WeakSet.prototype.delete(value): 清除指定成员
+ WeakSet.prototype.has(value): 返回一个布尔值,表示某个值是不是在实例中
<br>
WeakSet没有size属性,没有办法遍历其成员
<p id="p3"></p>

## :sunny:Map
<a href="#title">:whale2:回到目录</a><br>
#### :mag_right:含义和基本用法
JavaScript中对象本质上是键值对的集合,但只能用作字符串作为键名,为了解决这个问题,ES6提供了Map数据结构,类似于对象,但各种类型的值(包括对象)都可以作为键
```JavaScript
const m = new Map();
const o={p:'hello,world'};

m.set(o,'content')
m.get(o)  //"content"

m.has(o);  //true
m.delete(o) //true
m.has(o)   //false
```
Map结构也可以接收一个数组作为参数.该数组的成员是一个个表示键值对的数组
```JavaScript
const m=new Map([
    ['name','guixu'],
    ['title','Author']
])

m.size();   //2
m.has('name')  //true
m.get('name')   //guixu
m.has('title')  //true
m.get('title')  //Author
```
Map构造函数接受数组作为参数,实际上执行的是下面的算法
```JavaScript
 const items=[
    ['name','guixu'],
    ['title','Author']
 ]
 
 const map = new Map();
 
 items.forEach(([key,value])=>map.set(key,value));
```
不仅仅是数组,只要是就有iterable接口且每个成员都是**一个双元素数组的数据结构**,都可以当做Map构造参数的参数
```JavaScript
const set = new Set([
    ['foo',1],
    ['bar',2]
]);
const m1 = new Map(set);
m1.get('foo');  //1

const m2=new Map([['baz',3]]);
const m3=new Map(m2);
m3.get('baz')//3
```
如果对同一个键多次赋值,后面的值将覆盖前面的值,如果读取一个未知的值,则返回undefined.

---
**注意**: 只有对同一个对象的引用,Map结构才将其视为同一个键

---
```JavaScript
const m=new Map();

m.set(['a'],555);
m.get(['a']);  //undefined
```
上面的set和get方法表面上是针对同一个键,实际上却是两个值,内存地址不一样,<br>
同理,同样的值的两个实例在Map结构中被视为两个键
```JavaScript
const m=new Map();

const k1=['a'];
const k2=['a'];

m
 .set(k1,111)
 .set(k2,222)

m.get(k1);  //111
m.get(k2);  //222
```
如果Map的键是一个简单类型的值(数字,字符串,布尔值),则只要两个值严格相等,就视为一个键,包括+0和-0,NaN也视为同一个键
```JavaScript
let m=new Map();

m.set(-0,111);
m.get(+0);  //111

m.set(true,1);
m.set('true',2);
m.get(true);  //1

m.set(undefined,3);
m.set(null,4);
m.get(undefined);  //3

m.set(NaN,111);
m.get(NaN)  //123
```
#### :mag_right:实例的属性和方法
+ size属性:返回Map结构的成员总量
+ set(key,value):设置key所对应的键值,然后返回整个Map结构,如果key已有其值,则被更新,set方法返回的是当前的Map对象,所以可以采用链式写法
```JavaScript
let map=new Map();
  .set(1,'a')
  .set(2,'b')
  .set(3,'c');
```
+ get(key):读取key对应的键值,如果没有,则返回undefined
+ has(key):返回一个布尔值,表示某个键是否在Map数据结构中
+ delete(key): 删除某个键,成功返回true,否则false
+ clear(): 清除所有成员,没有返回值
#### :mag_right:遍历方法
提供了3个遍历器函数和一个遍历方法
+ key():返回建名
+ value(): 返回键值
+ entries(): 返回所有成员
+ forEach(): 遍历Map所有成员
<br>
**Map的遍历顺序就是插入顺序**
```JavaScript
let map =new Map([
    ['f','no'],
    ['t','yes']
]);

for(let key of map.key()){
    console.log(key);
}
//"f"  "t"

for(let key of map.value()){
    console.log(key);
}
//"no" "yes"

for(let item of map.entries()){
    console.log(item[0],item[1]);
}
//"f" "no"
//"t" "yse"
//或者
for(let [key,value] of map.entries(){

}
```
Map结构的默认遍历器接口(Symbol.iterator属性)就是entries()方法<br>
Map结构转换为数据结构最快的方法就是结合拓展运算符(...)

```JavaScript
const map=new Map([
    [1,"one"],
    [2,"two"],
    [3,three]
]);

[...map.key()]  //[1,2,3]
[...map.value()]  //['one','two','three']
```
结合数组的map和filter方法,可以实现Map的遍历和过滤(**Map本身没有map和filter方法**)
```JavaScript
const map0=new Map();
    .set(1,'a')
    .set(2,'b')
    .set(3,'c');
const map=new Map(
    [...map0].filter(([k,v])=>k<3)
);
// 产生的Map结构:{1=>'a',2=>'b'}
```
Map还有一个forEach方法,与数组的forEach方法类似
```JavaScript
map.forEach(function(value,key,map){
    console.log("key: %s,value: %s",key,value);
});
```
forEach方法还可以接受第二个参数,用于绑定this
#### :mag_right:与其他数据结构的相互转换
+ Map转为数组:最常用的方法就是扩展运算符(...)
```JavaScript
const myMap=new Map()
    .set(true,7)
    .set({foo:3},['abc']);
[...myMap]  // [[true,7],[{foo:3},['abc']]]
```
+ 数组转换为Map:将数组传入Map构造函数就可以
```JavaScript
new Map([
    [true,7],
    [{foo:3},['abc']]
])
```
+ Map转为对象:如果Map所有键都是字符串,则可以转为对象
```JavaScript
function strMapToObj(strMap){
    let obj=Object.create(null);
    for(let [k,v] of strMap){
        obj[k]=v;
    }
    return obj;
}

const myMap=new Map();
    .set('yes',true)
    .set('no',false);
strMapToObj(myMap);  //{yes:true,no:false}
```
+ 对象转为Map
```JavaScript
function objToStrMap(obj){
    let strMap = new Map();
    for(let k of Object.keys(obj)){
        strMap.set(k,obj[k]);
    }
    return strMap;
}

objToStrMap({yes:true,no:false});  //Map {"yes"=>true,"no"=>false}
```
+ Map转JSON<br>
第一种情况:Map的键名都是字符串,选择转为对象JSON
```JavaScript
function strMapToJson(strMap){
    return JSON.stringify(strMapToObj(strMap));
}

let myMap = new Map().set('yes',true).set('no',false);
strMapToJson(myMap);  //'{"yes": true,"no": false}';
```
另外一种情况,Map的键名有非字符串,选择转为数组JSON
```JavaScript
function mapToArrayJson(map){
    return JSON.stringify([...map]);
}
let myMap=new Map().set(true,7).set({foo:3},['abc']);
mapToArrayJson(myMap);
//'[[true,7],[{"foo":3},["abc"]]]'
```
+ JSON转为Map
```JavaScript
function jsonToMap(jsonStr){
    return objToStrMap(JSON.parse(jsonStr))
}
```
<p id="p4"></p>

## :sunny:WeakMap
<a href="#title">:whale2:回到目录</a><br>
#### :mag_right:含义
与Map类似,但只接收对象作为键名(null除外),键名所指向的对象不计入垃圾回收机制
#### :mag_right:WeakMap的语法
```JavaScript
const wm=new WeakMap()
```
#### :mag_right:WeakMap的示例
#### :mag_right:WeakMap的用途
典型应用场景就是以DOM节点作为键名的场景
```JavaScript
let myElement = document.getElementById('logo');
let myWeakmap=new WeakMap();

myWeakmap.set(myElement,{timesClicked:0});

myElement.addEventListener('click',function(){
    let logoData=myWeakmap.get(myElement);
    logeData.timesClicked++;
},false)
```
一旦DOM节点删除,该状态就会自动消失,不存在泄漏风险<br>
WeakMap的另一个用处是部署私有属性
```JavaScript
const _counter = new WeakMap();
const _action = new WeakMap();

class Countdown {
    constructor(counter,action){
        _counter.set(this,counter);
        _action.set(this,action);
    }
    dec() {
        let counter = _counter.get(this);
        if(counter<1) return;
        counter--;
        _counter.set(this,counter);
        if(counter==0){
            _action.get(this)();
        }
    }
}

const c=new CountDown(2,()=>console.log('DONE'));
c.dec()
c.dec()
//DONE
```
如果删除实例,两个内部属性也会消失,不会造成内存泄漏
