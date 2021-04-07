# Redux
## Redux的使用的三大原则
- 唯一的数据源
- 状态是只读的
- 数据的改变必须通过纯函数完成，也就是reducer是纯函数才可以
### 纯函数：
就是没有任何副作用的函数
## 使用redux时常用的目录解构
- reducers
    - cart(reducer,不会就有一个reducer所以)
        - index.js
    ```js
    import actionType from "../actions/actionType"

    const initState = [{
        id: 1,
        title: 'Apple',
        price: 8888,
        amount: 10
    },
    {
        id: 2,
        title: 'oringe',
        price: 33333,
        amount: 10
    }]

    export default (state=initState,action) => {
        switch(action.type){
            case actionType.CART_AMOUNT_INCREMENT:
                return state.map(item => {
                    if(item.id === action.payload.id){
                        item.amount +=1

                    }
                    return item
                })

            default:
                return state
        }


    }
    ```
    - index.js
    ```js
    //导出reducer时用到合并reducers的方法
    //combineReducers
    import { combineReducers } from 'redux'
    import cart from  './cart'

    export default combineReducers({
        cart
    })
    ```
- actions
    - actionType
    ```js
    export default  {
    CART_AMOUNT_INCREMENT: 'CART_AMOUNT_INCREMENT',
    CART_AMOUNT_DECREMENT: 'CART_AMOUNT_DECREMENT'
    }
    ```
    - cart.js
    ```js
    import actionType from './actionType'
    //在工作中，常用的一种方式是使用actionCreator，他是一个方法，返回一个对象，这个对象才是真正的action
    export const increment = (id) => {
        return {
            type: actionType.CART_AMOUNT_INCREMENT,
            payload: {
                id
            }
        }
    }

    export const decrement = (id) => {
        return {
            type: actionType.CART_AMOUNT_DECREMENT,
            payloade: {
                id
            }
        }
    }
    ```
- store.js 
```js
//创建store把reducers放进去
import { createStore } from 'redux'
import rootReducer from './reducers'

export default createStore(rootReducer)
```

## 使用redux时（redux使用时组件之间要用props对store进行传递）
```js
import { increment, decrement} from '../../actions/cart'

this.props.store.dispatch(increment(1))
this.props.store.getState().cart
```

## 总结
- 在action里定义处理的属性名，给一个方法名的对象里面有一个type的属性，通过这个type属性的值reducer就知道调用什么处理
- reducer里对state进行初始化，reducer的参数是store的state，和action；用 switch(action.type)进行处理分类
- 调用时；取store里的数据用getState().cart
- 分配方法用dispatch(increment(1))
- 因为有很多reducer所以在导出是用合并reducer导出`combineReducers`
- 因为用redux需要组件之间用props传递store所以可以用react-redux
                                                                                                                                                                                                                                                                                                                                         