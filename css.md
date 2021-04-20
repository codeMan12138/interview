### 选择器：

#### 类型：

- 通配符选择器（*）
- id选择器: #id{ }
- 类(class)选择器: .class{ }
- 标签选择器: div { }
- 属性选择器: [attr='test'] { }
- 伪类选择器:  :nth-child() { }
- 伪元素选择器：::before{ }
- 后代选择器: div p { } （匹配div下的所有p标签）
  - 子选择器: div > p { } （匹配div下面的直接后代p标签）
- 兄弟选择器: div ~ p { } （ 匹配在第一个元素**之后的所有的同一层级的**p标签 ）
  - 相邻兄弟选择器：div + p { } （ 匹配在第一个元素**紧随之后的所有的同一层级的**第二个元素。 ）

- 选择器列表：.class a,class b{ } （ 用于选中多个元素列表，并应用同套样式 ）
- 选择器组合：.class a.class b { } (中间没有空格，区别后代选择器。表示具有 class a 且具有 class b 的元素 )

#### 权重（优先级）：

```
 !important > 内联 > ID选择器 > 类选择器 > 标签选择器 > 通用选择器 （256进制）
```

![1615620591534](../images/1615620591534.png)

 链接： https://zhuanlan.zhihu.com/p/85788761 

#### 布局：

 https://juejin.cn/post/6844904121862979597#heading-0 
