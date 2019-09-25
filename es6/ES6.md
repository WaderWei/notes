# ES6笔记

### 简介

ES6（2015），ECMAScript6.0，是JavaScript的 下一个版本标准。JavaScript是ECMAScript的实现，ECMAScript是JavaScript的标准。



### let 和 const

* let声明的变量只在let命令所在的代码块中有效
* const声明一个只读常亮，一旦声明不能再被更改



let代码块中有效，var全局范围内有效且存在变量提升(即定义在后面的变量，前面可以访问到).

``` JavaScript
{
    var a = 3;/*全局都共享*/
    let b = 2;/*被限定在代码块中*/
}
console.log(a);/*3*/
//console.log(b);/*Uncaught ReferenceError: a is not defined*/
```



const声明一个只读变量，声明之后不允许修改，必须初始化。

``` javascript
{
    const PI = 3.14;
    /*编译器直接报错*/
    PI = 3.15;/*attempt to assign to const or readonly variable*/
    console.log(PI);
}
```

 注：这里的常量保证的只是地址不变，如果是基本类型，则保证数据不变；但如果是对象，只是保证对象的引用地址不变，对象里面的属性值依然可以改变

```javascript
{
    const person={
        name:"wade",
        age:20
    }
    person.name="peter";
    console.log(person);/*{name: "peter", age: 20}*/
    console.log(person.name);/*peter*/
}
```



### 解构函数

> 针对**数组**或者**对象**进行模式匹配，然后对其中的变量进行赋值。
>
> 解构的源=解构的目标 ，注意：左右解构要一样

#### 数组（Array）

1. 左右映射，对应

   ```JavaScript
   //基本
   {
       let [a, b, c] = [1, 2, 3];
       console.log(a, b, c)//1 2 3
   }
   //嵌套
   {
       let [a, [b, c]] = [3, [5, 7]];
       console.log(a, b, c)//3 5 7
   }
   
   //忽略
   {
       let [a, , b, c,] = [1, 3, 5, 6, 7];
       console.log(a, b, c)//1 5 6
   }
   ```

   2. 默认值，没有对应的可以给默认值

      ```JavaScript
      {
          let [a = 1, b] = [, 10];
          console.log(a,b)//1 10
      }
      ```

   3. 剩余运算符

      ```JavaScript
      {
          let [a,...b]=[1,2,3,5]
          console.log(a)//1
          console.log(b)//[2,3,5]
      }
      ```

   #### 对象（Object）

   对象解构与数组解构类似，注意{}与[]区别，左右对应即可，能匹配上就是右边的值，不能匹配上就是undefined。

   ```JavaScript
   {
       let {name, age} = {name: 'wade', age: 18};
       console.log(name, age)//wade 18
   }
   
   {
       let {name,...other}={name:'wade',age:12,sex:'male',height:'150'}
       console.log(name)//wade
       console.log(other)//{age: 12, sex: "male", height: "150"}
   }
   ```

### Symbol

> 定义一种新的类型，表示独一无二的值，最大的用法用来定义唯一的属性名。
>
> ES6 数据类型除了 Number 、 String 、 Boolean 、 Object、 null 和 undefined ，还新增了 Symbol 。

#### 用法

* Symbol 函数栈不能用 new 命令，因为 Symbol 是原始数据类型，不是对象。可以接受一个字符串作为参数，为新创建的 Symbol 提供描述，用来显示在控制台或者作为字符串的时候使用，便于区分。

```JavaScript
{
    let str1 = Symbol("abc");
    console.log(str1)//Symbol(abc)
    console.log(typeof(str1));symbol

    let str2 =Symbol("abc");
    console.log(str1 == str2)//false
}
```

#### 作为属性名，保证属性不重名

```JavaScript
let name = Symbol("name");
let age = Symbol("age");
{
    let obj = {
        [name]: "wade",
        [age]: 18
    }
    console.log(obj[name],obj[age])//wade 18
    console.log(obj.name)//undefined
}
```

注：只能通过obj[symbolName]去取值，不能通过点。



### Map 与 Set

#### Map

> Map 对象保存键值对。**任何值**(对象或者原始值) 都可以作为一个键或一个值。
>
> map.set(key:any,value:any)

#### Maps 和 Objects 的区别

- 一个 Object 的键只能是字符串或者 Symbols，但一个 Map 的键可以是任意值。
- Map 中的键值是有序的（FIFO 原则），而添加到对象中的键则不是。
- Map 的键值对个数可以从 size 属性获取，而 Object 的键值对个数只能手动计算。
- Object 都有自己的原型，原型链上的键名有可能和你自己在对象上的设置的键名产生冲突。

用法：

```javascript
{
    let map = new Map();
    let str = "key1";
    map.set(str, "123");
    let obj = {};
    map.set(obj, {name: 10});
    let bool = true;
    map.set(bool, 123);
    let boo=true;
    map.set(boo,234);//当map中存在此key时，会将原来的值替换

    console.log(map.get(str))//123
    console.log(map.get(obj))//{name:10}
    console.log(map.get(bool))//234
    console.log(map.get(boo))//234
}
```

#### for ... of 遍历

```JavaScript
//for...of
for (let [key, val] of map) {
    console.log(key, val)
}

for (let [key,val] of map.entries()){
    console.log(key,val);
}

for (let key of map.keys()){
    console.log(key)
}

for (let val of map.values()){
    console.log(val)
}
```

#### forEach

```JavaScript
map.forEach(function (val, key) {
    console.log(val,key)
})
```



#### Map <-----> Array

```javascript
{
    let map=new Map();
    map.set("k1","wade");
    map.set("k2","peter");

    //map to array
    let arr = Array.from(map);
     /*
     (2) [Array(2), Array(2)]
          0: (2) ["k1", "wade"]
          1: (2) ["k2", "peter"]*/
    console.log(arr)
    //array to map
    let mapFormArr = new Map(arr);
    
    /*
    Map(2) {"k1" => "wade", "k2" => "peter"}
        [[Entries]]
        0: {"k1" => "wade"}
        1: {"k2" => "peter"}
    * */
    console.log(mapFormArr)
}
```

### Set

Set 对象允许你存储任何类型的唯一值，无论是原始值或者是对象引用。

#### Set 中的特殊值

Set 对象存储的值总是唯一的，所以需要判断两个值是否恒等。有几个特殊值需要特殊对待：

- +0 与 -0 在存储判断唯一性的时候是恒等的，所以不重复；
- undefined 与 undefined 是恒等的，所以不重复；
- NaN 与 NaN 是不恒等的，但是在 Set 中只能存一个，不重复。



```javascript
{
    let set = new Set();
    set.add(1);
    set.add("a");
    set.add("a");
    set.add({name: "wade"})


    console.log(set)//Set(3) {1, "a", {…}}
}
```

[集合操作详情](https://www.cnblogs.com/xiaoyulive/p/7906548.html)



