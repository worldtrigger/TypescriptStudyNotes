# 类型断言

- 我们在获取类型的时候为了方便使用可以使用类型断言来判定他是哪一类类型

## 关键字 as

```javascript

const getLength = (target: number | string): number => {
  if ((target as string).length) {
    return (target as string).length;
  } else {
    return Number(target);
  }
};

console.log(getLength("222"));

console.log(getLength(222));

```

这里特别注意的就是不能用 `target as string` 必须用

`(target as string).length` 来判断

> as 只不过就是强制把变量的类型转变为你想要的类型 不能作为判断的依据
