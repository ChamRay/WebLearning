# 1、什么是vuex

~~~
1、状态管理是什么？
	vuex是一个专为vue.js应用程序开发的状态管理模式，是一个插件。
	它采用集中式存储管理应用的所有组件的状态（数据），并以响应的规则保证状态以一种可预测的方式发生变化。
	我们也可以认为它也是一种组件键通信的方式，并且使用与任意组件
2、理解：对vue应用中多个组件的共享状态进行集中式的管理（读/写）
3、为什么需要使用这个插件：
	多个视图依赖于同一个状态
	来自不同驶入的行为需要变更同一状态
	以前的解决方案：
		将数据以及操作数据的行为都定义在父组件
		将数据以及操作数据的行为传递个需要的各个子组件（有可能需要多级传递）
	vuex就是用来解决这个问题的
4、适用场景：
	vuex可以帮助我们管理共享状态，逼格附带了更多的该你那和框架。这需要对短期和长期效益进行权衡。
	也就是说应用简单（组件比较少）就不需要使用，应用复杂，使用就会带来很大的便捷
5、vuex的核心：把所有的共享状态数据拿出来放在vuex中进行集中式管理
		
~~~

# 2、使用

~~~js
1、安装
2、引入并声明使用vuex插件
	import Vue from 'vue'
	import Vuex from 'vuex'
	import {mapActions} from 'vuex'
	Vue.use(Vuex)
3、向外暴露一个store的实例化对象
//包含了六个核心模块
		//如果是映射方法，无论是actions还是mutations的方法都映射到methods里面
		//如果是映射属性数据，无论是state的数据还是getters当中的方法都映射到computed里面
		...mapActions(['increment','decrement'])//...运算符，是扩展运算符
//打包和拆包  要么是数组要么是对象  对于打包只有一种情况就时打包并且打包只能打包数组  数组打包，只会在函数形参当中会出现，为了传递不定形参
//对象拆包不能直接拆包，拆包对象只能狮子啊一个新的对象当中去拆老的对象
    const state = {
      count:0
    },
    //store是一个包含多个属性（不是方法）的对象，起始就是用来存储数据用的
    const mutations = {
      INCREMENT(state){//通过commit()调用
        state.count++
      },
      DECREMENT(state){
        state.count--
      }
    },
    //mutations也是一个对象，是一个包含了多个方法的对象，其实就是用这个里面的方法去直操作数据的
    //这个里面的方法不能包含if for 异步，是直接操作的（同步操作）
    const actions = {
      increment(context){
        context.commit('INCREMENT')
      },
      decrement({commit}){
        setTimeout(()={
          commit('DECREMENT')//通过dispatch()调用
        },1000);
      }
      
    },
    //actions也是一个对象，是一个包含了多个方法的对象。这个对象内部的方法是用来和vue当中用户的操作去关联的
    //通过commit()方法与mutations当中的方法进行关联，并可以包含if for 异步
    const getters = {
      
    }
    //getters也是一个对象，是一个包含了多个方法的对象，这个对象内部的每个方法对应了一个计算属性的get
    //就是通过state当中的已有数据，计算出来一个新的想要使用的属性数据
	export default new Vuex.Store({
    state,
    mutations,
    actions,
    getters
  })

4、将暴露出去的store实例化对象引入到实例化Vue的配置对象当中使用
import store from '@/store'
import Vue from 'vue'
new Vue({
  el:'#app',
  store:store  //将store对象在配置对象当中配置使用，每个组件对象当中都可以this.$store获取到我们这个对象
})
5、书写store对象当中包含的4个核心概念

~~~

# 3、vuex的原理

[手写Vuex核心原理，再也不怕面试官问我Vuex原理 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/166087818#:~:text=一、核心原理 1 Vuex本质是一个对象 2 Vuex对象有两个属性，一个是install方法，一个是Store这个类,3 install方法的作用是将store这个实例挂载到所有的组件上，注意是同一个store实例。 4 Store这个类拥有commit，dispatch这些方法，Store类里将用户传入的state包装成data，作为new Vue的参数，从而实现了state 值的响应式。)

![vuex](004-Vuex.assets/vuex.png)
