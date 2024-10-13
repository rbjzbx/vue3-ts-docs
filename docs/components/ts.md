# 文章简介

本文是我在学习TS课程中的一些学习笔记和听课记录

###  第一个 TypeScript 程序

我们可以使用以下 TypeScript 程序来输出 “Hello World” ：

```typescript
const hello : string = "Hello World!"
console.log(hello)
```

### TypeScript 区分大小写

TypeScript 区分大写和小写字符。

每行指令都是一段语句，你可以使用分号或不使用， 分号在 TypeScript 中是可选的，建议使用。

```typescript
console.log("Runoob")
console.log("Google");
```

### TypeScript 基础类型

```
any,number,string,boolean,数组类型，元组，枚举（enum）,void,null,undefined,never
```

```
let binaryLiteral: number = 0b1010; // 二进制
let octalLiteral: number = 0o744;    // 八进制
let decLiteral: number = 6;    // 十进制
let hexLiteral: number = 0xf00d;    // 十六进制
```

一个字符系列，使用单引号（'）或双引号（"）来表示字符串类型。反引号（`）来定义多行文本和内嵌表达式。

```typescript
let name: string = "Runoob";
let years: number = 5;
let words: string = `您好，今年是 ${ name } 发布 ${ years + 1} 周年`;
let flag: boolean = true;
// 在元素类型后面加上[]
let arr: number[] = [1, 2];

// 或者使用数组泛型
let arr: Array<number> = [1, 2];
let x: [string, number];
x = ['Runoob', 1];    // 运行正常
x = [1, 'Runoob'];    // 报错
console.log(x[0]);    // 输出 Runoob
enum Color {Red, Green, Blue};
let c: Color = Color.Blue;
console.log(c);    // 输出 2
function hello(): void {
    alert("Hello Runoob");
}
```

#### Any类型

```typescript
let x: any = 1;    // 数字类型
x = 'I am who I am';    // 字符串类型
x = false;    // 布尔类型
```

### TypeScript 变量声明

变量使用前必须先声明，我们可以使用 var 来声明变量。

我们可以使用以下四种方式来声明变量：

声明变量的类型及初始值：

```typescript
var [变量名] : [类型] = 值;
var [变量名] : [类型];
var [变量名] = 值;
var [变量名];
var uname:string = "Runoob"; 
var score1:number = 50;
var score2:number = 42.50
var sum = score1 + score2 
console.log("名字: "+uname) 
console.log("第一个科目成绩: "+score1) 
console.log("第二个科目成绩: "+score2) 
console.log("总成绩: "+sum)
```

### TypeScript 对象

```typescript
var object_name = { 
    key1: "value1", // 标量
    key2: "value",  
    key3: function() {
        // 函数
    }, 
    key4:["content1", "content2"] //集合
}
var sites = { 
   site1:"Runoob", 
   site2:"Google" 
}; 
// 访问对象的值
console.log(sites.site1) 
console.log(sites.site2)
```

### var，let，const三个声明变量

let与const

现在我们有两种作用域相似的声明方式，我们自然会问到底应该使用哪个。 与大多数泛泛的问题一样，答案是：依情况而定。

使用最小特权原则，所有变量除了你计划去修改的都应该使用const。 基本原则就是如果一个变量不需要对它写入，那么其它使用这些代码的人也不能够写入它们，并且要思考为什么会需要对这些变量重新赋值。 使用 const也可以让我们更容易的推测数据的流动。

var全局声明变量

### 循环语句

循环代码样式

```typescript
for ( init; condition; increment ){
    statement(s);
}
```

例子：

```typescript
for ( init; condition; increment ){
    statement(s);
}
```

### TypeScript Map 对象

```typescript
let myMap = new Map();//初始化
let myMap = new Map([
        ["key1", "value1"],
        ["key2", "value2"]
    ]); //赋值
```

