### 整体渲染流程：https://vue-js.com/learn-vue/

**模板-> 编译 -> render 函数 -> VNode -> patch -> 视图**

1. 模板编译：
   （一） 解析阶段：通过把原生 HTML 的内容找出来，再把非原生 HTML 找出来，经过一系列的逻辑处理生成渲染函数（render函数）

   - **HTML 解析器**是主线，先用 HTML 解析器进行解析整个模板，在解析过程中如果碰到文本内容，那就调用**文本解析器**来解析文本
   - HTML 解析器，文本解析器和**过滤器解析器**
   - 一边解析不同的内容一边调用对应的钩子函数生成对应的 **AST 节点**，最终完成将整个模板字符串转化成 AST。调用 **createASTElement** 函数来创建元素类型的 AST 节点。

   （二）优化阶段：
   目的：提高虚拟 DOM 中 patch 过程的性能

   1. 在 AST 中找出所有静态节点并打上标记；
      type 对应的 AST 节点类型
      1 元素节点
      2 包含变量的动态文本节点
      3 不包含变量的纯文本节点

   （三）生成阶段：

   递归 AST 生成 render 函数，调用 render 函数可生成 VNode

2. 虚拟 DOM（VNode）
   - 概念：虚拟 DOM，就是用一个 JS 对象来描述一个 DOM 节点
   - 解决的问题：**Vue 是数据驱动视图**的，数据发生变化视图就要随之更新，在更新视图的时候难免要操作 DOM,而**操作真实 DOM 又是非常耗费性能**的，这是因为浏览器的标准就把 DOM 设计的非常复杂。
   - 优点：通过 **DOM-Diff 算法**对比数据变化前后的状态，可以尽可能少的操作 DOM。（用 JS 的计算性能来换取操作 DOM 所消耗的性能）
   - 类型：
     注释节点
     文本节点
     元素节点
     组件节点
     函数式组件节点
     克隆节点
   - DOM-Diff 算法（patch 过程）：以新的 VNode 为基准，更新旧的 oldVNode 使之成为跟新的 VNode 一样。创建节点，删除节点，更新节点。

### Question：

- 生命周期： [https://vue-js.com/learn-vue/lifecycle/#\_1-%E5%89%8D%E8%A8%80](https://vue-js.com/learn-vue/lifecycle/#_1-前言)

- computed 和 watch： https://www.cnblogs.com/wuqilang/p/11241604.html

- Vue 最大的特点之一就是数据驱动视图,变化侦测。

- Vue 的双向数据绑定原理：https://juejin.cn/post/6850037277675454478#heading-11
  vue.js 是采用数据劫持结合发布者-订阅者模式的方式，通过 Object.defineProperty()来劫持各个属性的 setter，getter，在数据变动时发布消息给订阅者，触发相应的监听回调。
  - Observer 类会通过递归的方式把一个对象的所有属性都转化成可观测对象；
  - 在 getter 中收集依赖，在 setter 中通知依赖更新；
  - 依赖管理器 Dep 类；
  ```get(){
      dep.depend()    // 在getter中收集依赖
      return val;
    },
    set(newVal){
      if(val === newVal){
          return
      }
      val = newVal;
      dep.notify()   // 在setter中通知依赖更新
    }
  ```
  - Watcher 类观察者，数据变化时，不直接去通知依赖更新，而是通知依赖对应的 Watch 实例，由 Watcher 实例去通知真正的视图。有 update 方法
  - 使用 Vue.extends 封装组件：
    Vue.extend + $mount 这对组合使一些动态渲染或者使用 js 全局调用的组件变得更加灵活
    Vue.extend() 方法返回一个组件构造器，通过组件构造器创建组件实例，该实例的参数是一个包含组件选项的对象，用来在实例上扩展属性和方法。
    链接：https://blog.csdn.net/weixin_45426836/article/details/109667490
