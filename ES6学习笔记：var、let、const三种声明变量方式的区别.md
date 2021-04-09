# var 、let、const三种声明变量方式的区别
<table><tr><td bgcolor="fa6400"><font color=white size=5>概述</font></td></tr></table>

| 命令                 | var      | let                  | const                                                    |
| -------------------- | :------- | :------------------- | :------------------------------------------------------- |
| 变量有效区域         | 全局有效 | 块级作用域内         | 块级作用域内                                             |
| 是否允许重定义变量   | 允许     | 同一作用域内不允许   | 同一作用域内不允许                                       |
| 是否有变量提升       | 有       | 无                   | 无                                                       |
| 变量声明之前是否可用 | 可用     | 不可用（暂时性死区） | 不可用（暂时性死区）                                     |
|                      |          |                      | 声明只读变量（常量）且必须立即初始化                     |
|                      |          |                      | 声明复合对象时，数据地址不可修改，对象成员变量可以修改。 |
|                      |          |                      | 使用freeze冻结数据                                       |



# 1 let关键字

## 1.1 基本方法

​		ES6新增块级作用域。

​		ES5有两种声明变量的方法：<font color=red>var</font>、<font color=red>function</font>命令。

​		ES6有六种声明变量的方法：<font color=red>var</font>、<font color=red>function</font>、<font color=red>let</font>、<font color=red>const</font>、<font color=red>import</font>、<font color=red>class</font>命令。

​		let命令，用于声明变量。用法类似var，但所声明的变量只在let命令所在的代码块内有效。

```javascript
{
    let a =10;
    var b = 20;
}
console.log(a);		//[引用错误] ReferenceError:a is not defined
console.log(b);		//20
```

​		代码在let声明的块级作用域以外使用会报错，var却不会，所以**let只能所定义的块级作用域内部使用**。

```javascript
{
	var a = 10;
    var a = 20;
    console.log(a);		//20
}
{
    let b = 10;
    let b = 20;
    console.log(b);		//[语法错误] SyntaxError:Indentifier 'a' has already been declared
}
```

​		**var声明的变量可以重新定义覆盖，而let不允许在同一作用域内重复声明变量。**

​		let命令适合在for循环中使用。

​		ES6块级作用域可以无限嵌套，可替代ES5的匿名函数IIFE。

```javascript
{
    let a = 10;
    console.log(a);			//10
    {
        let b = 20;
    	console.log(b);		//20
    }
}
```

​		ES5严格模式下，函数不能再块级中声明，ES6明确规定可以在块级作用域中声明函数。但在块级作用域以外不能调用。（浏览器可以忽略此规则，但尽量避免在块级作用域内声明函数）

## 1.2 不存在变量提升

​		变量提升即在定义变量之前使用变量会显示var为undefined，并不会报错；而**let所定义的变量没有变量提升的问题**。

```javascript
console.log(a);		//undefined
var a = 10;
console.log(b);		//[引用错误] ReferenceError: a is not defined
let b = 20;
```

## 1.3 暂时性死区

​	ES6明确规定，若区块内存在let或const命令，则此区块对这些命声明命的变量从一开始就形成封闭作用域。

​	**在代码块内，变量在let命令声明之前不可用，只能在声明之后才能使用，此区域被称为“暂时性死区”。**

```javascript
{
    var a = 10;
    if(true){
        concole.log(a);		//[引用错误] ReferenceError: Cannot access 'a' before initialization
        let a;
	}
}
```

# 2 const关键字

## 2.1 基本方法

​		声明一个只读的常量，一旦声明，其值不能改变且必须立即初始化。除此之外，用法与let一致。

​		当const声明的不是普通类型的值，而是数据的地址（复合对象）的时候。数据的地址不可变，复合对象的成员变量可以更改；若要冻结数据，可以使用freeze。

```javascript
{
    const obj1 = {
        x:10,
    };
    obj1.y = 20;		//更改成员变量
    obj1.z = 30;
    console.log(obj1.y);	
    const obj2 = Object.freeze({});
    obj2.x = 10;		//常规模式下，该行代码无效，严格模式下会报错
    console.log(obj2.x);//undefined
}
```
<table><tr><td bgcolor="fa6400"><font color=white size=5>总结</font></td></tr></table>

| 命令                 | var      | let                  | const                                                    |
| -------------------- | :------- | :------------------- | :------------------------------------------------------- |
| 变量有效区域         | 全局有效 | 块级作用域内         | 块级作用域内                                             |
| 是否允许重定义变量   | 允许     | 同一作用域内不允许   | 同一作用域内不允许                                       |
| 是否有变量提升       | 有       | 无                   | 无                                                       |
| 变量声明之前是否可用 | 可用     | 不可用（暂时性死区） | 不可用（暂时性死区）                                     |
|                      |          |                      | 声明只读变量（常量）且必须立即初始化                     |
|                      |          |                      | 声明复合对象时，数据地址不可修改，对象成员变量可以修改。 |
|                      |          |                      | 使用freeze冻结数据                                       |

