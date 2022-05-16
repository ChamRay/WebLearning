# 1、vue-cli

~~~vue
在public中编写index.html
在components中编写单文件组件main.js文件中
~~~

- MyButton.vue文件自定义组件

~~~vue
<template>
	<div>
    <h2>我爱你</h2>
    <button @click='count++'>爱了{{count}}次</button>
  </div>

</template>

<script>
export default{
  name:'',
  data(){
    return{
      count:0
    }
  }
}

</script>
~~~

- App.vue文件中导入并使用自定义组件

~~~vue
<template>
	<div>
    <MyButton></MyButton>
  </div>
</template>

<script>
import MyButton from '@/components/MyButton'
export default{
  name:'',
  components:{
    MyButton
  }
}
</script>
~~~

- main.js入口文件中引入组件

~~~js
import Vue from 'vue'//在package.json的main中定义的默认版本
import App from '@/App'

//下列入口方法选择一种就可
new Vue({
  //使用这种入口方法导入vue得确定到具体的vue，默认导入的vue.runtime.common.js(不带解析器)
  //import Vue from 'vue/dist/vue.esm.js',这个是带解析器的vue.js
  el:'#app',
  components:{
    App,
  },
  template:'<App/>'
})

//使用的是render执行loader中vue-template-compiler解析模板
new Vue({
  el:'#app',
  tender:h=>h(App)//这个函数和上面我们自己写的，功能差不多
  							/*
  							1、定义并注册了App
  							2、使用了App组件
  							3、比上面的写法多干了一件事，就是寻找解析器的loader
  							*/
})

//以后我们使用的是下面这种：下面这种打包出来的项目体积小
~~~

# 2、组件中数据的约定

~~~
1、初始化数据动态显示
	初始化数据分析：
		数据类型：一边干我们的颚数据最终都是放在一个数组内部，数组内部发那个对象
		数据名称：comments[{},{},{}]
		定义在哪个组件：（看哪个组件还是哪些个组件使用到）
			数据用到不是说展示就代表用，而是说数据的增删改查都叫用到数据
			如果这个数据只是某一个组件中使用，那么数据就在这一个组件当中定义
			如果这个数据在某些个组件当中使用，那么就找这些个共同的祖先组件去定义
	组件标签名和属性名大小写问题：
		基本规则：要么原样去写，要么转小写中间用-连接；AddComment  add-comment
2、交互
	对于数据的操作：
		数据在哪里，操作数据的方法就要定义在哪里，而不是随便的在某一个组件当中去操作数据，想要操作数据的组件，可以用过调用操作数据的方法，间接去操作数据
	添加和删除:
		子组件添加事件和事件回调，事件回调当中去调用外部操作数据的方法，数据所在的组件去添加操作数据的方法

父组件在标签中通过属性:prop='data'传递数据（其中prop为属性名称，与子组件的接收组件名相同,data为当前组件中的数据名称）
子组件通过props:['prop']接收父组件中prop属性的值传递给子组件；props也可以给父组件传递函数数据，父组件接收到的数据最终也会混入到vm中，数据在哪里，操作数据的方法就要定义在哪里，哪里需要操作数据，我们是把操作数据的方法传过来，让其调用
~~~

# 3、组件通信的方式

- 事件总线

~~~
vm和组件对象的关系
	vm实例化对象的原型是组件对象原型的原型
	$on $emit 等方法是在vm的隐式原型身上的（Vue的显式原型身上）

全局事件总线组件间通信 适用于任意组件间传递，必须理解
	创建一个中间人，让所有的组件都可以看到这个人，并且这个人可以使用$on和$emit（vm添加到Vue原型当中作为总线）
	在想要接受数据的组件内，找到中间人去绑定事件
	在想要发送数据的组件内，触发中间人绑定的事件
~~~

- 原型链

~~~
待学完后回来研究

vm原型对象就是组件对象的原型对象的原型对象
~~~

## 3.1 props

是组件通信最常用最简单的一种方式

~~~js
props组件通信，只适用于父子组件传递
	父传给子：可以传递函数数据和非函数数据（非函数数据实质是将父数据传递给子；函数数据实质上是从子获取数据）
	子传给父：通过调用父传递过来的函数数据，然后通过参数给父传递数据
	
不足：兄弟关系，就必须先把一个数据传递给父亲，然后再通过父亲传递给另一个组件的通信；使用最频繁

第一种写法：
	props:['proName']
第二种写法：
	props:{
		//写对象，可以对传递过来的属性值类型进行限定
		objName:Function
	}
第三种写法：
	props:{
		//这是一个配置对象，它可以限定属性值的更多
		objName:{
			type:Function,//Function Number
			required:true,//代表必须传值
       default:10,//默认值，不传值就默认用10,与required互斥
       validator:function(value){
         return value>=0
       }
		}
	}
~~~

## 3.2 自定义事件

适用场景：专门子向父通信

~~~
自定义事件：
	自己定义的事件：事件类型（自己定义无数个）和回调函数（自己定义自己触发，无默认传参）
	系统定义的事件：事件类型（固定几个）和回调函数（自己定义系统触发 默认参数是时间对象）
	
//对父组件中子组件对象（自定义组件）声明ref='aa'的属性绑定自定义事件
this.$refs.aa.$on('name',this.method)//绑定当前组件的方法

//在子组件中通过$emit进行自定义事件的触发 分发 调用回调
this.$emit('name',obj)//调用自定义name的函数，并给该函数传递obj参数

