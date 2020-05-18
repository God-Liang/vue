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
  * 由于Object.defineproperty属于es5特性，不支持ie8及更老版本的浏览器
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

* ViewModel存在目的在于抽离Controller中展示的业务逻辑，而不是替代Controller，其它视图操作业务等还是应该放在Controller中实现。MVVM强调的是业务逻辑组件的复用，而将Controller弱化了。

4、数据双向绑定原理？
* Vue在初始化数据时，会使用Object.defineProperty重新定义data中的所有属性，当页面使用对应属性时，首先会进行依赖收集(收集当前组件的watcher)如果属性发生变化会通知相关依赖进行更新操作(发布订阅)。

5、组件之间如何传值？
* 父子传值：props和$emit
  * props父组件向子组件传值，$emit子组件向父组件传值
* 嵌套组件传值：$attrs和$listeners
* 全局事件传值(EventBus)：$emit和$on
  * $emit发送数据，$on接受数据
* 实例属性传值：$parent和$children
* 依赖注入  
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
* 组件化的好处就是复用，单个组件定义的data中属性相同，修改其中一个其他也会改变，为了每个组件实例管理自己的数据。data是一个函数。通过每次调用函数，重新声明data
 
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
* 钩子函数：
  * activated 组件渲染后调用
  * deactivated 组件销毁后调用
* 原理：Vue.js内部将DOM节点抽象成了一个个的VNode节点，keep-alive组件的缓存也是基于VNode节点的而不是直接存储DOM结构。它将满足条件（pruneCache与pruneCache）的组件在cache对象中缓存起来，在需要重新渲染的时候再将vnode节点从cache对象中取出并渲染。
* 配置属性：
  * `include` 字符串或正则表达式。只有名称匹配的组件会被缓存
  * `exclude` 字符串或正则表达式。任何名称匹配的组件都不会被缓存
  * `max` 数字。最多可以缓存多少组件实例

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
* 如果不采用异步更新，那么每次更新数据都会对当前组件进行重新渲染， 这样就会可能进行大量的dom重流或者重绘，所以为了性能考虑，减少浏览器在Vue每次更新数据后会出现的Dom开销，Vue 会在本轮数据更新后，再去异步更新视图!

23、$nextTick实现原理？
* 在下次 DOM 更新循环结束之后执行延迟回调
``` 官网介绍：异步更新队列
Vue 在更新 DOM 时是异步执行的。只要侦听到数据变化，Vue 将开启一个队列，并缓冲在同一事件循环中发生的所有数据变更。如果同一个 watcher 被多次触发，只会被推入到队列中一次。这种在缓冲时去除重复数据对于避免不必要的计算和 DOM 操作是非常重要的。然后，在下一个的事件循环“tick”中，Vue 刷新队列并执行实际 (已去重的) 工作。Vue 在内部对异步队列尝试使用原生的 Promise.then、MutationObserver 和 setImmediate，如果执行环境不支持，则会采用 setTimeout(fn, 0) 代替。
```

24、v-for为什么要用key？
* key的作用是尽可能的复用 DOM 元素
* 新旧 children 中的节点只有顺序是不同的时候，最佳的操作应该是通过移动元素的位置来达到更新的目的。

25、简述diff算法原理？diff算法事件复杂度？
* 同级比较，递归比较子级
* 新旧虚拟DOM 一个有子级一个没有子级，删除DOM,新增DOM
* 边比较边修改真实DOM,从而达到只有修改有差异的DOM。不用使整个DOM重绘重排。减少DOM操作

传统diff算法父级会跟子级比较，很少跨级移动，Vue diff算法使用的是只同级比较


26、用vnode来描述一个DOM结构？
* 所谓虚拟DOM，是一个用于表示真实 DOM 结构和属性的 JavaScript 对象，这个对象用于对比虚拟 DOM 和当前真实 DOM 的差异化，然后进行局部渲染从而实现性能上的优化

