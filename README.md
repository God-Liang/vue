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
* MVC
  * 模型(Model)-视图(View)-控制器(Controller)
  * Model 负责数据访问
  * View 负责显示数据-视图
  * Controller 负责将Model的数据用View显示出来
  * 控制器(Controller)做为模型(Model)和视图(View)桥梁，当模型(Model)发生改变，通过控制器(Controller)将视图(View)同步更新

* MVVM
  * 模型(Model)-视图(View)-视图模型(ViewModel)
  * Model 负责数据访问
  * View 负责显示数据-视图
  * ViewModel 处理业务逻辑
  * MVVM没有控制器。ViewModel是View和Model层的桥梁，数据会绑定到viewModel层并自动将数据渲染到页面中，视图变化的时候会通知viewModel层更新数据。

4、数据双向绑定原理？
* Vue在初始化数据时，会使用Object.defineProperty重新定义data中的所有属性，当页面使用对应属性时，首先会进行依赖收集(收集当前组件的watcher)如果属性发生变化会通知相关依赖进行更新操作(发布订阅)。

5、组件之间如何传值？
* 父子传值：props和$emit
* 嵌套组件传值：$attrs和$listeners
* 全局事件传值：$emit和$on
* 实例属性传值：$parent和$children
* vuex传值

6、路由有哪些钩子函数？
* 全局钩子函数：
  * router.beforeEach 进入路由前
  * router.afterEach 进入路由后
  * 功能：处理登录状态，动画加载效果、动态路由渲染等
* 局部钩子函数：
  * beforeRouteEnter 进入路由前
  * beforeRouteUpdate 路由改变时 例子：对于一个带有动态参数的路径 /foo/:id，在 /foo/1 和 /foo/2 之间跳转的时候调用此钩子函数
  * beforeRouteLeave 进入路由后
* 导航解析流程
  * 导航被触发。
  * 在失活的组件里调用离开守卫。
  * 调用全局的 beforeEach 守卫。
  * 在重用的组件里调用 beforeRouteUpdate 守卫 (2.2+)。
  * 在路由配置里调用 beforeEnter。
  * 解析异步路由组件。
  * 在被激活的组件里调用 beforeRouteEnter。
  * 调用全局的 beforeResolve 守卫 (2.5+)。
  * 导航被确认。
  * 调用全局的 afterEach 钩子。
  * 触发 DOM 更新。
  * 用创建好的实例调用 beforeRouteEnter 守卫中传给 next 的回调函数。

7、路由两种模式hash、history理解？
* hash：
  * 使用 URL 的 hash 来模拟一个完整的 URL，于是当 URL 改变时，页面不会重新加载。
* history：
  * 充分利用 history.pushState API 来完成 URL 跳转而无须重新加载页面。需要后端配合，将404指向app所依赖的index.html

8、v-if与v-show的区别？
* v-if：
  * 为false时，不渲染DOM
* v-show: 
  * 为false时，通过css中`display: none`隐藏DOM

9、Vue中v-html会导致哪些问题？
* scoped 的样式不会应用在 v-html 内部
  * 解决办法：深度设置样式。 不使用less、scss：`>>>`；使用less、scss：`/deep/`
* 更新的是元素的 innerHTML 。内容按普通 HTML 插入， 不会作为 Vue 模板进行编译。v-html中的表达式、绑定事件不会被解析
  * 解决办法：带有表达式、绑定事件的html格式字符串注册成组件,渲染成DOM,再插入到父节点中

10、为什么v-for和v-if不能连用？
* v-for优先与v-if，可以通过过滤、计算属性等方法处理需要遍历的数组。从而达到不渲染不必要的DOM。

11、v-model中的实现原理及如何自定义v-model？
* v-model本质就是一个语法糖，可以看成是value + input方法的语法糖。可以通过model属性的prop和event属性来进行自定义。原生的v-model，会根据标签的不同生成不同的事件和属性。
  * text 和 textarea 元素使用 value 属性和 input 事件；
  * checkbox 和 radio 使用 checked 属性和 change 事件；
  * select 使用 value 属性和 change 事件

12、组件中的data为什么是一个函数？
* 组件化的好处就是复用，单个组件定义的data中属性相同，修改其中一个其他也会改变，为了每个组件实例管理自己的数据。data是一个函数。
 
13、如何注册组件？组件渲染和更新的过程？
* 全局注册：Vue.component
* 局部注册：components：{}
* 通过递归，将组件转化为VNode

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
* 通过插槽分发内容,内置组件。

16、keep-alive的作用与原理？
* 作用：实现组件缓存
* 原理：Vue.js内部将DOM节点抽象成了一个个的VNode节点，keep-alive组件的缓存也是基于VNode节点的而不是直接存储DOM结构。它将满足条件（pruneCache与pruneCache）的组件在cache对象中缓存起来，在需要重新渲染的时候再将vnode节点从cache对象中取出并渲染。

17、计算属性和 watch 的区别？
* 计算属性：
  * 将复杂的逻辑放入计算属性中处理数据，获取返回值。减少多次计算
* watch：
  * 监听数据，调用对应的方法

18、理解Vue中的Render渲染函数？
* JSX语法创建虚拟DOM

19、Vue中相同逻辑如何抽离？
  * 使用混入(mixins)分发可复用功能
  * 挂载到Vue原型上：Vue.prototype

20、Watch中deep:true是如何实现的？
* 通过判断是否是对象、数组，使用递归的方式为每个属性添加监听

21、Vue中如何检测数组变化？
* Vue重写了push、'pop'、'shift'、'unshift'、'splice'、'sort'、'reverse'等改变数组确无法监听的方法

22、为何Vue采用异步渲染？

23、$nextTick实现原理？

24、v-for为什么要用key？

25、简述diff算法原理？diff算法事件复杂度？
* 同级比较，递归比较子级
* 新旧虚拟DOM 一个有子级一个没有子级，删除DOM,新增DOM
* 边比较边修改真实DOM,从而达到只有修改有差异的DOM。不用使整个DOM重绘重排。减少DOM操作

传统diff算法父级会跟子级比较，很少跨级移动，Vue diff算法使用的是只同级比较


26、用vnode来描述一个DOM结构？

27、Vue中模板编译原理？

28、Vue常见性能优化？

29、Vue3.0中的改进？
