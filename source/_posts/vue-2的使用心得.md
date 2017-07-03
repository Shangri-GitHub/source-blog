---
title: vue 2的使用心得
date: 2017-05-25 18:13:01
tags: ['vue 表单验证','vue跳转页面','vue拦截器'] 
---

> elementUI 网站快速成型工具

[elementUI官网](http://element.eleme.io/#/zh-CN)   [vue官网](http://vuejs.org/)  [vue-router官网](http://router.vuejs.org/zh-cn/)

##### 页面之间的路由配置及传参

```  html

// home.vue中写入
<template>
    <div>
        <router-link to="/nav">跳转页面</router-link>
        <el-button type="primary" @click="goHeader">主要按钮</el-button>
        <router-link :to="{ name: 'header', params: { userId: 123 }}">header页面传参</router-link>
    </div>
</template>
<script>
    export default{
        name: 'home',
        data(){
            return {}
        },
        methods: {
            goHeader: function () {
                // 字符串
                this.$router.push('header/123')
                // 对象
                this.$router.push({path: 'header/0'})
                // 命名的路由
                this.$router.push({name: 'header', params: {userId: 1}})
            }
        }
    }
</script>

<style>
</style>

// 在router.js文件中写入
// 引用模板
import header from '../components/header.vue'
import home from '../components/home.vue'
import nav from '../components/frame/nav.vue'
// 配置路由
export default [
    {
        path: '/',
        component: home
    },
    {
        path: '/nav',
        component: nav
    },
    {
        path: '/header/:userId',
        name: 'header',
        component: header
    }
]


```

##### vue如何使用组件

``` html
<template>
    <div>
        <steps></steps>   
    </div>
</template>
<script>
// 第一种方法
    import Steps from './steps.vue'  //此处引入
    export default{
        components: {Steps},   // 此处注册组件，调用的时候，要用大写
        name: 'home',
        data(){
            return {
                dialogFormVisible: false,
            }
        },
    }
// 第二种方法
    var Steps = require('./steps.vue'); // 返回的是一个组件，必须注册才能使用
    export default{
        components: {'steps': Steps},
        //components: {'steps': require('./steps.vue')},  // 换了一种表达式
        name: 'home',
        data(){
            return {
                dialogFormVisible: false,
            }
        },
    }
</script>

<style scope>
</style>
```

#####   vue2.0之axios使用
``` javascript
发送一个get请求：
axios.get('/user', {
params: {
ID: 12345
}}).then(function (response) {
console.log(response);
}).catch(function (error) {
console.log(error);
});
第一种方法：
 var params = {
     loginCode: this.loginCode,
     passWord: this.passWord,
     url: 'yatouLogin'
 }
 // 发送post请求把对象转成字符串
 var postparams = new URLSearchParams();
 postparams.append('loginCode', this.loginCode);
 postparams.append('passWord', this.passWord);
 this.$http.post('yatouLogin', postparams).then(function (res) {
     console.log(res);
     if (res.data.success) {
         that.$router.push({path: 'nav'})
         localStorage.clear('powerList');
         localStorage.setItem('powerList', JSON.stringify(res.data.data))
     } else {
         that.$message.error(res.data.errMsg);
     }
 }).catch(function (response) {
     console.log(response);
});

第二种方法：
在main.js中配置axiso的属性
import axios from 'axios'
import qs from 'qs'

Vue.use(qs);
axios.defaults.headers.post['Content-Type'] = 'application/x-www-form-urlencoded;charset=UTF-8';           //配置请求头
axios.defaults.baseURL = 'http://wx.bokedata.com/yatou/';
//设置携带session，解决跨域
axios.defaults.withCredentials = true;
Vue.prototype.$http = axios;
const router = new VueRouter({
  routes
})
// 拦截器处理post的参数
axios.interceptors.request.use((config) => {
    if(config.method  === 'post'){
        config.data = qs.stringify(config.data);
    }
    return config;
},(error) =>{
     _.toast("错误的传参", 'fail');
    return Promise.reject(error);
})
// 调用接口
var params = {
    loginCode: this.loginCode,
    passWord: this.passWord,
    url: 'yatouLogin'
}
this.$http.post(params.url, {
    'loginCode': params.loginCode,
    'passWord': params.passWord
}).then(function (res) {
    console.log(res);
    if (res.data.success) {
        that.$router.push({path: 'nav'})
        localStorage.clear('powerList');
        localStorage.setItem('powerList', JSON.stringify(res.data.data))
    } else {
        that.$message.error(res.data.errMsg);
    }
})


```

##### 调用组件及传值问题
``` html
向main.js中引入组件
import componnets from './components/common/component.vue'
Vue.component('component', componnets)
<el-button type="primary" @click="componentProp()">主要按钮</el-button>
<!--组件调用 :xx 为设置变量-->
<component :is="dialogTest" :id="id" v-if="destroyDialog"></component>
methods: {
     // 向父页面传过来的值
     componentProp(){
         this.destroyDialog=true;
         this.id = '001'
         this.dialogTest = 'component'
         this.destroyDialog=true;
     },
 }

```

##### 组件的模版页面
``` html

<template>
    <div class="component">
        <el-dialog title="收货地址" :visible.sync="dialogFormVisible">
            <el-form :model="form">
                <el-form-item label="活动名称">
                    <el-input v-model="form.name" auto-complete="off"></el-input>
                </el-form-item>
                <el-form-item label="活动区域">
                    <el-select v-model="form.region" placeholder="请选择活动区域">
                        <el-option label="区域一" value="shanghai"></el-option>
                        <el-option label="区域二" value="beijing"></el-option>
                    </el-select>
                </el-form-item>
            </el-form>
            <div slot="footer" class="dialog-footer">
                <el-button @click="dialogFormVisible = false;cancal()">取 消</el-button>
                <el-button type="primary" @click="dialogFormVisible = false">确 定</el-button>
            </div>
        </el-dialog>

    </div>
</template>
<script>
    export default {
        data() {
            return {
                dialogFormVisible: false,
                form: {
                    name: '',
                    region: '',
                    date1: '',
                    date2: '',
                    delivery: false,
                    type: [],
                    resource: '',
                    desc: ''
                }
            };
        },
        // 父页面传过来的值
        props: ['id'],
        methods: {
            cancal(){
                // 父元素为关闭
                this.$parent.destroyDialog = false;
            }
        },
        mounted: function () {
            var that = this;
            console.log(this.id);
            this.dialogFormVisible = true

        }
    };

</script>
<style>
</style>
```

##### 表单验证
```
 <el-form :model="edit" :rules="rules">
            <el-form-item label="编码" prop="code">
                <el-input v-model="edit.code"></el-input>
            </el-form-item>
            <el-form-item label="电话号码" prop="telephone">
                <el-input v-model="edit.telephone"></el-input>
            </el-form-item>
            <el-form-item label="备注" prop="remark">
                <el-input v-model="edit.name"></el-input>
            </el-form-item>
</el-form>
  data(){
       return {
            edit: {},
            rules: {
                //编码输入框验证规则
                code: [
                    {required: true, message: '编码不能为空', trigger: 'blur'}
                ],
                //名称输入框验证规则
                name: [
                    {required: true, message: '名称不能为空', trigger: 'blur'}
                ],
                //备注输入框验证规则
                telephone: [
                    {required: true, message: '电话不能为空', trigger: 'blur'},
                    {
                        validator(r, v, b){
                            (/^\d{2,}$/).test(v) ? b() : b(new Error('请填写手机号'))
                        }
                    }
                ]
            }
        }
  

```

##### 拦截器的使用

``` javascript
axios.interceptors.response.use(function (response) {
    // 处理响应数据
    if (response.data.respCode == '000001') {
        // ElementUI.Message.error('服务器异常')
        ElementUI.MessageBox('此登录信息已过期，请重新登录', '提示', {
            confirmButtonText: '确定',
            type: 'warning'
        }).then(() => {
            router.replace({
                path: '/',
            })
        });
    }
    return response;
}, function (error) {
    // 处理响应失败
    if (error.response.status == 500) {
        ElementUI.Message.error('服务器异常')
    } else if (error.response.status == 404) {
        ElementUI.Message.error('资源不存在')
    } else if (error.response.status == 405) {
        ElementUI.Message.error('请求方法错误')
    }
});

```