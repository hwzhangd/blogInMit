---
title: promise
date: 2016-02-01 10:18:21
tags: js, promise
---

# js的异步
重点：
1、js是单线程
2、js是单线程
3、js是单线程

重要的事情说三遍！单线程使js不能像java、c#的代码一样多线程地执行（优劣暂不分析）。

大多数的任务需要去执行，但是如果需要长时间等待或者计算的任务，后面的任务不得不等它结束再执行，就用户体验来说是页面很卡，对于开发者来说也是资源的浪费，这样的设计显然是不合理的。异步就是将需等待的事件进入“任务队列”，程序继续执行，待“任务队列”的事件通知可以执行了，程序将执行这个任务。详情可看：[JavaScript 运行机制详解：再谈Event Loop] (http://www.ruanyifeng.com/blog/2014/10/event-loop.html)

在前端用异步基础只有三个地方：

* setTimeout、setInterval：两种方法的参数均是回调函数、等待时间。区别是setTimeout只执行一次，setInterval可以执行多次。它们都是等待时间过后再执行参数一的回调函数
* XHR请求： 原生的XHR在收到接口返回内容后执行load方法，jquery封装的ajax是放在success里，或者通过直接通过该$ajax.then来执行后续操作（ajax返回的就是一个带promise的对象）；ES6可以不用xhr请求，直接通过fetch可调用接口，fetch本身就是一个promise。
* 观察者模式（设计思维，暂不介绍）

然后复杂的场景来了：

1、连接性请求，即请求一个接口成功后再去请求另一个，如果这种请求特别多就会出来很多层，可读性与可维护性很差，而且一旦某一项报错就整个挂掉了。所以这时候promise就来了，使用then方法即可。

2、需要在获取N个接口或文件后再去执行一些操作，promise提供all方法可满中这类需求

再说nodejs，因为nodejs本身就是异步的，所以在nodejs出现层层包裹很正常，即使是使用异步封装的库也大多是链式的，通过then进行传递。


还有另一种类似同步的使用库：可参考[深入掌握 ECMAScript 6 异步编程](http://www.ruanyifeng.com/blog/2015/04/generator.html)

* co 基于ES6的generator的异步解决方案，代价是 yield 后面的函数必须返回一个 Thunk 或者一个 Promise. [co 函数库的含义和用法](http://www.ruanyifeng.com/blog/2015/05/co.html)
* async  [async 函数的含义和用法](http://www.ruanyifeng.com/blog/2015/05/async.html)




