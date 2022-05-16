# 1、简介

- 什么是路由

~~~
是一个vue官方的一个插件
专门用来实现一个SPA应用
基于vue的项目基本都会用到此库
vuex vue-router  这两个插件使用比较广泛
~~~

- 什么是SPA

~~~
单页web应用（single page web application，SPA）
	整个应用只有一个完整的页面（这个页面由多个组件组成）
	点击页面中的连接不会刷新页面，本身也不会像服务器发送请求
	当点击路由连接时，只会做页面的局部更新（组件切换）
	数据都需要通过ajax请求获取，并在前端异步展现
~~~

- 路由组件和非路由组件

~~~
组件：一个组件包含html css js img的结合体 定义、注册、使用
路由组件：定义、注册（不是在另外一个组件当中注册，是在路由当中注册的） 使用
非路由组件：定义 注册（一定是在另外一个组件当中去注册的） 使用
~~~

- 前台路由

~~~
是一个key：value的映射关系

前台路由  路径  和 要显示的组件
{
	path:'/home',
	component:Home//注册路由组件
}
当我们点击链接的时候，路径会发生变化，但是不会像服务器发送普通请求，而是去显示对应的组件，显示组件过程当中发ajax请求吧数据渲染在组件当中
~~~

- 后台路由

~~~
路径和匹配的函数
app.get('/user/info',function(){})
当点击链接的时候，路径会发生变化，而且会想服务器发送普通请求，然后匹配到后端的一个函数处理这个路由的请求，返回需要的数据
~~~

~~~
简单的理解前台路由：路由可以实现组件的切换和跳转
~~~

# 2、非路由组件

~~~js
<div>
 <Component/>  
</div>

import Component from '@/componnet'

export default {
  name:'',
  components:{
    Component
  }
}

~~~

# 3、路由组件

- 1、安装路由

~~~
npm i vue-router -S
~~~

- 2、引入并声明使用

~~~
import Vue from 'vue'
import VueRouter from 'vue-router'
Vue.use(VueRouter)
~~~

- 3、实例化一个路由器对象并暴露

~~~js
export default new VueRouter({
	//5、配置路由
	routes:[
	{
		path:'/home',
		component:Home//注册路由组件
	},
	{
		path:'/about',
    component:About
	},
	{//重定向路由
		path:'/',
		redirect:'/home'//重定向路径
	}
	]
})
~~~

- 4、将实例化的路由器对象在new Vue的配置对象中使用（在index文件中）

~~~js
import Home from '@/components/Home'

export default new VueRouter({
	//5、配置路由
	routes:[
	{
		path:'/home',
		component:Home//注册路由组件
	},
	{
		path:'/about',
    component:About
	},
	{//重定向路由
		path:'/',
		redirect:'/home'//重定向路径
	}
	]
})

~~~

- 5、new路由器的时候配置对象当中的代码

~~~
见上面
~~~

- 路由标签

~~~
<router-link to='home'></router-link> 最终解析到页面还是a标签,通过to跳转到页面

<router-view></router-view>//自动跳转切换,不用手动配置:跳转router-link中路由的数据

~~~

- main.js

~~~
new Vue({
	router //所有的组件当中都可以通过this.$router拿到路由器对象，还可以通过this.$route拿到当前路由对象 
})
~~~

## 3.1、子路由二级路由

~~~
routes:[
	{
		path:'/home',
		component:Home,//注册路由组件
		children:[
			{
				path:'/message',
				component:ChildrenComponent
			}
		]
	},
	{
		path:'/about',
    component:About
	},
	{//重定向路由
		path:'/',
		redirect:'/home'//重定向路径
	}
]

//通过children可以无限嵌套路由
~~~

# 4、路由传参

## 4.1 路径传参

~~~
路由传参写法： 只能传递params和query参数 /params参数是路径的一部分，?query参数不占路径
1、路径的原始写法：字符串拼接
	:to="'/home/message/msgdetail/'+message.id+'?content='+message.content'"
	
	path:'msgdetail/:msgid'//msgid是用来接受路径传过来的params参数，匹配的同时把参数解析出来，添加到这个路由对象当中
2、路径的模板写法：模板字符串拼接
	:to="'/home/message/msgdetail/${message.id}?content=${message.cotent}'"
3、路径的对象写法：需要给路由起个名字
	:to="{name:'routeName',params:{msgid:message.id},query:{content:message.content}}"
~~~

## 4.2 props

~~~
props在index中配置，props:['data']在组件中使用,其中data是路由中的数据名

props:true
	1、如果写的是布尔值，值为true代表会把传递过来的路径当中的params参数映射为要显示的组件当中属性去使用
props:{username:'username'}
	2、如果写对象，props是用来把需要自己额外传递的静态数据映射为组件当中的属性，这个对象用法只能传递一些自己添加的额外数据
props(route){
	return {
		msgid:route.params.msgid,content:route.query.content
	}
}
	3、如果写函数，可以让我们自己把params参数和query参数一起映射为组件当中的属性
~~~

## 4.3 总结

~~~
路由传参：
	第一步：把参数卸载路径当中
	第二步：点击路由链接的时候，路径会去路由器当中的路由当中匹配，匹配同时会把参数解析添加到路由对象当中
	第三步：匹配成功，显示对应的路由组件同时把当前的路由对象传递到路由组件当中，我们就可以从路有对象当中获取参数
	
路由组件和非路由组件的最大区别：
	路由组件的生命周期是点击链接的时候才开始的，路由组件才会创建爱你，mounted才能执行；路由组件在切换的时候，会被销毁，显示的时候重新创建
	同一个路由组件传参显示不同数据，mounted回调只会执行一次，因为是同一个组件
	
缓存路由组件：
	使用vue的一个组件，可以保证切换组件的时候，原来显示的组件不被销毁
	<keep-alive include="Home">
			<router-view></router-view>
		</keep-alive>
~~~

# 5、路由功能

## 5.1 编程式导航

~~~
//跳转路由切换组件，有历史记录，返回的时候可以返回到之前去过的地方
this.$router.push('/home/news/'+new.id+'?content='+new.content)
this.$router.push('/home/news/${new.id}?content=${new.content}')
this.$router.push({name:'newsDetail',params:{newid:new.id},query:{content:new.content}})
//跳转路由切换组件，没有历史记录，返回的时候不可以返回到之前去过的地方
this.$router.replace('')
//请求（返回）上一个记录路由
this.$router.back()
//请求（返回）上一个记录路由
this.$router.go(-1)
//请求下一个记录路由
this.$router.go(1)
~~~

## 5.2 声明式导航

~~~
手动写<view-link>，通过to属性进行跳转导航
~~~

5.3 路由的两种模式

~~~
hash模式：
	路径中带# ：http://localhost:8080/#/home
	发请求的路径：http://localhost:8080 x
	响应：返回的总是index页面 ==> path部分(/home)被解析为前台路由路径
	
history模式：
	路径中不带#：http://localhost:8080/home
	发请求的路径：http://localhost:8080/home
	响应：404错误
	希望：如果没有对应的资源，返回index页面，path部分(/home)被解析为前台路由路径
		解决:添加配置
			devServer添加：historyFallback:true//任意的404页面会被替代为index.html
			output添加：publicPath:'/'，引入打包的文件时路径以/开头
~~~