专门子向父通信
	做法：在父组件当中可以看到子组件对象，给子组件对象绑定自定义事件$on，回调函数在父组件中
			 在子组件当中，我们需要传递数据的地方，去触发自己身上的事件$emit，调用回调函数中传参给父组件
			 $off:解绑事件
			 $once:绑定只能触发一次的事件
	接受数据的组件必须能看到与绑定事件的组件对象，才能绑定
	发送数据的组件必须能看到绑定了事件的组件对象，才能触发事件

因为父组件内部可以看到子组件对象，可以给子组件对象绑定事件，回调函数在父组件定义
~~~

## 3.3 LocalStorage的使用

~~~js
浏览器本地的一个小型数据库，以键值对的形式存储数据

watch:{
  todos:{
    deep:true,//深度监视  深度监视可以监视到数组本身的数据，也可以监视到
      //一般监视监视的是数组的数据，但是数组内部对象的数据监视不到
    handler(newVal,oldVal){
      //只要todos数据发生变化，就把变化后的颚数据存储到localStorage当中
      //localStorage 是前端本地存储的方案，是一个小型的数据库，存储到localStorage当中的东西就会自动转化为字符串
      //localStorage当中有4个Api
      localStorage.setItem('key',value) 存储数据
      localStorage.getItem('key') 获取特定数据
      localStorage.removeItem('key') 删除特定数据
      localStorage.clear() 清空所有数据
      
      //不能直接存对象数据类型，因为对象数据全部都会私自转基本，数据类型就变了
    }
  }
}
~~~

## 3.4 全局事件总线

适用场合：任何场合

~~~js
事件总线（对象）满足的两个条件：1、所有的组件对象都能找到它 2、可以调用$on和$emit
	在vue当中一般都是选择vm作为全局事件总线
	
A、B相互之间传递数据
	在A当中可以获取到bus绑定事件：this.$bus.$on，回调函数留在了绑定事件的地方（A），回调函数在那个组件，哪个组件就是为了接收数据
	在B当中也可以获取到bus触发事件：this.$bus.$emit，在B当中触发总线身上的事件。B当中写的触发，B就是传递数据的一方

new Vue({
  beforeCreate(){
    Vue.prototype.$bus=this //配置总线 就是把vm挂到Vue的原型上，让所有的组件对象都能找到它，进而调用$on和$emit
  },
  ../...
})
	
~~~

## 3.5 消息订阅与发布

适用场景：用法类似于全局事件总线，vue当中几乎不用

~~~
github上下载源码 PubSubJS第三方插件

订阅者：PubSub.subscribe() 是接受数据的组件
发布者：PubSub.publish() 是发送数据的组件

不足：订阅者的回调函数里面形参第一个必须有，而且是为了接收发布者的消息类型的，没有实际意义，必须写上
~~~

## 3.6 插槽

### 3.6.1 默认插槽

默认插槽只能有一个

~~~html
<slot>
	//slot内部的东西，是等待父组件使用的时候给传过来
</slot>

父组件中必须按规定格式使用进行传值
<SubTab>
	<template>
		//在这中间放入内容，会传递到子组件的插槽中
	</template>
</SubTab>

<script>
import SubTab from '../'
  
  ../..
  components:{
    SubTab
  }
</script>
~~~

### 3.6.2 具名插槽

~~~html
<slot name = 'xxx'>
	//slot内部的东西，是等待父组件使用的时候给传过来
</slot>

父组件中必须按规定格式使用进行传值
<SubTab>
	<template slot="xxx">//为具名插槽传递数据
		//在这中间放入内容，会传递到子组件的插槽中
	</template>
</SubTab>

<script>
import SubTab from '../'
  
  ../..
  components:{
    SubTab
  }
</script>
~~~

无论是默认插槽还是具名插槽，里面都可以写东西，也可以不写东西；如果写了东西，就看用的时候有没有给slot传递新的数据。如果传递了，原有的就被覆盖了；如果没有传递新的东西，默认显示的就是slot中的东西

### 3.6.3 作用域插槽

父子组件之间传输数据，由子展示，数据结构由父说了算

~~~html
<slot name = 'xxx'>
	//slot内部的东西，是等待父组件使用的时候给传过来
</slot>

//作用域插槽
<template>//为具名插槽传递数据
  <ul>
    <li v-for='todo in todos' :key='todo.id'>
    	<slot :todo='todo'>//插槽向父组件传递数组中的数据
      	{{todo.content}}
      </slot>
    </li>
  </ul>
</template>
<script>
	props:['todos']
</script>
父组件中必须按规定格式使用进行传值
<SubTab>
	<template slot="xxx">//为具名插槽传递数据
		//在这中间放入内容，会传递到子组件的插槽中
	</template>
</SubTab>
<ScopeChild :todos='todos'>
	//数据是由父组件传给子组件去展示的，子组件展示数据的过程当中，数据的结构是由父组件说了算
  <template slot-scope='aa'>
  	aa:{
    	todo:todo//封装在对象中,对象中展示传过来的数据
    }
  </template>
  <template slot-scope='{todo}'>
    <span v-if='todo.xxx'>{{todo.content}}</span>
  </template>
   <template slot-scope='scopeProps'>
     <span v-if='scopeProps.todo.xxx'>{{scopeProps.todo.content}}</span>
  </template>
</ScopeChild>

<script>
import SubTab from '../'
import ScopeChild from '../'  
  ../..
  components:{
    SubTab，
    ScopeChild
  },
  data(){
    return{
      todos:[{},{},{}]
    }
  }  
</script>
~~~

