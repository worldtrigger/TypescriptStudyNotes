# 枚举类型

> 枚举一般用于定义状态,这样方便快速查找对应的值

## 数字枚举

- 当数字枚举没有指定具体的值时候,默认从 0 开始

```javascript

enum Status{
   "删除",
   "新增",
   "更新",
}

console.log(Status.删除)  //0
console.log(Status.新增)  //1
console.log(Status.更新)  //2

```

- 当我们指定了具体的值之后，就从具体的值之后开始

```javascript

enum Status {
  "删除",
  "新增" = 300,
  "更新",
}

console.log(Status.删除);
console.log(Status.新增);
console.log(Status.更新);

//0
//300
//301
```

- 这里必须注意的就是数字枚举要是使用了计算值或者常量，那后面必须设置初始值,在不能使用默认的递增值了。

```javascript

const Status = 1;  //因为使用了常量

enum Index {
  a = Status,
  b, //error枚举成员必须要具有初始化值
  c
}

const getValue = ()=>{
  return 0 ;
}

enum Index2{
  a = getValue(),
  b = 1,
  c
}
```

## 反向映射

- `反向映射只支持数字枚举,字符串枚举不支持`

```javascript

enum Status{
  Success = 200,
  NotFound = 404,
  Error = 500
}

console.log(Status[200])  //'Success'
cosnole.log(Status[Status['Success']])  // 'Success'
```

## 字符串枚举

- 字符串枚举值要求每个字段的值都必须是字符串字面量

```javascript

enum Message{
  Error = 'Sorry,error',
  Success = 'Great,success'
}

console.log(Message.Error)  // 'Sorry,error'
```

- 在看看我们使用枚举值中其他枚举成员的例子

```javascript

enum Message{
  Error = 'error message',
  ServerError = Error,
  ClientError = Error
}

console.log(Message.ServerError) //error message
console.log(Message.ClientError)  //error message
```

## 既有数字又有字符串的枚举

- 这种情况一般最好不要用,枚举类型最好统一化

```javascript

enum Result{
  Faild = 0,
  Success = 'Success'
}

```
