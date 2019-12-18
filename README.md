# vue_sell_cube

## Build Setup

``` bash
# install dependencies
npm install

# serve with hot reload at localhost:8080
npm run dev

# build for production with minification
npm run build

# run unit tests
npm run unit

# run e2e tests
npm run e2e

# run all tests
npm testfrom '../../components/cartControl/cartcontrol.vue';

# 新建一个项目
vue create 项目名

# 运行项目
npm run serve      //此处与旧版本不一样

```
#参考资料
1.http://es6.ruanyifeng.com/#docs/string

#坑点
1.注意要是保持驼峰命名，驼峰大写字母前面要加-,HTML不区分大小写这个是原因

2.为了解决在PC端点击时触发两次, 使用event._constructed,如果_constructed说明是原生的事件，不处理，直接返回

#使用组件的顺序
1.import组件
  import 组件变量名 from 组件文件路径
  Ps. import cartControl 

2.注册组件
  ```vue 
    components: {
          '组件变量名': 组件名称(相当于类名)
    }
  ```   
3.通过Vue.set(变量, '属性', 值)，设置变量不存在的属性值是，可以被Vue观察到，从而导致界面刷新

#CSS
1. font-size: 0px 为了去掉元素之间的间隙

2. padding: 有时候可以在元素不增大的基础上，增大操作区域

#动画
##当在VUE中与V-IF V-SHOW V-For一起使用时，才会触发动画效果

1. 当V-SHOW触发时，会触发`enter`和`leave`两个事件

2. 简单认为`move-enter`进入时效果，`move-leave`退出时效果

##实现动画的基本步骤
1. 在div中定义`transition="xxx"`
2. 在css中加入`&.xxx_transition`, 表示动画最终状态
    ``` vue 
      transition: all 0.4s linear //全部移动，0.4秒，线性移动
      transform: translate3d(0, 0, 0) //最终移动到X->0 Y->0 Z->0
    ``` 
3. 在css中加入&.xxx_enter, 表示动画进入位置
4. 在css中加入&.xxx_leave, 表示动画离开位置

#VUE访问子组件
1. v-ref:xxx定义, 使用this.$refs.xxx来调用该元素的方法

#VUE访问元素
1. `this.$els`访问元素

#小球动画 Q&A
1.Q：为什么把balls设置为5  
　A: 认为就算连续点击，最大在空中飞行的小球不会超过5个
  
#CSS小技巧
1. 为了让加载图片时，不出现伸缩，padding-top为100%，此时高度以width为基准进行计算

#使用better-scroll组件
1. 应用组件库
   import BScroll from 'better-scroll'
2. 定义一个div，承载内容 使用v-el以便步骤四使用 
    ```vue 
   <div v-el:xxx>
    <div>
    ``` 
3. 固定视口高度，防止出现滚动条, 定位使用绝对定位  
    ```vue 
    position: absolute
    bottom: 0             //这个没有理解  
    overflow: hidden      //禁止出现浏览器滚动条, 保证bscroll在视口之内
    ```
4. 使用的代码套路   
    ```vue 
    created() {
          this.$nextTick(() => {
            if (!this.scroll) {
              this.scroll = new BScroll(this.$els.xxx, {
                click: true
              });
            } else {
              this.scroll.refresh();
            }
          });
    }
    ```
    
#防止click冒泡
1. 使用`click.stop.prevent`

#组件消息
1. 分发消息
    ```vue 
    this.$dispatch('消息名', 参数);
    ``` 
2. 拦截消息
   ```vue 
    events{
      '消息名'(参数) {
      }
    }
    ``` 
#filter
如果需要特殊显示，可以使用filter
1. 定义过滤器 ` 过滤器名称`
2. 拦截过滤器
   ```vue 
    filters: {
        过滤器名称
    }
   ```
#watch
1. 用于观察变量状态变化

#localstorage  
1. window.localStorage  
   详见 store.js   

#项目打包  
1. 运行npm run build  
  执行package.json中的build部分
    "scripts": {
      "build": "node build/build.js",
    }
2. 会在当前项目下产生一个dist目录  
  


  
For detailed explanation on how things work, checkout the [guide](http://vuejs-templates.github.io/webpack/) and [docs for vue-loader](http://vuejs.github.io/vue-loader).
