# react-fetch
## fetch的get请求(fetch基于promise)
```js
fetch("url")
.then(res => {
    res.json();
})
.then(data => {
    
})
```
## fetch的post请求
```js
improt queryString from 'querystring'
//ajax对象类型的参数
//可是这里的body是字符串类型（之间用&连接），所以需要用到querystring进行对象专程字符串
fetch("url"，{
    method: "POST",
    headers: {
        'content-type': 'application/json',
        'Accept': 'application/json,text/plain,*/*'
    },
    body: queryString.stringify({
        user_id: ""
    })
})
.then(res => {
    res.json();
})
.then(data => {
    
})
```