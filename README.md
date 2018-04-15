# pos

## 1.开发环境搭建:Webpack+Vue-router

$ npm install vue-cli -g
$ vue init webpack pos
$ npm install

修改app组件,新建组件pos,修改路由文件index.js

iconfont图标库,新建组件leftnav

$ npm install element-ui --save
main.js内引入,并全局Vue.use
import ElementUI from 'element-ui'
import 'element-ui/lib/theme-default/index.css'

$ npm install axios --save
在pos组件内import axios from 'axios'
钩子函数created拉取远端数据

实现订单操作方法
vue的filter传入箭头函数,要注意花括号的使用
slot-scope替代scope,v2.5后的更改
利用elementUI提供的$message回复

项目打包注意config下index.js的路径assetsPublicPath:'./',绝对路径=>相对路径

