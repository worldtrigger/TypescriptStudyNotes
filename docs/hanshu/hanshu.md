# 函数

## 函数定义类型

- 我们可以给函数定义类型,这个定义包括对参数和返回值的类型定义

```javascript
function addone(arg1: number, arg2: number): number {
  return arg1 + arg2;
}

//或者

const add = (arg1: number, arg2: number): number => {
  return arg1 + arg2;
};
```

## 完整的函数类型

- 一个函数的定义包括函数名,参数,逻辑和返回值。我们为一个函数定义类型的时候,完整的定义应该包括参数类型和返回值类型

```javascript
let add: (x: number, y: number) => number;
add = (arg1: number, arg2: number): number => arg1 + arg2;
add = (arg1: string, arg2: string): string => arg1 + arg2; // error
```

上面报的错误是

```bash

不能将类型"(arg1: string, arg2: string) => string"分配给类型"(x: number, y: number) => number"。
  参数"arg1"和"x" 的类型不兼容。
    不能将类型"number"分配给类型"string"。

```

## 使用接口定义函数类型

- 代码如下

```javascript
interface Add {
  (x: number, y: number): number;
}
let add: Add = (arg1: string, arg2: string): string => arg1 + arg2; // error 不能将类型“(arg1: string, arg2: string) => string”分配给类型“Add”
```

## 使用别名

```javascript
type Add = (x: number, y: number) => number;
let add: Add = (arg1: string, arg2: string): string => arg1 + arg2; // error 不能将类型“(arg1: string, arg2: string) => string”分配给类型“Add”
```

# 参数

## 可选参数,可选参数必须放到最后。通过?来判定

```javascript
type Add = (x?: number, y: number) => number; // error 必选参数不能位于可选参数后。

type Add2 = (x: number, y?: number) => number; //正确
```

## 默认参数

```javascript
const add = (x: number, y: number = 2) => {
  return x + y;
};
```

## 剩余参数

- 通过...来解构

```javascript
const handleData = (arg1, ...args) => {
  // 这里省略逻辑
  console.log(args);
};
handleData(1, 2, 3, 4, 5); // [ 2, 3, 4, 5 ]
```

再比如

```javascript
const handleData = (arg1: number, ...args: number[]) => {
  //
};
handleData(1, 'a'); // error 类型"string"的参数不能赋给类型"number"的参数
```

## 函数重载

- 最后必须写一个 any 函数 否则出不来

```javascript

function handleData(x: string): string[]; // 这个是重载的一部分，指定当参数类型为string时，返回值为string类型的元素构成的数组
function handleData(x: number): string; // 这个也是重载的一部分，指定当参数类型为number时，返回值类型为string
function handleData(x: any): any { // 这个就是重载的内容了，他是实体函数，不算做重载的部分
  if (typeof x === "string") {
    return x.split("");
  } else {
    return x
      .toString()
      .split("")
      .join("_");
  }
}
handleData("abc").join("_");
handleData(123).join("_"); // error 类型"string"上不存在属性"join"
handleData(false); // error 类型"boolean"的参数不能赋给类型"number"的参数。

```
