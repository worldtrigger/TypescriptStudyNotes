# 命名空间

> 在代码量较大的情况下,为了避免各种变量命名相冲突,可将相似功能的函数,类,接口等放置到命名空间内,如果想在命名空间外访问,则用 export 到处。用关键字 namespace 来声明命名空间

## 分离到多文件

```bash

当应用变得很大时候,我们需要将代码分离到不同的文件,以便维护.这就是多文件的命名空间

```

## 作用

```bash

简单来说就是逻辑分组和避免命名冲突

```

## 使用命名空间必须有 export 导出

```javascript
 //Validation.ts
  namespace Validation {
    export interface StringValidator {
      isAcceptable(s:string): boolean;
    }
  }

  //LettersOnlyValidator.ts
  /// <reference path="./Validation" />
  namespace Validation {
    const lettersRegexp = /^[A-Za-z]+$/;
    export class LettersOnlyValidator implements StringValidator {
      isAcceptable( s: string ) : boolean {
        return lettersRegexp.test(s);
      }
    }
  }

  //ZipCodeValidator.ts
  /// <reference path="./Validation.ts" />
  namespace Validation {
    const numberRegexp = /^[0-9]+$/;
    export class ZipCodeValidatior implements StringValidator {
      isAcceptable( s: string ) : boolean {
        return s.length === 5 && numberRegexp.test(s)
      }
    }
  }

  //Test.ts
  ///<reference path="Validator.ts" />
  ///<reference path="LettersOnlyValidator.ts" />
  ///<reference path="ZipCodeValidator.ts" />
  let strings = ["Hello", "98502", "101"];
  let validators: { [s: string ] : Validation.StringValidator } = {};
  validators["ZIP code"] = new Validation.ZipCodeValidator();
  validators["Letters only"] = new Validation.LettersOnlyValidator();

  for (let s of strings ) {
    for( let name in validators ) {
      console.log(""" + s + "" " + (validators[name]).isAcceptable(s) ? "matches" : " does not match " + name)
    }
  }

  //Summery:
  //在ts中引用带命名空间的文件，用三斜线指令引入要引用的文件。但貌似在实际开发过程中，我们还是用模块用得比较多。
```

## 别名(一般用的很少)

```javascript
namespace Shapes {
    export namespace Polygons {
      export class Triangle {}
      export class Square {}
    }
  }

  import polygons = Shapes.Polygons;
  let sq = new polygons.Square();
```
