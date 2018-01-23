---
title: async/await简介
date: 2016-07-17 17:00:35
thumbnail: /images/22.jpg
categories:
  -  技术
tags:
  - 前端开发
  - ES Next
---

# WTF!!!

ECMAScript 7 发布，竟然没有`async/await`［懵逼脸］。相较于`generator`，我更偏爱于`async/await`，我为此还将所有的`promise.then`和`generator`全改为`async/await`［再次懵逼］。

<!--more-->

# 什么是`async/await`?

`async/await`被定义在这个[仓库中](https://github.com/tc39/ecmascript-asyncawait)，相较于`generator`，我们利用`async/await`可以以看起来更为同步的方式写出异步代码，且可读性更高。比如：
```javascript
// 一个异步操作
const asyncOp = () => new Promise((resolve, reject) => {
  console.log(2)
  setTimeout(resolve(true), 3000)
})

// async/await 方式
const asyncFun = async () => {
  console.log(1)
  const result = await asyncOp()
  console.log(result)
  console.log(3)
}

asyncFun()

// output
// 1
// 2
// true
// 3
```

从上面可以看出`async/await`的存在使得你可以等待await一个Promise的完成。这将以非阻塞的方式暂停这个函数的进行，并且等待Promise的resolve函数的执行并返回结果。如果Promise抛出异常，你可以通过catch去处理这个异常。

而如果我们用`generator`的方式去写这部分异步操作我们会怎么写呢，请看代码：
```javascript
// generator 方式
function* asyncFun () {
  console.log(1)
  yield asyncOp()
  console.log(3)
}

const demo = asyncFun()
const ret = demo.next().value
console.log(ret)
demo.next()
// output
// 1
// 2
// Promise {[[PromiseStatus]]: "resolved", [[PromiseValue]]: true}
// 3
```
我承认，我的写法需要改善，但是我真的不喜欢这种写法[这不是偏见！！！]，而且当`yield`之后返回的就是一个`Promise`，你还需要其他做一些其他操作再得到这个确切的返回结果。

总之就是喜欢`async/await`，没有理由！
