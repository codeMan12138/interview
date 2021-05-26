### 执行期上下文(Context)：

每个执行期上下文都有三个属性：

- 变量对象（VO）

- **作用域链**（Scope）：

  **是由当前环境与上层环境的一系列变量对象组成，它保证了当前执行环境对符合访问权限的变量和函数的有序访问。**

 查找变量的时候，会先从当前上下文的变量对象中查找，如果没有找到，就会从父级(词法层面上的父级)执行上下文的变量对象中查找，一直找到全局上下文的变量对象，也就是全局对象。这样由多个执行上下文的变量对象构成的链表就叫做作用域链。

 函数的作用域在函数定义的时候就决定了（词法作用域）。因 JavaScript 代码的整个执行过程，分为两个阶段：

- 代码编译阶段与代码执行阶段。编译阶段由编译器完成，将代码翻译成可执行代码，这个阶段作用域规则会确定。
- 执行阶段由引擎完成，主要任务是执行可执行代码，执行上下文在这个阶段创建。

```
checkscopeContext = {
    AO: {
        arguments: {
            length: 0
        },
        scope2: 'local scope'
    },
    Scope: [AO, globalContext.VO],
    this:undefined
}
```

https://github.com/mqyqingfeng/Blog/issues/8

https://segmentfault.com/a/1190000012646221

- **this**： **在对象内部的方法中使用对象内部的属性**

  - 通过函数的 call 方法设置

  - 通过对象调用方法设置

  - 通过构造函数中设置

  - 嵌套函数中的 this 不会从外层函数中继承：

    ```javascript
    var myObj = {
      name: " 极客时间 ",
      showThis: function () {
        console.log(this);
        function bar() {
          console.log(this);
        }
        bar();
      },
    };
    myObj.showThis();
    // 函数 bar 中的 this 指向的是全局 window 对象，而函数 showThis 中的 this 指向的是 myObj 对象
    ```

### 闭包(Closure)：

- 本质：当前环境中存在指向父级作用域的引用。

- 闭包是一种特殊的对象，它由两部分组成：执行上下文（代号 A），以及在该执行上下文中创建的**函数** （代号 B），当 B 执行时，如果访问了 A 中变量对象的值，那么闭包就会产生，且在 Chrome 中使用这个执行上下文 A 的函数名代指闭包。

  **在 JavaScript 中，根据词法作用域的规则，内部函数总是可以访问其外部函数中声明的变量，当通过调用一个外部函数返回一个内部函数后，即使该外部函数已经执行结束了，但是内部函数引用外部函数的变量依然保存在内存中，我们就把这些变量的集合称为闭包。比如外部函数是 foo，那么这些变量的集合就称为 foo 函数的闭包**。

- 应用：

  - 柯里化：

### 数组相关：

- splice、sort、reverse 会改变原数组

- 拷贝数组方法：

1. **slice**: arrayObject.slice(start,end) 返回选定元素，不改变原数组；

   ```javascript
   let arr1 = [1, 2, 3, "hello", "world"]; //原数组
   let arr2 = arr1.slice(0); // 或者不传参数
   console.log(arr2); //打印新数组
   [1, 2, 3, "hello", "world"]; //新数组
   ```

2. **concat：**arrayObject.concat(arrayX,arrayX,......,arrayX) 返回结果，不影响原数组

   ```javascript
   let arr3 = [].conat(arr1);
   console.log(arr3); //打印新数组
   [1, 2, 3, "hello", "world"]; //新数组
   ```

3. **拓展运算符：**es6 对象的方法 返回对象

   ```javascript
   const arr = [1, 2, 3];
   const arrClone = [...arr];
   ```

   ![img](https://user-gold-cdn.xitu.io/2019/8/28/16cd6d6deb3a6f8f?imageslim)

### 对象相关：

- 拷贝对象的方法：

  ```javascript
  var player = { score: 1, name: "Jeff" };

  var newPlayer = Object.assign({}, player, { score: 2 });
  // player 的值没有改变, 但是 newPlayer 的值是 {score: 2, name: 'Jeff'}

  // 使用对象展开语法，就可以写成：
  var newPlayer1 = { ...player, score: 2 };
  ```
  
- for in: **`for...in`语句**以任意顺序遍历一个对象的除[Symbol](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Symbol)以外的[可枚举](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Enumerability_and_ownership_of_properties)属性。 包括原型上的。

- for of： 在[可迭代对象](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/iterable)（包括 [`Array`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Array)，[`Map`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Map)，[`Set`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Set)，[`String`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/String)，[`TypedArray`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/TypedArray)，[arguments](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions_and_function_scope/arguments) 对象等等）上创建一个迭代循环，调用自定义迭代钩子，并为每个不同属性的值执行语句

- **`instanceof`** **运算符**用于检测构造函数的 `prototype` 属性是否出现在某个实例对象的原型链上

- in: 如果指定的属性在指定的对象或其原型链中，则**`in` 运算符**返回`true`

- 防抖函数在做动画时的应用：

  ```
  function debounce(func) {
      var t;
      return function () {
          cancelAnimationFrame(t)
          t = requestAnimationFrame(func);
      }
  }
  ```

  链接： https://github.com/mqyqingfeng/Blog/issues/22 讨论区

### 判断类型：

- 基本类型：
  - typeof：number、string、boolean、object(null)、undefined、function
  - Object.prototype.toString.call( ) 结果: [object Null]...
- 判断实例：instanceof、constructor

### 事件循环：

- 为什么会有事件循环？

  因为JavaScript是单线程，之所以是单线程的原因是因为JavaScript是为了浏览器而生的脚本语言，浏览器主要的职责是和用户交互，这个特性决定了JavaScript是单线程，不然多线程在操作dom的时候会有很复杂的状态同步问题。同时也正因为要防止渲染的同时JavaScript操作DOM造成冲突，JavaScript线程和渲染线程是互斥的。需要务都同步执行，那么一个任务执行时间过久的时候，其他任务就会被阻塞，会给用户造成不好的体验如页面卡死等。

- 任务队列：

  ​	渲染进程内部会维护任务队列，也就是宏任务队列，然后主线程采用一个for循环不断的从这个任务队列里取出任务来执行。

  任务里包括渲染事件，交互事件，JavaScript脚本执行请求和网络请求完成，文件读写完成等事件。

  但是这样还不够，可以看到JavaScript执行也只是任务中的一种，所以我们在写JavaScript的时候没办法精确的掌控任务的执行时机，所以浏览器提供了微任务队列。

- 微任务：

   	微任务是就是一个异步执行的函数，它属于JavaScript的执行上下文，每当执行一个JavaScript脚本的时候，就会在全局执行上下文中创建一个微任务队列，在执行这段脚本过程中产生的微任务全部会被添加到这个队列当中，当这段脚本执行完毕，即将退出全局执行上下文并且清空调用栈的时候，会检查微任务队列，然后按顺序执行其中的微任务。 