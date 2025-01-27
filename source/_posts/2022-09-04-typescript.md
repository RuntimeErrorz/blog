---
layout: post
title: Typescript入门
subtitle: 类型体操！
author: RuntimeEroor
categories: 前端
tags: Threejs
date: 2022-09-04
---
# 安装tsc和ts-node

```powershell
cnpm i typescript --g
cnpm i ts-node --g
```

# 看代码就够了

```typescript
//******基本类型******//
let str: string = "123"

let nan: number = NaN
let hex: number = 0xf00d
let bin: number = 0b100
let oct: number = 0o744

let bool: boolean = true
let bool2: boolean = Boolean(1)

let undef: void = undefined

let an: any = 123
an = true

let bbb: unknown = '123'
let aaa: string = '456'
//aaa = bbb  不能将类型“unknown”分配给类型“string”

//******接口的使用******//
interface A {
    name: String
}
interface A {
    age: Number
}

interface A { //相同名称的接口会合并
    readonly a: string,
    b?: string,
    [propName: string]: any, //允许添加新的任意属性
    func: () => string
}

let obj: A = {
    name: "RuntimeError",
    age: 20,
    a: "I am readonly",
    func: () => {
        return "Hello"
    }
}

//******数组类型******//
let arr_number: number[] = [1, 2]
let list: any[] = ['test', 1, [], { a: 1 }]

let arr_number_2: Array<number> = [1, 2]

let arr_in_arr: number[][] = [[1, 2], [3, 4]];

let list_any: any[] = ['test', 1, [], { a: 1 }]

interface NumberArray {
    [index: number]: number;
} //表示：只要索引的类型是数字时，那么值的类型必须是数字。
let fibonacci: NumberArray = [1, 1, 2, 3, 5];

function Arr(...args: any): IArguments {
    // console.log(arguments)
    //ts内置对象IArguments 定义
    let arr: IArguments = arguments
    return arr
}
Arr(111, 222, 333)

//******函数类型******// 
function reverse(x: number): number;
function reverse(x: string): string;
function reverse(x: number | string): number | string | void { //联合类型
    if (typeof x === 'number') {
        return Number(x.toString().split('').reverse().join(''));
    } else if (typeof x === 'string') {
        return x.split('').reverse().join('');
    }
}

interface People {
    age: number,
    height: number
}
interface Man {
    sex: string
}
const xiaoman = (man: People & Man) => { //交叉类型
    // console.log(man.age)
    // console.log(man.height)
    // console.log(man.sex)
}
xiaoman({ age: 18, height: 180, sex: 'male' });

function promise(): Promise<number> {
    return new Promise<number>((resolve, reject) => {
        resolve(1)
    })
}

promise().then(res => {
    // console.log(res)
})

//******元组类型******// 
let excel: [string, string, number, string][] = [
    ['title', 'name', 1, '123'],
    ['title', 'name', 1, '123'],
    ['title', 'name', 1, '123'],
    ['title', 'name', 1, '123'],
    ['title', 'name', 1, '123'],
]

//******枚举类型******//
enum Types {
    Red,
    Green,
    BLue
}

//******类型别名******//
type str = () => string
let s: str = () => "RuntimeError"

type str2 = string | number
let s2: str2 = 123
let s3: str2 = '123'

type value = boolean | 0 | '213'
let v: value = true

//******泛型******//
function Sub<T, U>(a: T, b: U): Array<T | U> {
    const params: Array<T | U> = [a, b]
    return params
}
console.log(Sub(1, '2'))

interface Len { //泛型约束
    length: number
}
function getLegnth<T extends Len>(arg: T) {
    return arg.length
}
getLegnth<string>('123')

function prop<T, K extends keyof T>(obj: T, key: K) {
    return obj[key]
}
let o = { a: 1, b: 2, c: 3 }
prop(o, 'a')
```
