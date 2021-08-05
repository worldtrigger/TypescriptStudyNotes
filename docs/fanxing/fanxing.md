# 泛型

泛型的作用就是当我们不知道变量类型的时候,又想返回变量的类型使用

## 简单使用

- demo

```javascript
const getArray = <T>(arg1: T, times: number = 5): T[] => {
  let arr = [];
  for (let i = 0; i < times; i++) {
    arr.push(arg1);
  }
  return arr;
};

console.log(getArray('哈哈'));

//最后的结果
/* 
[ '哈哈', '哈哈', '哈哈', '哈哈', '哈哈' ]
*/
```

## 泛型变量

当我们使用泛型的时候,你在处理这个数据的时候就必须把这个数据当作任意类型来处理.这就意味着不是所有类型做的操作都不能做,不是所有类型都能调用的方法不能调用

```javascript
const getLength = <T>(arg1: T): number => {
  return arg1.length;
};

//直接报错
```

## 接口形式来定义泛型

```javascript
interface GetArray {
  <T>(arg: T, times: number): T[];
}
const getArray: GetArray = <T>(arg: T, times: number): T[] => {
  return new Array(times).fill(arg);
};
```

## 泛型约束(继承)

```javascript

interface a1 {
  name: string;
}

const getLength = <T extends a1>(a1: T): T => {
  return a1;
};
getLength({ name: '哈哈', sex: '男' });

```
