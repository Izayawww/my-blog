---
title: vue
tag: 知识
description: 一些vue的知识
---
### MVVM
    全称是Model-View-ViewModel；
    1、M就是Model模型层，存的⼀个数据对象。 
    2、V就是View视图层，所有的html节点在这⼀层。 
    3、VM就是ViewModel，它通过data属性连接Model模型层，通过el属性连接View视图层。 

### vue生命周期
    总共分为8个阶段创建前/后，载入前/后，更新前/后，销毁前/后。
    创建前/后： 在beforeCreated阶段，vue实例的挂载元素el还没有。
    
    
    载入前/后：在beforeMount阶段，vue实例的$el和data都初始化了，但还是挂载之前为虚拟的dom节点，data.message还未替换。
    在mounted阶段，vue实例挂载完成，data.message成功渲染。
    
    
    更新前/后：当data变化时，会触发beforeUpdate和updated方法。
    
    
    销毁前/后：在执行destroy方法后，对data的改变不会再触发周期函数，说明此时vue实例已经解除了事件监听以及和dom的绑定，
    但是dom结构依然存在。
    
    ajax请求最好放在created里面，因为此时已经可以访问this了，请求到数据就可以直接放在data里面。
    
    关于dom的操作要放在mounted里面，在mounted前面访问dom会是undefined。
    
    每次进入/离开组件都要做一些事情，用什么钩子：
    
    不缓存：
    进入的时候可以用created和mounted钩子，离开的时候用beforeDestory和destroyed钩子,
    beforeDestory可以访问this，destroyed不可以访问this。
    
    缓存了组件：
    缓存了组件之后，再次进入组件不会触发beforeCreate、created 、beforeMount、 mounted，
    如果你想每次进入组件都做一些事情的话，你可以放在activated进入缓存组件的钩子中。
    同理：离开缓存组件的时候，beforeDestroy和destroyed并不会触发，可以使用deactivated离开缓存组件的钩子来代替。
    
### vue的双向数据绑定
    vue.js 是采用数据劫持结合发布者-订阅者模式的方式，
    通过Object.defineProperty()来劫持各个属性的setter，getter，
    在数据变动时发布消息给订阅者，触发相应的监听回调。
    具体步骤：
    
    第一步：需要observe的数据对象进行递归遍历，包括子属性对象的属性，都加上 setter和getter。
    这样的话，给这个对象的某个值赋值，就会触发setter，那么就能监听到了数据变化
    
    
    第二步：compile解析模板指令，将模板中的变量替换成数据，然后初始化渲染页面视图，
    并将每个指令对应的节点绑定更新函数，添加监听数据的订阅者，一旦数据有变动，收到通知，更新视图
    
    
    第三步：Watcher订阅者是Observer和Compile之间通信的桥梁，主要做的事情是:
    
    
    1、在自身实例化时往属性订阅器(dep)里面添加自己
    
    
    2、自身必须有一个update()方法
    
    
    3、待属性变动dep.notice()通知时，能调用自身的update()方法，并触发Compile中绑定的回调，则功成身退。
    
    
    第四步：MVVM作为数据绑定的入口，整合Observer、Compile和Watcher三者，
    通过Observer来监听自己的model数据变化，通过Compile来解析编译模板指令，
    最终利用Watcher搭起Observer和Compile之间的通信桥梁，
    达到数据变化 -> 视图更新；视图交互变化(input) -> 数据model变更的双向绑定效果。
    
### keep-alive
    是Vue的内置组件，能在组件切换过程中将状态保留在内存中，防止重复渲染DOM。
    prop:
        include: 字符串或正则表达式。只有匹配的组件会被缓存。
        exclude: 字符串或正则表达式。任何匹配的组件都不会被缓存。
    结合router，缓存部分页面
        使用$route.meta的keepAlive属性
        需要在router中设置router的元信息meta 
            meta: {
            keepAlive: false // 不需要缓存
                  }
### v-model
    实现双向绑定，指令
    <input v-model="searchText"> 
    等价于
    <input
      v-bind:value="searchText"
      v-on:input="searchText = $event.target.value">

###vuex
    vue框架中状态管理
    State:单一状态树
    Getter:getters 可以对State进行计算操作，它就是Store的计算属性
    Mutation:类似于事件,mutation 必须是同步函数
    Action:Action 提交的是 mutation，而不是直接变更状态。
                Action 可以包含任意异步操作。
    Module:每个模块拥有自己的 state、mutation、action、getter、甚至是嵌套子模块
    
### Vue.js中ajax请求代码应该写在组件的methods中还是vuex的actions中？
    一、如果请求来的数据是不是要被其他组件公用，仅仅在请求的组件内使用，
    就不需要放入vuex 的state里。
    二、如果被其他地方复用，这个很大几率上是需要的，
    如果需要，请将请求放入action里，方便复用，并包装成promise返回，
    在调用处用async await处理返回的数据。如果不要复用这个请求，那么直接写在vue文件里很方便。
    
### 每个周期具体适合哪些场景？
    生命周期钩子的一些使用方法： 
    beforecreate : 可以在这加个loading事件，在加载实例时触发 
    created : 初始化完成时的事件写在这里，如在这结束loading事件，异步请求也适宜在这里调用 
    mounted : 挂载元素，获取到DOM节点 
    updated : 如果对数据统一处理，在这里写上相应函数 
    beforeDestroy : 可以做一个确认停止事件的确认框 
    nextTick : 更新数据后立即操作dom
### axios的特点有哪些？
    一、Axios 是一个基于 promise 的 HTTP 库，支持promise所有的API
    二、它可以拦截请求和响应
    三、它可以转换请求数据和响应数据，并对响应回来的内容自动转换成 JSON类型的数据
    watch computed
    computed是基于它的依赖进⾏缓存的。computed只有在它的相关依赖发⽣变化才会重新 计算求值
    watch 当需要在数据变化时执⾏异步