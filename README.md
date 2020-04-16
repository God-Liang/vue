# Vue 面试题汇总

1、Vue是什么？两大核心？优点？与其他框架的区别？

2、Vue生命周期？

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
  使用混入(mixins)分发可复用功能

20、Watch中deep:true是如何实现的？

21、Vue中如何检测数组变化？

22、为何Vue采用异步渲染？

23、$nextTick实现原理？

24、v-for为什么要用key？

25、简述diff算法原理？diff算法时间复杂度？

26、用vnode来描述一个DOM结构？

27、描述组件渲染和更新过程？

28、Vue中模板编译原理？

29、Vue常见性能优化？

30、Vue3.0中的改进？
