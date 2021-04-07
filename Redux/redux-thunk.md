## redux-thunk 是redux的中间件处理异步action
- 想看redux还有什么异步action的中间件去redux官网观摩一下
- store.js
```js
//applyMiddleware用来设置redux中间件的
import { createStore,applyMiddleware } from 'redux'
import rootReducer from './reducers'
import thunk from 'redux-thunk'

export default createStore(
    rootReducer,
    applyMiddleware(thunk)
    )
```
- action
```js
export const decrementAsyns = (id) => {
    return dispatch => {
        setTimeout(() => {
            dispatch({
                ype: actionType.CART_AMOUNT_DECREMENT,
                payloade: {
                    id
                }
            })

        },2000)
    }
}

export const decrementAsyns = id => dispatch =>{
        setTimeout(() => {
            dispatch({
                ype: actionType.CART_AMOUNT_DECREMENT,
                payloade: {
                    id
                }
            })
        },2000)
    }
}
```