# 快速开始

Typescript 是微软 2012 年推出的一种编程语言,属于 Javascriipt 的超集,可以编译为 Javascript 执行。它最大特点是强大的类型系统和对 ES6 的支持,Typescript 可以通过编译转换为纯正的 Javascript 代码,且编译出来的 Javascript 可以运行在任何浏览器上。Typescript 的编译工具也可以运行在任何服务器和任何系统上

- 重点: 数据类型 类 接口 泛型

# 安装 TypeScript

两种主要的方式来获取 Typescript

- 通过 npm(Node.js 包管理器)

- 安装 vscode 插件

vscode 最新的默认包含了 Typescript.

针对 npm 用户可以安装包依赖

```bash
cnpm i typescript -g
```

然后在安装 ts-node 来运行

```bash
cnpm i ts-node -D
```

如果运行 ts-node xxx.ts 报错

```bash
Error: Cannot find module '@types/node/package.json'
```

则还需要安装一个包依赖

```bash
cnpm install -D  @types/node
```

# 入门级 Demo

- 在编辑器,将下面的代码输入到 greeter.ts 里面

```javascript
function greeter(person: string) {
  return 'Hello' + person;
}
let user = 'Jan User';

console.log(greeter(user));
```
