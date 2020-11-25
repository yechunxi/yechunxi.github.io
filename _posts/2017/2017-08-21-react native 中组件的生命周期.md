---
layout: post
title:  "react native组件生命周期"
date:   2017-08-21 00:07
categories: react-native
tags: js react
excerpt: 
---

 初学react native,
，看到过很多关于生命周期的文章，然而很多的时候，还是觉得自己总结一遍吧，这样的理解才会更加深刻。




> **组件中有两个很重要两个概念**：

props 属性：

（1）组件本身不可修改props，只能是其他组件调用时修改
（2）父组件和子组件交互的桥梁
 
 state 状态：
 
 （1）主要是用来存储自身需要的数据
 （2）组件定义了setState方法，调用时会更新组件的状态，触发render方法重新渲染
 

---
> **其中组件的生命周期主要分为四个阶段：**
1. 创建阶段
2. 实例化阶段
3. 运行阶段
4. 销毁阶段

经典的生命周期图如下：

![image](https://yechunxi.github.io/images/3-3-component-lifecycle.jpg)

**创建阶段**：

初始化组件属性和默认属性，defaultProps/getDefaultProps()

组件的初始化值在这个阶段赋值，组件内用this.props获取初始化的值

---
**实例化阶段**：

（1）constructor/getInitialState(),对控件的一些状态进行初始化，比如对控件上显示的文字，利用this.state来获取值；

（2） componentWillMount,准备加载组件，在组件初始化之后，第一次调用render之前，比如对一些业务初始化操作，设置组件状态，此时调用setState，则render渲染的是更新后的状态；

（3） render, 页面的渲染，返回jsx或其他组件来构建DOM，只能返回一个顶级元素

（4） componentDidUpdate，组件加载成功渲染出来后执行的函数，一般会将网络请求等加载数据的操作，这样保证不会出现UI的错误

---
**运行阶段**:

改操作是发生在用户操作或者父组件更新时，会进行相应的页面调整

（1） componentWillRecieveProps，组件收到新的props时触发，通过setState方法设置state的值

（2） shouldComponentUpdate(nextProps, nextState),决定是否需要更新组件，在默认情况下，一直都是true，因此，在大型项目中，可以重载改该函数，检测状态值的变化，触发render，提升性能

（3） componentWillUpdate(nextProps, nextState)，准备更新组件，当shouldComponentUpdate返回true之后触发，可以做一些在更新界面之前要做的事情，但是不定调用setState来更新状态，该函数调用之后，就会把 nextProps 和 nextState 分别设置到 this.props 和 this.state 中

（4） render，更新组件，生成需要更新的虚拟dom节点

（5） componentDidUpdate，虚拟DOM同步到DOM之后，会调用，因此，该方法可以进行相关DOM操作

**注意：componentWillUpdate与componentDidUpdate不要进行setState，否则会一直循环**

---
**销毁阶段**：

componentWillUnmount()，组件在界面上移除的时候调用，可以做一些组件清理的工作，比如清除定时器，取消时间绑定，取消网络请求等。

更新组件（重新渲染界面）的方式有以下四种：

（1）首次渲染Initial Render，即首次加载组件
调用this.setState；

（2）状态发生改变（并不是一次setState会触发一次render，React可能会合并操作，再一次性进行render）


（3）父组件发生更新（一般就是props发生改变，但是就算props没有改变或者父子组件之间没有数据交换也会触发render）

（4）调用this.forceUpdate，强制更新


---
总结：

1. 能够调用setState方法的函数：
componentWillMount，componentDidMount，componentWillReceiveProps

2. 只调用一次的函数：
defaultProps / getDefaultProps(全局只调用一次)，
constructor / getInitialState	，
componentWillMount，componentDidMount，componentWillUnmount

3. render函数调用至少一次

4. 调用0次或者多次，componentWillReceiveProps，shouldComponentUpdate，componentWillUpdate，componentDidUpdate










