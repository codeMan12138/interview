### 执行期上下文(Context)：
  每个执行期上下文都有三个属性： 

- 变量对象（VO）

- **作用域链**（Scope）：

  **是由当前环境与上层环境的一系列变量对象组成，它保证了当前执行环境对符合访问权限的变量和函数的有序访问。**

​	查找变量的时候，会先从当前上下文的变量对象中查找，如果没有找到，就会从父级(词法层面上的父级)执行上下文的变量对象中查找，一直找到全局上下文的变量对象，也就是全局对象。这样由多个执行上下文的变量对象构成的链表就叫做作用域链。

​	函数的作用域在函数定义的时候就决定了（词法作用域）。因JavaScript代码的整个执行过程，分为两个阶段：

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

- this

### 闭包(Closure)：

- 本质：当前环境中存在指向父级作用域的引用。

- 闭包是一种特殊的对象，它由两部分组成：执行上下文（代号 A），以及在该执行上下文中创建的**函数** （代号 B），当 B 执行时，如果访问了 A 中变量对象的值，那么闭包就会产生，且在 Chrome 中使用这个执行上下文 A 的函数名代指闭包。

   	**在 JavaScript 中，根据词法作用域的规则，内部函数总是可以访问其外部函数中声明的变量，当通过调用一个外部函数返回一个内部函数后，即使该外部函数已经执行结束了，但是内部函数引用外部函数的变量依然保存在内存中，我们就把这些变量的集合称为闭包。比如外部函数是 foo，那么这些变量的集合就称为 foo 函数的闭包**。 

- 应用：
  
  - 柯里化：



- ### 数组

  -  splice、sort、reverse  会改变原数组

  -  拷贝数组方法：

  1. **slice**: arrayObject.slice(start,end) 返回选定元素，不改变原数组；

     ```javascript
     let arr1 = [1 , 2 , 3 , "hello" , "world"];  //原数组
     let arr2 = arr1.slice(0); // 或者不传参数
     console.log(arr2);   //打印新数组
     [1 , 2 , 3 , "hello" , "world"];  //新数组
     ```

     

  2. **concat：**arrayObject.concat(arrayX,arrayX,......,arrayX) 返回结果，不影响原数组

     ```javascript
     let arr3 = [].conat(arr1);
     console.log(arr3);   //打印新数组
     [1 , 2 , 3 , "hello" , "world"];  //新数组
     ```

     

  3. **拓展运算符：**es6对象的方法 返回对象 

     ```javascript
     const arr = [1, 2, 3]
     const arrClone = [...arr]
     ```

      ![img](https://user-gold-cdn.xitu.io/2019/8/28/16cd6d6deb3a6f8f?imageslim) 

  ### 对象

  - 拷贝对象的方法：

    ```javascript
    var player = {score: 1, name: 'Jeff'};
    
    var newPlayer = Object.assign({}, player, {score: 2});
    // player 的值没有改变, 但是 newPlayer 的值是 {score: 2, name: 'Jeff'}
    
    // 使用对象展开语法，就可以写成：
    var newPlayer1 = {...player, score: 2};
    ```

    

- for in: **`for...in`语句**以任意顺序遍历一个对象的除[Symbol](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Symbol)以外的[可枚举](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Enumerability_and_ownership_of_properties)属性。 包括原型上的。

- for of： 在[可迭代对象](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/iterable)（包括 [`Array`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Array)，[`Map`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Map)，[`Set`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Set)，[`String`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/String)，[`TypedArray`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/TypedArray)，[arguments](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions_and_function_scope/arguments) 对象等等）上创建一个迭代循环，调用自定义迭代钩子，并为每个不同属性的值执行语句 

- **`instanceof`** **运算符**用于检测构造函数的 `prototype` 属性是否出现在某个实例对象的原型链上

- in:  如果指定的属性在指定的对象或其原型链中，则**`in` 运算符**返回`true` 

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

  链接： https://github.com/mqyqingfeng/Blog/issues/22  讨论区