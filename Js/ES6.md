# ES6
## 变量
### let
- 特点 ：
> 1. 在块作用域内有效
> 2. 不能重复声明
> 3. 不会预处理，所以没有提升
### const
- 定义常量，不能被修改
## 变量的结构复制
- 理解：从对象或者
数组中提取数据，并复制给变量（多个）
## 模版字符串
- 简化字符串的拼接，
```
`${}`
```
## 对象的简写方式
```javascript
//老版本
let username = 'kobbe';
let age = 20;
let obj = {
    username: username,
    age: age,
    getName: function (){
        return this.username;
    }
}

//简化写法（对象属性名和要赋值的变量名一样的情况）
let obj = {
    username,
    age,
    getName(){
       return this.username; 
    }//把冒号和funcion去掉
}
```
##  箭头函数
- 箭头函数没有自己的this，箭头函数的this不是调用的时候决定的，而是在定义的时候所处的对象就是他的this。
- 箭头函数的this看外层是否有`函数`，如果有，外层函数的this就是内部箭头函数的this，如果没有则this是window
## 三点运算符
- rest（可变）参数，用来取代arguments，但比arguments灵活，arguments是伪数组，这个是真数组也就是可以用数组的方法
## 形参默认值
```javascript
function Point(x = 0,y = 0){

}
```
## promise对象
- 理解：Promise对象：可以将一步操作以同步的流程表达出来，避免了层层嵌套的回掉函数，ES6的Promise是一个构造函数，用来生成promise实例
- promise对象的3个状态
 1. pending：初始化状态
 2. fullfilled：成功状态
 3. rejected： 失败状态
 ```javascript
 //创建promise对象
 let promise = new Promise((resolve,reject)=>{
     //初始化primise状态
     //执行异步操作，通常是发送ajax请求，开启定时器
     setTimeout(()=>{
         //根据异步任务放回结果来修改promise的状态
         //异步执行成功
         resolve(“ddd”)//修改promise的状态为fullfilled成功的状态，这里会去调用成功的回掉函数
         //失败的】reject()//修改promise的状态为rejected失败的状态

     },2000)
 })
//有连个参数，第一个是成功的回掉，第二个是失败的回掉
 promise.then((data)=>{},(error)=>{})
 ```
 ## acync(源于es7)
 - 概念：真正意义上解决异步回掉的问题，同步流程表达异步操作
 - 本质：Generator的语法糖
>语法：
>> async function foo(){
     await 异步操作；
 }

> 特点： 
>> 1. 不需要像Generator去调用next方法，遇到await等待，当前的异步操作完成就往下执行.
>> 2. 放回的总是Promise对象，可以用then方法进行下一步操作。
>> 3. async取代Generator函数的*号，await取代Generator的yield。
- 使用
```javascript
async function getNews(url){
    return new Promise((resolve,reject)=>{
        $.ajax({
            method: 'GET',
            url,
            success: data=>resolve(data),
            error: error=reject(error)
        })
    })
}
async function sendXml(){
    let result = await getNews('htttp://ddd')//这里的返回值就是上面给resolve的数据
    result = await getNews('http://'+ result.url)//用上次请求得到的数据进行下一次请求，await会等待异步执行完后执行下面
}
sendXml()
```
## class类
- 通过class定义是想类的继承
- 在类中通过constructor定义构造函数
- 通过new来创建类的是咧
- 通过extends来是想类的继承
- 通过super调用弗雷的构造方法
- 重写父类中继承的一般方法
## 以下封装axios代码来自csdn
```js
import axios from 'axios'
import qs from 'qs'

axios.interceptors.request.use(config => {
    return config;
},error => {
    return Promise.reject(error)
})

axios.interceptors.response.use(res => {
    return res.data

},error => {
    return Promise.reject(error)
})

const errorState = (res) => {

    if (res && (res.status === 200 )){
        return res

    } else {

        console.log("zhuangtai budui")
    }
}

const successState = (res) => {

    return res

}

const apiAxios = (method, url, params) => {

    return new Promise((resolve, reject) => {
        axios({
            method,
            url,
            params: method === 'GET' || method === 'DELETE' ? params : null,
            data: method === 'POST' || method === 'PUT' ? qs.stringify(params) : null,
            timeout: 10000
        })
        .then(res => {
            successState(res)
            resolve(res)
        })
        .catch(res => {
            errorState(res)
            reject(res)
        })

    })

}

export default {
    getAxios: (url, params) => apiAxios('GET', url, params),
    postAxios: (url, params) => apiAxios('POST', url, params),
    putAxios: (url, params) => apiAxios('PUT', url, params),
    delectAxios: (url, params) => apiAxios('DELECT', url, params),
}
```