# 类型概述

## 数字类型

- 代码

```javascript
let a1: number = 17;
a1 = '哈哈'; //报错误
```

## 布尔类型

- 代码

```javascript
let a1: boolean = false;
a1 = true; //正确
a1 = '123'; //错误
```

## 字符串

- 代码

```javascript
let str: string = 'abc'; //字符串
str = 123; //错误
```

## 数组

- 数组有两种形式。

第一种: (类型)[] 这种方式

```javascript
let arr1: (number | string)[] = [1, 2, '哈哈'];
```

第二种:Array<number>不推荐

```javascript
let arr2: Array<number> = [1, 2, 3];
```

## null 和 undefined

```javascript
let u: undefined = undefined; // 这里可能会报一个tslint的错误：Unnecessary initialization to 'undefined'，就是不能给一个值赋undefined，但我们知道这是可以的，所以如果你的代码规范想让这种代码合理化，可以配置tslint，将"no-unnecessary-initializer"设为false即可
let n: null = null;
```

## Object

- 代码如下 , 一般情况下我们用的都是接口类型

```javascript
let obj: object;
obj = { name: 'Lison' };
obj = 123; // error 不能将类型“123”分配给类型“object”
```

## 元组

元组可以看作是数组的拓展,他表示已知元素数量和类型的数组.

```javascript
let tuple: [string, number, boolean] = ['1', 2, true];
```

`元组各个位置上的元素类型都要对应，元素个数也要一致`

```javascript
tuple[1] = 223;
```

我们还可以给单个元素赋值

## 枚举

- 关键字 enum

```javascript

enum Roles{
 super,
 admin,
 user
}

```

- 当我们调用的时候只需要

```javascript
console.log(Roles.super); //结果就是0
console.log(Roles.admin); //结果就是1
console.log(Roles.user); //结果就是2
```

`当没有指定的数值的时候枚举默认值从0开始,指定了就从指定后的值开始`

- 指定值了

```javascript
enum Roles{
  super=3,
  admin,
  user
}
```

调用的时候

```javascript
console.log(Roles.super); //3
console.log(Roles.admin); //4
console.log(Roles.user); //5
```

## Any

- any 类型就是不限制,什么类型都行

```javascript
let value: any = 123;
value = '456';
value = true;
```

`请注意不要滥用any,因为如果把任何值指定为any,Typescript就失去了意义`

## void

void 表示没有返回值

```javascript
const consoleText = (name1: string): void => {
  console.log(consoleText);
};
```

## never

- never 一般用在抛出异常

```javascript
const errorFunc = (message: string): never => {
  throw new Error(message);
};
```
