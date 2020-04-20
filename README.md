# Vue 面试题汇总

1、Vue是什么？两大核心？优、缺点？
* 构建单页面应用程序的渐进式框架
* 特点(两大核心)
  * 组件化：单个应用中的各个模块由一个个单独的组件拼接而成。组件之间独立性强。
  * 数据驱动：当数据发生改变，视图自动更新。
* 优点：
  * 主张性弱，简单易用
  * 使用虚拟DOM,减少DOM操作
  * 渐进式框架，轻量
* 缺点：
  * vue1.0和vue2.0区别较大
  * 由于Object.defineproperty属于es5特性，不支持ie8及更多版本的浏览器
  * 实现方法过多，不便与维护

2、Vue生命周期？
* 从开始创建、初始化数据、编译模板、挂在DOM、渲染-更新-渲染、卸载等一系列从创建到销毁的过程
  * beforeCreate：Vue实例初始化
  * created：初始化数据
  * beforeMount：创建虚拟DOM，编译模板
  * mounted：渲染真实DOM
  * beforeUpdate：更新前
  * updated：更新数据，虚拟DOM重新渲染
  * beforeDestroy：销毁前
  * destroyed：销毁Vue实例

3、MVVM实现原理？与MVC的区别？

4、数据双向绑定原理？

5、组件之间如何传值？

6、路由有哪些钩子函数？

7、路由两种模式hash、history理解？

8、v-if与v-show的区别？

9、Vue中v-html会导致哪些问题？

10、为什么v-for和v-if不能连用？

11、v-model中的实现原理及如何自定义v-model？

12、组件中的data为什么是一个函数？
 
13、如何注册组件？

14、自定义指令的用法？
  * 全局注册：Vue.directive()
  * 局部注册：directives: {}
  * 钩子函数：
    * bind：DOM加载之前调用
    * inserted：DOM加载之后调用
    * update：更新之前调用
    * componentUpdated：更新之后调用
    * unbind： 解除绑定时调用    如v-if

15、插槽的作用？

16、keep-alive的作用与原理？

17、计算属性和 watch 的区别？

18、理解Vue中的Render渲染函数？

19、Vue中相同逻辑如何抽离？
  * 使用混入(mixins)分发可复用功能
  * 挂载到Vue原型上：Vue.prototype

20、Watch中deep:true是如何实现的？

21、Vue中如何检测数组变化？

22、为何Vue采用异步渲染？

23、$nextTick实现原理？

24、v-for为什么要用key？

25、简述diff算法原理？diff算法事件复杂度？
* 同级比较，递归比较子级
* 新旧虚拟DOM 一个有子级一个没有子级，删除DOM,新增DOM
* 边比较边修改真实DOM,从而达到只有修改有差异的DOM。不用使整个DOM重绘重排。减少DOM操作

传统diff算法父级会跟子级比较，很少跨级移动，Vue diff算法使用的是只同级比较


26、用vnode来描述一个DOM结构？

27、描述组件渲染和更新过程？

28、Vue中模板编译原理？

29、Vue常见性能优化？

30、Vue3.0中的改进？
