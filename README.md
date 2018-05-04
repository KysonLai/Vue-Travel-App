# Vue去哪儿网App

#### 项目介绍
参照教程，用Vue+一些小插件搭建的demo

#### 搭建过程
1.编辑index.html中的<meta>适配移动端

2.在main.js中

  引入reset.css 重置移动端样式

  引入border.css

  引入fastclick，并添加fastclick.attach(document.body) 因为移动端中某些浏览器click事件存在300毫秒延迟

  引入stylus和stylus-loader，<style lang="stylus">

3.home页面

  Header组件

    基本html css

    引入iconfont

    代码优化

      在styles下创建varibles.styl文件，声明一些全局样式变量，然后在组件中@import 'xxx.styl',再使用相应的样式即可，这种做法便于维护

      打开build下的webpack.base.conf.js，在resolve中添加一些路径别名，注意如果是css中的路径前面应该加个~ 然后重启服务

  Swiper组件

    引入Vue-Awesome-Swiper

  Icons组件

    基本的html和css，添加swiper和computed来实现图标分页滑动

    在styles下创建mixins.styl文件，声明一些全局样式，然后在组件中@import 'xxx.styl',再使用相应的样式即可

  Recommend组件

  Weekend组件

  引入axios，在static下创建mock，存放json数据，然后父组件向子组件传值

  swiper默认显示最后一张图片是因为，刚开始传递过去的list是空值，所以应该在<swiper>中加入v-if

4.city页面

  创建City组件并配置路由

  Header组件

  Search组件

  List组件

    引入better-scroll

  Alphabet组件

  在City组件中引入axios调用数据,父组件向子组件传值

  兄弟组件之间的联动

    click事件

      在Alphabet组件中绑定click事件，click事件发生时将值传给City组件，City组件再将值传递给List组件

      在List组件中给字母的area搬定ref，增加watch来监听，这样点击了哪个元素就可以获取到哪个元素，再通过better-scroll的方法来滚到相应
位置
    scroll事件

      在Alphabet组件中绑定touchstart，touchmove，touchend事件，在data中添加 touchStatus来记录touch的状态

      增加computed，添加letters数组来存取字母，在touchmove中获取所touch的元素的序号

  List组件优化

    把startY写在updated就不用每次触发事件都重新赋值

    函数节流，当scroll的时候touchmove的执行频率非常高，通过timer设定时间，如果这个时间内再次触发了这个事件会把之前的东西先清除

	搜索功能

    添加search-content，在input中添加v-model双向绑定keyword，然后在父组件传来的cities里查找，并将结果存储到list中

    加入better-scroll让搜索结果可以滚动

  引入vuex管理公共数据

    引入vuex，在src下创建store目录，创建index.js文件并引用vuex

  优化vuex

    在store下创建state.js和mutations.js，内容写到这里面，然后在index.js中引入即可

    在需要使用vuex数据的地方import mapState， mapMutations，然后映射一下，就可以调用

  使用keep-alive优化网页性能

    每次切换路由都会发送一个axios请求，影响性能，在App.vue中用<keep-alive>包裹<router-view>，这样就可以从内存中调用

    在Home.vue中把vuex中的city数据拿到，然后给axios请求传参，增加activated函数，来判断这次的页面是否要重新请求

5.detail页面

  给recommend配置路由，创建Detail.vue

  创建Banner.vue

  公共图片画廊组件

    创建scr > commong > gallary > Gallary.vue

    打开build下的webpack.base.conf.js，在resolve中添加一些路径别名，注意如果是css中的路径前面应该加个~ 然后重启服务

    然后在Banner.vue中引用Gallary即可

    Gallary.vue

	Header渐隐渐现

			通过绑定动态样式来实现渐隐渐现

	通过deactivated解绑全局事件

	List组件

		使用递归组件来遍历数据

	使用axios获取数据

	在keep-alive中增加exclude="Detail"，取消这个页面的缓存

	在router下的index.js中增加    scrollBehavior (to, from, savedPosition){ return {x:0,y:0} }使路由切换时都回到顶部

	封装动画
		创建scr > commong > fade > Fade.vue

#### App截图
![首页（1）](https://github.com/KysonLai/Imgs/blob/master/Vue-Travel-App/首页（1）.png)
![首页(2)](https://github.com/KysonLai/Imgs/blob/master/Vue-Travel-App/首页（2）.png)
```
================================================================================================
```
![城市选择](https://github.com/KysonLai/Imgs/blob/master/Vue-Travel-App/城市选择.png)
![搜索](https://github.com/KysonLai/Imgs/blob/master/Vue-Travel-App/搜索.png)
```
================================================================================================
```
