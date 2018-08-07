title: Js事件循环
date: 2018-02-04 16:04:15

tags:
  - Js
---

# JavaScript 事件循环

JavaScript 是单线程的语言，同一个时间只能做一件事，但却有着无处不在的异步。

- `同步：`同步方法调用一旦开始，调用者必须等到方法调用返回后，才能继续后续的行为。
- `异步：` 异步方法调用更像一个消息传递，一旦开始，方法调用就会立即返回，调用者就可以继续后续的操作。而，异步方法通常会在另外一个线程中，“真实”地执行着。整个过程，不会阻碍调用者的工作。
# 内存空间
## 1,堆(heap)
- 堆数据结构是一种树状结构。它的存取数据的方式，则与书架与书非常相似。好比在JSON格式的数据中，我们存储的key-value是可以无序的，因为顺序的不同并不影响我们的使用，我们只需要关心书的名字。
## 2,栈(stack)
- 先进后出，后进先出
![](http://p4.cdn.img9.top/ipfs/QmWhxEh4X4vcZkxYgzHT93aogtuKpwKrX7cL4zLNfVDK41?4.png)
## 3,队列(queue)
- 队列是一种先进先出（FIFO）的数据结构
![](http://upload-images.jianshu.io/upload_images/599584-7ca4b641daf48c57.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

# 执行上下文
- 控制器转到js可执行代码的时候，就会进入到一个执行上下文。
### 全局代码（Global code）
- 这种类型的代码是在"程序"级处理的：例如加载外部的js文件或者本地<script></script>标签内的代码。全局代码不包括任何function体内的代码。 这个是默认的代码运行环境，一旦代码被载入，引擎最先进入的就是这个环境。
### 函数代码（Function code）
- 任何一个函数体内的代码，但不包括内部函数的代码。

# 执行环境栈

- 列
```

function foo(i) {
  if (i < 0) return;
  console.log('begin:' + i);
  foo(i - 1);
  console.log('end:' + i);
}
foo(1);

```

# 函数调用栈与任务队列
- 每个函数调用都会创造新的上下文与局部作用域，这些执行上下文堆叠就形成了所谓的执行上下文栈。
![](http://upload-images.jianshu.io/upload_images/599584-58d31e5b80737ca0.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

# 浏览器环境下的Event Loop
- 当主线程运行的时候,JS会产生堆和栈(执行栈)
- 主线程中调用的webaip所产生的异步操作(dom事件、ajax回调、定时器等)只要产生结果，就把这个回调塞进“任务队列”中等待执行。
- 当主线程中的同步任务执行完毕，系统就会依次读取“任务队列”中的任务，将任务放进执行栈中执行。
- 执行任务时可能还会产生新的异步操作，会产生新的循环，整个过程是循环不断的。
![](https://user-gold-cdn.xitu.io/2018/3/18/162385d14ae83726?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)

- 事件循环其实就是入栈出栈的循环。问问