27、Vue中模板编译原理？
* 解析器：将模板Template生成AST语法树（也就是一个对象）
* 优化器：为AST语法树的静态节点及静态根节点打标记
* 代码生成器：将AST语法树转化为render函数
* render函数转化为虚拟DOM,再将虚拟DOM通过diff算法转生成真实DOM
![模板编译原理](https://upload-images.jianshu.io/upload_images/9955987-0bc6a3a6a0306382.png?imageMogr2/auto-orient/strip|imageView2/2/w/1200/format/webp)

28、Vue常见性能优化？
* v-for 设置唯一key便于diff算法查找处理
* 路由懒加载
* 使用keep-alive通过对组件进行缓存，从而节省性能
* 图片懒加载、骨架屏
* 抽离公共组件、API接口
* 第三方模块按需导入，或使用cdn加载
* 压缩，缓存
* 搜索、滚动使用防抖、节流
* 使用pug/jade 模板渲染引擎，使用less/sass

29、Vue3.0中的改进？
* 双向数据绑定：
  * 不同点：proxy 可以直接监听对象、数组；Object.defineProperty只能劫持属性，监听对象需要遍历整个对象，无法监听数组
  * 相同点：都无法监听嵌套对象
* 掘金相关文章
  * [抄笔记：尤雨溪在Vue3.0 Beta直播里聊到了这些…](https://juejin.im/post/5e9f6b3251882573a855cd52#heading-12)
  * [Vue3 究竟好在哪里？](https://juejin.im/post/5e9ce011f265da47b8450c11)
  * [精读《Vue3.0 Function API》](https://juejin.im/post/5d1955e3e51d4556d86c7b09)

30、Vue 传参query和params的区别？
* params是通过router配置的，如：`/:id`、`/:id/:childrenId`。当存在多个参数时，在页面中`/1/10`，不知道对应的参数。
* query 是直接在路径后跟`?id=1&childrenId=10`。可以很直观的看到参数值对应的参数名

31、Vue 常用修饰符？
* .stop 阻止事件冒泡
* .prevent 阻止默认行为。相当于event.preventDefault()
* .once 只触发一次
* .self 点击自身元素触发，点击内部元素不触发
* 按键修饰符 
  * .enter
  * .tab
  * .delete (捕获“删除”和“退格”键)
  * .esc
  * .space
  * .up
  * .down
  * .left
  * .right
  * 全局自定义`Vue.config.keyCodes.f1 = 112`，使用 `v-on:keyup.f1`

32、项目如何分模块开发？
* 配置webpack多入口，通过cross-env设置环境变量。从而打包不同模块。

33、怎样理解 Vue 的单向数据流？
* 所有的 prop 都使得其父子 prop 之间形成了一个单向下行绑定：父级 prop 的更新会向下流动到子组件中，但是反过来则不行。这样会防止从子组件意外改变父级组件的状态，从而导致你的应用的数据流向难以理解。
额外的，每次父级组件发生更新时，子组件中所有的 prop 都将会刷新为最新的值。这意味着你不应该在一个子组件内部改变 prop。如果你这样做了，Vue 会在浏览器的控制台中发出警告。子组件想修改时，只能通过 $emit 派发一个自定义事件，父组件接收到后，由父组件修改。

34、refs的使用及缺点？
* 当用于普通的DOM元素时，refs指向的是当前DOM元素
* 当用于子组件时，refs指向的是组件实例
* 缺点：vue更新视图使用的是虚拟DOM，而refs是直接操作真实DOM元素的属性，所以不推荐使用。(可以通过设置变量来动态改变DOM元素的属性)

35、Vue.set、this.$set的原理？
* 响应式属性是在vue初始化时期，调用data()函数，利用Object.defineProperty()为每一个属性添加监听事件。而通过赋值的方法添加新属性，视图是不发生改变的。如：this.data.name新增name属性。
* [Vue.set源码](https://github.com/vuejs/vue/blob/dev/src/core/observer/index.js#L201)
```/ src/core/observer/index.js
export function set (target: Array<any> | Object, key: any, val: any): any {
  if (process.env.NODE_ENV !== 'production' &&
    (isUndef(target) || isPrimitive(target))
  ) {
    warn(`Cannot set reactive property on undefined, null, or primitive value: ${(target: any)}`)
  }
  if (Array.isArray(target) && isValidArrayIndex(key)) {
    target.length = Math.max(target.length, key)
    target.splice(key, 1, val)
    return val
  }
  if (key in target && !(key in Object.prototype)) {
    target[key] = val
    return val
  }
  const ob = (target: any).__ob__
  if (target._isVue || (ob && ob.vmCount)) {
    process.env.NODE_ENV !== 'production' && warn(
      'Avoid adding reactive properties to a Vue instance or its root $data ' +
      'at runtime - declare it upfront in the data option.'
    )
    return val
  }
  if (!ob) {
    target[key] = val
    return val
  }
  defineReactive(ob.value, key, val)
  ob.dep.notify()
  return val
}
```
* 源码解析：
  - 1、如果是在开发环境，且target未定义（为null、undefined）或target为基础数据类型（string、boolean、number、symbol）时，抛出告警；
  - 2、如果target为数组且key为有效的数组key时，将数组的长度设置为target.length和key中的最大的那一个，然后调用数组的splice方法（vue中重写的splice方法）添加元素；
  - 3、如果属性key存在于target对象中且key不是Object.prototype上的属性时，表明这是在修改target对象属性key的值（不管target对象是否是响应式的，只要key存在于target对象中，就执行这一步逻辑），此时就直接将value直接赋值给target[key]；
  - 4、判断target，当target为vue实例或根数据data对象时，在开发环境下抛错；
  - 5、当一个数据为响应式时，vue会给该数据添加一个__ob__属性，因此可以通过判断target对象是否存在__ob__属性来判断target是否是响应式数据，当target是非响应式数据时，我们就按照普通对象添加属性的方式来处理；当target对象是响应式数据时，我们将target的属性key也设置为响应式并手动触发通知其属性值的更新；