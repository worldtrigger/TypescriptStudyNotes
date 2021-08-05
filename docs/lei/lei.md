# TS 中的类

## 类基础

- 简易版入门

```javascript
class Point {
  x: number;
  y: number;
  constructor(x: number, y: number) {
    this.x = x;
    this.y = y;
  }
  getPositon() {
    return `${this.x} + ${this.y}`;
  }
}

const point = new Point(1, 2);

console.log(point.getPositon());
```

# 修饰符

## public

- public 公共的, 能继承，能实例，没限制

```javascript

class Point {
  public x: number;
  public y: number;
  constructor(x: number, y: number) {
    this.x = x;
    this.y = y;
  }
  public getPosition() {
    return `(${this.x}, ${this.y})`;
  }
}

```

## private

- private 私有的 不能被继承，不能被实例，全部受限制

- 只能在类 class 本身里面使用

```javascript

class Parent {
  private age: number;
  constructor(age: number) {
    this.age = age;
  }
}
const p = new Parent(18);
console.log(p); // { age: 18 }
console.log(p.age); // error 属性“age”为私有属性，只能在类“Parent”中访问
console.log(Parent.age); // error 类型“typeof ParentA”上不存在属性“age”
class Child extends Parent {
  constructor(age: number) {
    super(age);
    console.log(super.age); // 通过 "super" 关键字只能访问基类的公共方法和受保护方法
  }
}

```

## protected 保护

- protected 能被继承，但是不能被实例,部分受限制

```javascript

class Parent {
  protected age: number;
  constructor(age: number) {
    this.age = age;
  }
  protected getAge() {
    return this.age;
  }
}
const p = new Parent(18);
console.log(p.age); // error 属性“age”为私有属性，只能在类“ParentA”中访问
console.log(Parent.age); // error 类型“typeof ParentA”上不存在属性“age”
class Child extends Parent {
  constructor(age: number) {
    super(age);
    console.log(super.age); // undefined
    console.log(super.getAge());
  }
}
new Child(18)

```

## readonly 修饰符

- readonly 只读

```javascript

class UserInfo {
  readonly name: string;
  constructor(name: string) {
    this.name = name;
  }
}
const user = new UserInfo("Lison");
user.name = "haha"; // error Cannot assign to 'name' because it is a read-only property

```

## 静态属性 static

- static 可以在外部不用实例化类，直接用类使用

- 要是写法顺序必须是 private,public, static 之类的

```javascript

class Parent {
  public static age: number = 18;
  public static getAge() {
    return Parent.age;
  }
  constructor() {
    //
  }
}
const p = new Parent();
console.log(p.age); // error Property 'age' is a static member of type 'Parent'
console.log(Parent.age); // 18

```

## 可选类属性

- 一个?号表示可有可无的属性

```javascript

class Info {
  name: string;
  age?: number;
  constructor(name: string, age?: number, public sex?: string) {
    this.name = name;
    this.age = age;
  }
}
const info1 = new Info("lison");
const info2 = new Info("lison", 18);
const info3 = new Info("lison", 18, "man");
```

## 存储器(改变 private 私有属性的值)

- 利用 set get

```javascript

class Parent {
  private _name: string;
  constructor(name: string) {
    this._name = name;
  }

  set name(name: string) {
    this._name = name;
  }
  get name() {
    return this._name;
  }
}

const PersonOne = new Parent("哈哈哈");

console.log(PersonOne.name);
```

## 抽象类 abstract

- 抽象类 只能被继承，不能被实例，类里面也不能被调用

```javascript

abstract class People {
  constructor(public name: string) {}
  abstract printName(): void;
}
class Man extends People {
  constructor(name: string) {
    super(name);
    this.name = name;
  }
  printName() {
    console.log(this.name);
  }
}
const m = new Man(); // error 应有 1 个参数，但获得 0 个
const man = new Man("lison");
man.printName(); // 'lison'
const p = new People("lison"); // error 无法创建抽象类的实例

```

# 类继承接口

- 类类型接口

```javascript
interface FoodInterface {
  type: string;
}
class FoodClass implements FoodInterface {
  // error Property 'type' is missing in type 'FoodClass' but required in type 'FoodInterface'
  static type: string;
  constructor() {}
}
```

- 类继承类

```javascript

class Parent {
  constructor(public name: string) {
    this.name = name;
  }
}

class Man extends Parent {
  constructor(public name: string, public sex: string) {
    super(name);
    this.sex = sex;
  }
}

const ManPerson = new Man("今天", "男");

console.log(ManPerson.sex);

```
