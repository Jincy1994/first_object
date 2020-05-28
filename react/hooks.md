# hooks
## hooks说明：
- react 16.8的新增功能
- state和生命周期函数都是class式组件独有的，所以为了解决函数式组件对这些问题的解决就有了hooks

## hooks的使用：
### useState
1. 引入useState方法（结果是一个数组，数组里面有第一个是状态，第二个是方法可以理解成更改状态的方法）
```javascript
import React，{useState} from 'react'
```
2. 使用（因为是匿名的方法所以可以随便什么名解构出来）函数式组件里面可以使用多个useState
```Javascript
const Counter = () => {
    const [count,setCount] = useState(0)
    console.log(count)   // 0
    const [title,setTitle] = useState("title")
    console.log(title)   // title
    return {
        <div>
            <button onClick={() => { setCount(count - 1)}}></button>
        </div>
    }
}

render{
    <Counter />,
    document.querySelector('#root')
}
```
### useEffect
1. 引入useState方法（里面的参数是回调函数）
```javascript
import React,{ useState, useEffect } from 'react'
```
2. 使用（第一次加载和每次组件更新时就会出发这个回调函数跟class组件的componentDidMount和componentDidUpdate一样）
```javascript
useEffect (() => {
    console.log("更新了")
})
```






