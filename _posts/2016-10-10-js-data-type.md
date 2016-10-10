---
layout: post
title:  数据类型
date:   2016/10/10 16:46:04
categories: Javascript
tag: 基本概念
---

* content
{:toc}

# 数据类型

> 5种基本类型
> - **Undifined**
> - **Null**
> - **Boolean**
> - **Number**
> - **String**
> - **Object**：本质上是由一组无序的名值对组成

***

### typeof操作符

- **“undefined”**——如果这个值未定义；
- **“boolean”**——如果这个值是布尔值；
- **“string”**——如果这个值是字符串；
- **“number”**——如果这个值是数值；
- **“object”**——如果这个值是对象或null；
- **“function”**——如果这个值是函数；

```javascript
var message = "hi";
alert(typeof message); //"string"
```
> 调用`typeof null`会返回“object”，因为特殊值null被认为是一个空的对象的引用。

### Undefined类型

Undefined类型只有一个值，即特殊的undefined。在使用var声明变量但未对其加以初始化时，这个变量的值就是undefined，例如

```js
var msg;
alert(msg == undefined); //true
```
> 未经初始化的值默认就会取得undefined值。
>
>对于未声明过的变量，只能执行一项操作，即使用typeof操作符检测其数据类型，不然会报错
>
>对未初始化和未声明的变量执行typeof操作符都会返回undefined值。

### Null类型

Null同样只有一个特殊值，就是null。从逻辑角度来看，null值表示一个空对象指针，而这也正是使用typeof操作符检测null值时会返回“object”的原因；

```js
var msg = null;
alert(typeof msg); //object
```
> 如果定义的变量准备在将来用于保存对象，那么最好将该变量初始化为null而不是其他值。这样一来，只要直接检查null值就可以知道相应的变量是否已经保存了一个对象的引用。例如

```js
if (car != null){
    //对car对象执行操作
}
```

> 实际上，undefined值是派生自null值的：`alert(null == undefined); //true`

# Boolean类型

Boolean类型只有两个字面值：true和false。这两个值和数字值没有相关，因此true不一定等于1；false也不一定等于0。

- Boolean()：转型函数，可以将一个值转化为其对应的Boolean值。因为所有类型的值都有与这两个Boolean值等价的值。至于返回的值是true还是false，取决于要转换的值得数据类型及其实际值。

```js
var msg = "hello world";
var msgBln = Boolean(msg); //true
```

数据类型 | 转换为true的值 | 转换为false的值
---|---|---
Boolean | true | false
String | 任何非空字符 | 空字符
Number | 任何非零数字值（包括无穷大） | 0和NaN
Object | 任何对象 | null
Undefined | n/a | undefined

### Number类型

Number类型包括八进制、十进制、十六进制。

- 八进制字面值的第一位必须是0，然后是八进制数字序列（0~7）。如果字面值中的数值超出了范围，那么前导0将被忽略，后面的数值将被当作十进制数值解析

    ```js
    var octalNum1 = 070; //八进制的56
    var octalNum2 = 079; //无效——解析为79
    var octalNum3 = 08; //无效——解析为8
    ```

- 十六进制的前两位必须是0x，后跟任何十六进制数字（0~9及A~F）。其中字母A~F大小写不区分。

    ```js
    var hexNum1 = 0xA; //十六进制的10
    var hexNum2 = 0x1f; //十六进制的31
    ```

- 浮点数值  定义：就是该数值中必须包含一个小数点

    - e表示法（科学记数法）：用e表示法表示的数值等于e前面的数值乘以10的指数次幂。

        ```js
        var floatNum1 = 3.125e7;  //等于31250000
        var floatNum2 = 3.125e-3;  //等于0.003125
        ```

    >关于浮点数值计算会产生舍入误差的问题。

- 数值范围

    js的最大数值保存在 **`Number.MAX_VALUE`** 中，最小数值保存在 **`Number.MIN_VALUE`** 中。
使用函数isFinite()，如果参数位于最小和最大值之间会返回true。

    ```js
    var result = Number.MAX_VALUE + Number.MIN_VALUE;
    alert(isFinite(result));  //false
    ```

- NaN：即非数值（Not a Number），是一个特殊的数值，这个数值用于表示一个本来要返回数值的操作数未返回数值的情况，从而避免抛出错误。
    >0除以0返回NaN，正数除以0返回Infinity，负数除以0返回-Infinity。

    - 任何涉及到NaN的操作（例如NaN/0）都会返回NaN。
    - NaN与任何值都不相等，包括NaN本身。`alert(NaN == NaN); //false`
    - isNaN()函数，在接收到一个值之后，会尝试将这个值转换为数值。无法转换则返回false。

        ```
        alert(isNaN(NaN)); //true
        alert(isNaN(10));  //false(转换成10)
        alert(isNaN("10"));  //false(转换成10)
        alert(isNaN("blue"));  //true
        alert(isNaN(true));  //false(转换成1)
        ```

- 数值转换
    - Number()：
        - true->1，false->0；
        - null->0；
        - undefined->NaN；
        - string
            - 数值忽略前导零
            - 十六进制转十进制
            - 空的话转为0
            - 乱七八糟转为NaN
    - parseInt()：

        ```JS
        var num1 = parseInt("10",2);  //按二进制解析
        var num2 = parseInt("10",8);  //按八进制解析
        var num3 = parseInt("10",10);  //按十进制解析
        var num4 = parseInt("10",16);  //按十六进制解析
        ```
    - parseFloat()：只解析十进制，一直解析到字符串末尾或者遇见一个无效的浮点数字字符为止。

### String类型

- 用于表示由零或多个16位的Unicode字符组成的字符序列，即字符串。
- toString()
    - 除了null和undefined值没有这个方法之外，其他类型都有；
    - 通过传递基数，可输出二、八、十六等任意有效进制的字符串值

        ```javascript
        var num = 10;
        alert(num.toString(2));  // "1010"
        ```
- String()
    - 如果值有toString()方法，则调用该方法（不带参数）并返回相应的结果；
    - 如果值是null，则返回null；
    - 如果值是undefined，则返回undefined；

### Object类型
对象其实就是一组数据和功能的集合。对象可以通过执行new操作符后跟要创建的对象类型的名称来创建。而创建Object类型的实例并为其添加属性以及方法，就可以创建自定义对象，例如：

    ```js
    var o = new Object();
    ```
- Object类型是所有它的实例的基础。换句话说，Object类型所具有的任何属性和方法也同样存在与更具体的对象中。

- Object的每个实例都具有下列属性和方法：
    - **constructor** ：保存着用于创建当前对象的函数。对于前面的例子而言，构造函数（constructor）就是Object()。
    - **hasOwnProperty(propertyNname)** ：用于检查给定的属性在当前对象实例中（而不是在实例的原型中）是否存在。其中，作为参数的属性名（propertyNname）必须以字符串形式指定（例如：o.hasOwnProperty("name")）。
    - **isPrototypeOf(object)** ：用于检查传入的对象是否是传入对象的原型（原型的详细介绍参考《javascript高级程序设计第5章》）。
    - **propertyIsEnumerable(propertyNname)** ：用于检查给定的属性是否能够使用 `for-in` 语句来枚举。其中，作为参数的属性名（propertyNname）必须以字符串形式指定。
    - **toLocaleString()** ：返回对象的字符串表示，该字符串与执行环境的地区对应。
    - **toString()** ：返回对象的字符串表示。
    - **valueOf()** ：返回对象的字符串、数值或布尔值表示。通常与toString()方法的返回值相同
