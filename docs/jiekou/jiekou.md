# 接口

使用接口可以定义几乎任意结构

## 基本用法

- 关键字 interface

```javascript
interface Person {
  name: string;
}
const PersonOne: Person = {
  name: "哈哈哈",
};
```

## 可选属性

- 一般情况 使用 ? 来表示可选属性,可有可无

```javascript
interface Person2 {
  name: string;
  color?: string;
}

const Man: Person2 = {
  name: "哈哈",
};
```

## 绕开多余属性检查

有的时候我们不希望 Typescript 这么严格的对数据检查,我们需要绕开多余性检查

1.使用?变成可选属性

```javascript
interface Vegetables {
  color?: string;
  type: string;
}

const VegetablesResult: Vegetable = {
  type: "哈哈哈",
};
```

2.添加索引签名

```javascript
interface Vegetables {
  color: string;
  type: string;
  [prop: string]: any;
}

const food = {
  color: "red",
  type: "水果",
  price: 30,
};
```

## 只读属性

- 接口设置为只读属性

```javascript
interface Role{
  readonly name: string;
  readonly sex:  string;
}

const shili:Role = {
  name:'今天',
  sex:'男'
}

shili.name = '明天'  //报错误

```

## 函数类型

- 接口类型还可以描述函数

```javascript
interface AddFunc {
  (num1: number, num2: number): number;
}

const add2: AddFunc = (arg1: number, arg2: number) => {
  return arg1 + arg2;
};

add2(1, 3);
```

- 接口里面除了函数类型还有其他的类型

```javascript
interface Func {
  (num1: number, num2: number): number;
}

interface typeAddson {
  id: number;
  type: string;
  add: Func;
}

const typeResult: typeAddson = {
  id: 1,
  type: "哈哈",
  addPosition: (arg1, arg2) => {
    return arg1 + arg2;
  },
};

typeResult.addPosition(1, 2);
```

## 接口的高阶用法

### 索引签名

```javascript

interface RoleDic{
  readonly [id:number] :string;
}

const role:RoleDic = {
  0:"super_admin"
}

role[0] = 'Hello';  //error 类型报错误 因为readonly只读

```

## 接口继承

### 接口和接口的继承 extends

```javascript
interface Person {
  name: string;
}

interface Man extends Person {
  sex: string;
}

const Man_People: Man = {
  name: "哈哈哈",
  sex: "男",
};
```

### 接口和类之间的继承

- 接口继承类 extends

```javascript
class Person {
  name: string;
  constructor(name: string) {
    this.name = name;
  }
  printname() {
    return this.name;
  }
}
interface Man extends Person {
  sex: string;
}

const Man_People: Man = {
  name: "哈哈哈",
  sex: "男",
  printname: () => {
    return Man_People.name;
  },
};

console.log(Man_People.printname());
```

- 类继承接口 implements

```javascript
interface Man {
  sex: number;
}

class Person implements Man {
  name: string;
  sex: number;
  constructor(name: string, sex: number) {
    this.name = name;
    this.sex = sex;
  }
  printname() {
    return this.name;
  }
  printsex() {
    return this.sex;
  }
}

const Person2 = new Person("哈哈哈", 123);

console.log(Person2.printname());

console.log(Person2.printsex());
```
